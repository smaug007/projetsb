# Détails Techniques Approfondis - Smart Building

## 📡 Communications Détaillées

### 1. I²C - Protocole et Implémentation

#### Principe de Fonctionnement
```
Master (Arduino)    Slave (Capteur)
    │                    │
    ├── START ──────────►│
    ├── ADDR + W ───────►│
    │◄──── ACK ──────────┤
    ├── REGISTER ───────►│
    │◄──── ACK ──────────┤
    ├── STOP ────────────►│
    │                    │
    ├── START ──────────►│
    ├── ADDR + R ───────►│
    │◄──── ACK ──────────┤
    │◄──── DATA ─────────┤
    ├── ACK ────────────►│
    │◄──── DATA ─────────┤
    ├── NACK ───────────►│
    ├── STOP ────────────►│
```

#### Code Exemple - MCP9808 (Température Extérieure)

```cpp
// Arduino Nano IoT - Lecture MCP9808
#include <Wire.h>
#include <Adafruit_MCP9808.h>

Adafruit_MCP9808 tempSensor = Adafruit_MCP9808();

void setup() {
  Serial.begin(115200);
  Wire.begin();
  
  if (!tempSensor.begin(0x18)) {
    Serial.println("Erreur: MCP9808 non trouvé!");
    while(1); // Bloquer si capteur absent
  }
  
  // Configuration résolution (optionnel)
  tempSensor.setResolution(3); // 0.0625°C (max précision)
}

void loop() {
  float tempC = tempSensor.readTempC();
  
  if (isnan(tempC)) {
    Serial.println("Erreur lecture température");
  } else {
    Serial.print("Température extérieure: ");
    Serial.print(tempC, 2);
    Serial.println(" °C");
  }
  
  delay(2000); // Lecture toutes les 2 secondes
}
```

#### Code Exemple - TSL2561 (Luminosité)

```cpp
// Arduino Nano Sense - Lecture TSL2561
#include <Wire.h>
#include <Adafruit_TSL2561_U.h>

Adafruit_TSL2561_Unified tsl = Adafruit_TSL2561_Unified(TSL2561_ADDR_FLOAT, 12345);

void setup() {
  Serial.begin(115200);
  
  if (!tsl.begin()) {
    Serial.println("TSL2561 non trouvé!");
    while(1);
  }
  
  // Configuration
  tsl.enableAutoRange(true); // Gain automatique
  tsl.setIntegrationTime(TSL2561_INTEGRATIONTIME_402MS); // Précision moyenne
}

void loop() {
  sensors_event_t event;
  tsl.getEvent(&event);
  
  if (event.light) {
    Serial.print("Luminosité: ");
    Serial.print(event.light);
    Serial.println(" lux");
  } else {
    Serial.println("Overload ou underflow");
  }
  
  delay(1000);
}
```

#### Code Exemple - LCD I²C

```cpp
// Arduino Nano IoT - Affichage LCD
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Adresse 0x27 ou 0x3F, 16 colonnes, 2 lignes
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();
  lcd.clear();
}

void displayMeasures(float tempInt, float hum) {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(tempInt, 1);
  lcd.print("C H:");
  lcd.print(hum, 0);
  lcd.print("%");
  
  lcd.setCursor(0, 1);
  lcd.print("Salle A102");
}

void displayCommand(String cmd) {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Consigne:");
  lcd.setCursor(0, 1);
  lcd.print(cmd);
}
```

---

### 2. Bluetooth BLE - Architecture Détaillée

#### Service BLE Personnalisé

```cpp
// Arduino Nano 33 BLE Sense - Périphérique BLE
#include <ArduinoBLE.h>
#include <Arduino_HTS221.h> // Temp/Humidité intégrée

// UUID Service personnalisé (générer avec uuidgen)
BLEService sensorService("19B10000-E8F2-537E-4F6C-D104768A1214");

// Caractéristiques BLE (lecture seule pour central)
BLEFloatCharacteristic tempCharacteristic("19B10001-E8F2-537E-4F6C-D104768A1214", BLERead | BLENotify);
BLEFloatCharacteristic humCharacteristic("19B10002-E8F2-537E-4F6C-D104768A1214", BLERead | BLENotify);
BLEFloatCharacteristic luxCharacteristic("19B10003-E8F2-537E-4F6C-D104768A1214", BLERead | BLENotify);

void setup() {
  Serial.begin(115200);
  
  // Init capteurs
  if (!HTS.begin()) {
    Serial.println("Erreur HTS221!");
    while(1);
  }
  
  // Init BLE
  if (!BLE.begin()) {
    Serial.println("Erreur BLE!");
    while(1);
  }
  
  // Configuration BLE
  BLE.setLocalName("NanoSense-A102");
  BLE.setAdvertisedService(sensorService);
  
  sensorService.addCharacteristic(tempCharacteristic);
  sensorService.addCharacteristic(humCharacteristic);
  sensorService.addCharacteristic(luxCharacteristic);
  
  BLE.addService(sensorService);
  
  // Valeurs initiales
  tempCharacteristic.writeValue(0.0);
  humCharacteristic.writeValue(0.0);
  luxCharacteristic.writeValue(0.0);
  
  BLE.advertise();
  Serial.println("BLE Périphérique actif: NanoSense-A102");
}

void loop() {
  BLEDevice central = BLE.central();
  
  if (central) {
    Serial.print("Connecté à central: ");
    Serial.println(central.address());
    
    while (central.connected()) {
      // Lecture capteurs
      float temperature = HTS.readTemperature();
      float humidity = HTS.readHumidity();
      float luminosity = readTSL2561(); // Fonction à implémenter
      
      // Mise à jour caractéristiques BLE
      tempCharacteristic.writeValue(temperature);
      humCharacteristic.writeValue(humidity);
      luxCharacteristic.writeValue(luminosity);
      
      Serial.print("Envoi BLE - T:");
      Serial.print(temperature);
      Serial.print(" H:");
      Serial.print(humidity);
      Serial.print(" L:");
      Serial.println(luminosity);
      
      delay(5000); // Mise à jour toutes les 5 secondes
    }
    
    Serial.println("Déconnecté du central");
  }
}
```

```cpp
// Arduino Nano IoT - Central BLE
#include <ArduinoBLE.h>

float bleTemp = 0.0;
float bleHum = 0.0;
float bleLux = 0.0;

void setup() {
  Serial.begin(115200);
  
  if (!BLE.begin()) {
    Serial.println("Erreur BLE!");
    while(1);
  }
  
  Serial.println("Recherche périphérique BLE...");
  BLE.scan();
}

void loop() {
  BLEDevice peripheral = BLE.available();
  
  if (peripheral) {
    if (peripheral.localName() == "NanoSense-A102") {
      BLE.stopScan();
      
      Serial.println("Périphérique trouvé!");
      connectAndRead(peripheral);
      
      // Relancer scan après déconnexion
      BLE.scan();
    }
  }
}

void connectAndRead(BLEDevice peripheral) {
  if (peripheral.connect()) {
    Serial.println("Connecté!");
    
    if (peripheral.discoverAttributes()) {
      BLECharacteristic tempChar = peripheral.characteristic("19B10001-E8F2-537E-4F6C-D104768A1214");
      BLECharacteristic humChar = peripheral.characteristic("19B10002-E8F2-537E-4F6C-D104768A1214");
      BLECharacteristic luxChar = peripheral.characteristic("19B10003-E8F2-537E-4F6C-D104768A1214");
      
      if (tempChar && humChar && luxChar) {
        // S'abonner aux notifications
        tempChar.subscribe();
        humChar.subscribe();
        luxChar.subscribe();
        
        while (peripheral.connected()) {
          if (tempChar.valueUpdated()) {
            tempChar.readValue(bleTemp);
          }
          if (humChar.valueUpdated()) {
            humChar.readValue(bleHum);
          }
          if (luxChar.valueUpdated()) {
            luxChar.readValue(bleLux);
          }
          
          Serial.print("BLE - T:");
          Serial.print(bleTemp);
          Serial.print(" H:");
          Serial.print(bleHum);
          Serial.print(" L:");
          Serial.println(bleLux);
          
          delay(100);
        }
      }
    }
    
    peripheral.disconnect();
    Serial.println("Déconnecté");
  }
}
```

---

### 3. WiFi - Communication Serveur

#### Configuration WiFi Arduino Nano IoT

```cpp
#include <WiFiNINA.h>
#include <ArduinoHttpClient.h>
#include <ArduinoJson.h>

// Credentials WiFi
const char* ssid = "VotreRouterSSID";
const char* password = "VotreMotDePasse";

// Serveur (IP fixe ou hostname)
const char* serverAddress = "192.168.1.100"; // IP de votre PC
const int serverPort = 80;

WiFiClient wifi;
HttpClient client = HttpClient(wifi, serverAddress, serverPort);

void setup() {
  Serial.begin(115200);
  
  // Connexion WiFi
  connectWiFi();
}

void connectWiFi() {
  Serial.print("Connexion à ");
  Serial.println(ssid);
  
  int status = WL_IDLE_STATUS;
  while (status != WL_CONNECTED) {
    status = WiFi.begin(ssid, password);
    delay(5000);
  }
  
  Serial.println("WiFi connecté!");
  Serial.print("IP: ");
  Serial.println(WiFi.localIP());
}

void sendMeasurements(int pieceId, float tempInt, float tempExt, float hum, float lux) {
  // Créer JSON
  StaticJsonDocument<256> doc;
  doc["piece_id"] = pieceId;
  doc["temperature_int"] = tempInt;
  doc["temperature_ext"] = tempExt;
  doc["humidite"] = hum;
  doc["luminosite"] = lux;
  
  String jsonBody;
  serializeJson(doc, jsonBody);
  
  Serial.println("Envoi mesures au serveur:");
  Serial.println(jsonBody);
  
  // POST Request
  client.beginRequest();
  client.post("/api/mesures/create.php");
  client.sendHeader("Content-Type", "application/json");
  client.sendHeader("Content-Length", jsonBody.length());
  client.beginBody();
  client.print(jsonBody);
  client.endRequest();
  
  // Lire réponse
  int statusCode = client.responseStatusCode();
  String response = client.responseBody();
  
  Serial.print("Status: ");
  Serial.println(statusCode);
  Serial.print("Response: ");
  Serial.println(response);
  
  client.stop();
}

void checkCommands(int pieceId) {
  String path = "/api/consignes/pending.php?piece_id=" + String(pieceId);
  
  client.get(path);
  
  int statusCode = client.responseStatusCode();
  String response = client.responseBody();
  
  if (statusCode == 200) {
    StaticJsonDocument<512> doc;
    DeserializationError error = deserializeJson(doc, response);
    
    if (!error) {
      JsonArray consignes = doc["consignes"];
      
      for (JsonObject consigne : consignes) {
        int id = consigne["id"];
        String type = consigne["type"];
        String action = consigne["action"];
        float valeur = consigne["valeur"];
        
        // Exécuter consigne
        executeCommand(type, action, valeur);
        
        // Marquer comme exécutée
        markCommandExecuted(id);
      }
    }
  }
  
  client.stop();
}

void executeCommand(String type, String action, float valeur) {
  Serial.print("Exécution: ");
  Serial.print(type);
  Serial.print(" - ");
  Serial.print(action);
  Serial.print(" - ");
  Serial.println(valeur);
  
  // Activer relais selon type
  if (type == "CHAUFFAGE") {
    // digitalWrite(RELAY_PIN_HEATING, ...);
  }
  // ... autres types
  
  // Afficher sur LCD
  String lcdMsg = type + " " + action;
  displayCommand(lcdMsg);
}

void loop() {
  // Vérifier connexion WiFi
  if (WiFi.status() != WL_CONNECTED) {
    connectWiFi();
  }
  
  // Collecter données
  float tempInt = bleTemp; // De BLE
  float tempExt = readMCP9808();
  float hum = bleHum;
  float lux = bleLux;
  
  // Envoyer au serveur
  sendMeasurements(1, tempInt, tempExt, hum, lux);
  
  // Vérifier consignes
  checkCommands(1);
  
  delay(10000); // Boucle toutes les 10 secondes
}
```

---

## 🗄️ Base de Données - Exemples de Requêtes

### Requêtes Courantes

```sql
-- 1. Insérer une nouvelle pièce
INSERT INTO pieces (nom, surface, etage, description)
VALUES ('Salle A102', 45.5, 1, 'Salle de cours informatique');

-- 2. Définir valeurs de référence
INSERT INTO valeurs_reference 
  (piece_id, temp_min, temp_max, hum_min, hum_max, lux_min, lux_max, tolerance)
VALUES (1, 18.0, 22.0, 40.0, 60.0, 200.0, 800.0, 1.0);

-- 3. Insérer mesure (fait par Arduino via PHP)
INSERT INTO mesures 
  (piece_id, temperature_int, temperature_ext, humidite, luminosite)
VALUES (1, 21.5, 15.2, 45.0, 320.5);

-- 4. Récupérer dernières mesures d'une pièce
SELECT * FROM mesures
WHERE piece_id = 1
ORDER BY timestamp DESC
LIMIT 1;

-- 5. Historique sur période
SELECT 
  DATE_FORMAT(timestamp, '%Y-%m-%d %H:%i') as temps,
  temperature_int,
  temperature_ext,
  humidite,
  luminosite
FROM mesures
WHERE piece_id = 1
  AND timestamp BETWEEN '2025-11-01' AND '2025-11-03'
ORDER BY timestamp ASC;

-- 6. Détecter dépassements
SELECT 
  m.*,
  v.temp_min, v.temp_max,
  CASE 
    WHEN m.temperature_int < v.temp_min - v.tolerance THEN 'TROP FROID'
    WHEN m.temperature_int > v.temp_max + v.tolerance THEN 'TROP CHAUD'
    ELSE 'OK'
  END as alerte_temperature
FROM mesures m
JOIN valeurs_reference v ON m.piece_id = v.piece_id
WHERE m.piece_id = 1
ORDER BY m.timestamp DESC
LIMIT 100;

-- 7. Moyennes par heure
SELECT 
  DATE_FORMAT(timestamp, '%Y-%m-%d %H:00') as heure,
  AVG(temperature_int) as temp_moy,
  AVG(humidite) as hum_moy,
  AVG(luminosite) as lux_moy,
  COUNT(*) as nb_mesures
FROM mesures
WHERE piece_id = 1
  AND timestamp >= DATE_SUB(NOW(), INTERVAL 24 HOUR)
GROUP BY DATE_FORMAT(timestamp, '%Y-%m-%d %H')
ORDER BY heure;
```

---

## 🌐 API PHP - Implémentation Complète

### Structure de Fichiers

```
server/
├── config/
│   └── database.php
├── api/
│   ├── mesures/
│   │   ├── create.php
│   │   ├── latest.php
│   │   └── history.php
│   ├── consignes/
│   │   ├── create.php
│   │   ├── pending.php
│   │   └── execute.php
│   └── pieces/
│       ├── list.php
│       └── create.php
└── web/
    ├── index.html
    ├── css/
    ├── js/
    └── assets/
```

### config/database.php

```php
<?php
header("Access-Control-Allow-Origin: *");
header("Content-Type: application/json; charset=UTF-8");
header("Access-Control-Allow-Methods: POST, GET, PUT, DELETE");
header("Access-Control-Max-Age: 3600");
header("Access-Control-Allow-Headers: Content-Type, Access-Control-Allow-Headers, Authorization, X-Requested-With");

class Database {
    private $host = "localhost";
    private $db_name = "smart_building";
    private $username = "root";
    private $password = "";
    public $conn;

    public function getConnection() {
        $this->conn = null;
        
        try {
            $this->conn = new PDO(
                "mysql:host=" . $this->host . ";dbname=" . $this->db_name,
                $this->username,
                $this->password
            );
            $this->conn->exec("set names utf8");
            $this->conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        } catch(PDOException $exception) {
            echo json_encode([
                "success" => false,
                "message" => "Erreur connexion: " . $exception->getMessage()
            ]);
        }
        
        return $this->conn;
    }
}
?>
```

### api/mesures/create.php

```php
<?php
include_once '../config/database.php';

$database = new Database();
$db = $database->getConnection();

// Récupérer données POST
$data = json_decode(file_get_contents("php://input"));

if (
    !empty($data->piece_id) &&
    isset($data->temperature_int) &&
    isset($data->temperature_ext) &&
    isset($data->humidite) &&
    isset($data->luminosite)
) {
    try {
        // Insérer mesure
        $query = "INSERT INTO mesures 
                  (piece_id, temperature_int, temperature_ext, humidite, luminosite) 
                  VALUES (:piece_id, :temp_int, :temp_ext, :hum, :lux)";
        
        $stmt = $db->prepare($query);
        $stmt->bindParam(":piece_id", $data->piece_id);
        $stmt->bindParam(":temp_int", $data->temperature_int);
        $stmt->bindParam(":temp_ext", $data->temperature_ext);
        $stmt->bindParam(":hum", $data->humidite);
        $stmt->bindParam(":lux", $data->luminosite);
        
        $stmt->execute();
        $mesure_id = $db->lastInsertId();
        
        // Vérifier dépassements
        $alertes = checkAlerts($db, $data->piece_id, $data);
        
        echo json_encode([
            "success" => true,
            "mesure_id" => $mesure_id,
            "alertes" => $alertes
        ]);
        
    } catch(PDOException $e) {
        echo json_encode([
            "success" => false,
            "message" => "Erreur: " . $e->getMessage()
        ]);
    }
} else {
    echo json_encode([
        "success" => false,
        "message" => "Données incomplètes"
    ]);
}

function checkAlerts($db, $piece_id, $data) {
    $query = "SELECT * FROM valeurs_reference WHERE piece_id = :piece_id";
    $stmt = $db->prepare($query);
    $stmt->bindParam(":piece_id", $piece_id);
    $stmt->execute();
    
    $ref = $stmt->fetch(PDO::FETCH_ASSOC);
    if (!$ref) return [];
    
    $alertes = [];
    
    // Température intérieure
    if ($data->temperature_int < $ref['temp_min'] - $ref['tolerance']) {
        $alertes[] = [
            "type" => "temperature_int",
            "valeur" => $data->temperature_int,
            "reference" => ["min" => $ref['temp_min'], "max" => $ref['temp_max']],
            "niveau" => "FROID"
        ];
    } elseif ($data->temperature_int > $ref['temp_max'] + $ref['tolerance']) {
        $alertes[] = [
            "type" => "temperature_int",
            "valeur" => $data->temperature_int,
            "reference" => ["min" => $ref['temp_min'], "max" => $ref['temp_max']],
            "niveau" => "CHAUD"
        ];
    }
    
    // Humidité
    if ($data->humidite < $ref['hum_min'] - $ref['tolerance']) {
        $alertes[] = [
            "type" => "humidite",
            "valeur" => $data->humidite,
            "reference" => ["min" => $ref['hum_min'], "max" => $ref['hum_max']],
            "niveau" => "SEC"
        ];
    } elseif ($data->humidite > $ref['hum_max'] + $ref['tolerance']) {
        $alertes[] = [
            "type" => "humidite",
            "valeur" => $data->humidite,
            "reference" => ["min" => $ref['hum_min'], "max" => $ref['hum_max']],
            "niveau" => "HUMIDE"
        ];
    }
    
    // Luminosité
    if ($data->luminosite < $ref['lux_min']) {
        $alertes[] = [
            "type" => "luminosite",
            "valeur" => $data->luminosite,
            "reference" => ["min" => $ref['lux_min'], "max" => $ref['lux_max']],
            "niveau" => "SOMBRE"
        ];
    } elseif ($data->luminosite > $ref['lux_max']) {
        $alertes[] = [
            "type" => "luminosite",
            "valeur" => $data->luminosite,
            "reference" => ["min" => $ref['lux_min'], "max" => $ref['lux_max']],
            "niveau" => "LUMINEUX"
        ];
    }
    
    return $alertes;
}
?>
```

### api/consignes/pending.php

```php
<?php
include_once '../config/database.php';

$database = new Database();
$db = $database->getConnection();

$piece_id = isset($_GET['piece_id']) ? $_GET['piece_id'] : null;

if ($piece_id) {
    $query = "SELECT * FROM consignes 
              WHERE piece_id = :piece_id 
              AND executee = 0
              ORDER BY timestamp ASC";
    
    $stmt = $db->prepare($query);
    $stmt->bindParam(":piece_id", $piece_id);
    $stmt->execute();
    
    $consignes = [];
    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
        $consignes[] = $row;
    }
    
    echo json_encode([
        "success" => true,
        "consignes" => $consignes
    ]);
} else {
    echo json_encode([
        "success" => false,
        "message" => "piece_id requis"
    ]);
}
?>
```

---

## 📱 Interface Web - Exemples

### Dashboard - JavaScript

```javascript
// js/dashboard.js

const API_BASE = 'http://localhost/api';
const PIECE_ID = 1;
const REFRESH_INTERVAL = 5000; // 5 secondes

// Éléments DOM
const tempIntElement = document.getElementById('temp-int');
const tempExtElement = document.getElementById('temp-ext');
const humElement = document.getElementById('humidite');
const luxElement = document.getElementById('luminosite');
const alertesContainer = document.getElementById('alertes');

// Récupérer dernières mesures
async function fetchLatestMeasures() {
    try {
        const response = await fetch(`${API_BASE}/mesures/latest.php?piece_id=${PIECE_ID}`);
        const data = await response.json();
        
        if (data.success) {
            updateDisplay(data.mesure);
            updateAlertes(data.alertes);
        }
    } catch (error) {
        console.error('Erreur fetch:', error);
    }
}

function updateDisplay(mesure) {
    tempIntElement.textContent = `${mesure.temperature_int}°C`;
    tempExtElement.textContent = `${mesure.temperature_ext}°C`;
    humElement.textContent = `${mesure.humidite}%`;
    luxElement.textContent = `${mesure.luminosite} lux`;
    
    // Animation changement
    [tempIntElement, tempExtElement, humElement, luxElement].forEach(el => {
        el.classList.add('updated');
        setTimeout(() => el.classList.remove('updated'), 500);
    });
}

function updateAlertes(alertes) {
    alertesContainer.innerHTML = '';
    
    if (alertes.length === 0) {
        alertesContainer.innerHTML = '<p class="text-success">✅ Toutes les valeurs sont normales</p>';
        return;
    }
    
    alertes.forEach(alerte => {
        const div = document.createElement('div');
        div.className = 'alert alert-warning';
        div.innerHTML = `
            ⚠️ ${alerte.type}: ${alerte.valeur} ${getUnit(alerte.type)}
            (Référence: ${alerte.reference.min}-${alerte.reference.max})
            - Niveau: ${alerte.niveau}
        `;
        alertesContainer.appendChild(div);
    });
}

function getUnit(type) {
    const units = {
        'temperature_int': '°C',
        'temperature_ext': '°C',
        'humidite': '%',
        'luminosite': 'lux'
    };
    return units[type] || '';
}

// Envoyer consigne
async function sendCommand(type, action, valeur = 0) {
    try {
        const response = await fetch(`${API_BASE}/consignes/create.php`, {
            method: 'POST',
            headers: {'Content-Type': 'application/json'},
            body: JSON.stringify({
                piece_id: PIECE_ID,
                type: type,
                action: action,
                valeur: valeur
            })
        });
        
        const data = await response.json();
        
        if (data.success) {
            alert(`Consigne envoyée: ${type} ${action}`);
        } else {
            alert('Erreur envoi consigne');
        }
    } catch (error) {
        console.error('Erreur:', error);
    }
}

// Boutons contrôle
document.getElementById('btn-chauffage-plus').addEventListener('click', () => {
    sendCommand('CHAUFFAGE', 'AUGMENTER', 1.0);
});

document.getElementById('btn-chauffage-moins').addEventListener('click', () => {
    sendCommand('CHAUFFAGE', 'DIMINUER', 1.0);
});

// Auto-refresh
setInterval(fetchLatestMeasures, REFRESH_INTERVAL);

// Premier chargement
fetchLatestMeasures();
```

---

## 🎓 Conseils Pratiques pour Démarrer

### Semaine 1: Setup Complet

**Jour 1-2: Installation**
1. Arduino IDE + bibliothèques
2. EasyPHP DevServer
3. Git repository

**Jour 3-4: Tests Matériel**
1. Brancher Arduino, téléverser code test
2. Scanner I²C pour détecter adresses
3. Test WiFi basique

**Jour 5-7: Base de Données**
1. Créer BD dans phpMyAdmin
2. Exécuter script SQL
3. Test INSERT/SELECT manuel

### Debugging

**I²C:**
```cpp
// Scanner I²C
void scanI2C() {
  Wire.begin();
  for (byte addr = 1; addr < 127
