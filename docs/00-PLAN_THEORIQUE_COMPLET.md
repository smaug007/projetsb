# Plan Théorique Complet - Projet Smart Building

**Date de création**: 3 novembre 2025  
**Deadline**: 20 février 2026 (≈ 16 semaines)  
**Équipe**: 2 personnes  
**Effort disponible**: 20-50h/semaine (320-800h total)

---

## 📊 Vue d'Ensemble du Projet

### Objectif Principal
Créer un système de télémesure pour bâtiment intelligent permettant:
- Mesure de température (intérieure/extérieure), humidité, luminosité
- Stockage des données dans une base de données
- Visualisation web en temps réel et historique
- Envoi de consignes de contrôle (chauffage, volets, etc.)

### Architecture Globale

```
┌─────────────────────────────────────────────────────────────────┐
│                         SALLE MONITOREÉ                          │
│                                                                   │
│  ┌──────────────────┐         ┌────────────────────┐            │
│  │ Arduino Nano     │  BLE    │  Arduino Nano IoT  │            │
│  │ 33 BLE Sense     │◄───────►│                    │            │
│  │                  │         │                    │            │
│  │ - Temp interne   │         │ ┌────────────────┐ │            │
│  │ - Humidité       │    I²C  │ │ MCP9808        │ │            │
│  │ - Luminosité     │◄────────┤ │ (Temp externe) │ │            │
│  │   (TSL2561)      │         │ └────────────────┘ │            │
│  └──────────────────┘         │                    │            │
│                                │ ┌────────────────┐ │            │
│                           I²C  │ │ Écran LCD      │ │            │
│                          ◄─────┤ │ 2 lignes       │ │            │
│                                │ └────────────────┘ │            │
│                                │                    │            │
│                                │ ┌────────────────┐ │            │
│                                │ │ Carte Relai    │ │            │
│                                │ │                │ │            │
│                                │ └────────────────┘ │            │
│                                └────────────────────┘            │
│                                       │ WiFi                     │
└───────────────────────────────────────┼──────────────────────────┘
                                        │
                        ┌───────────────▼───────────────┐
                        │     Routeur WiFi Personnel    │
                        └───────────────┬───────────────┘
                                        │
                        ┌───────────────▼───────────────┐
                        │  Ordinateur Portable Serveur  │
                        │                                │
                        │  ┌──────────────────────────┐ │
                        │  │  EasyPHP DevServer       │ │
                        │  │  - Apache (serveur web)  │ │
                        │  │  - MySQL (BD)            │ │
                        │  │  - PHP 7.x/8.x           │ │
                        │  └──────────────────────────┘ │
                        │                                │
                        │  ┌──────────────────────────┐ │
                        │  │  Base de Données MySQL   │ │
                        │  │  - pieces                │ │
                        │  │  - valeurs_reference     │ │
                        │  │  - mesures               │ │
                        │  │  - consignes             │ │
                        │  └──────────────────────────┘ │
                        │                                │
                        │  ┌──────────────────────────┐ │
                        │  │  API REST PHP            │ │
                        │  │  - POST /mesures         │ │
                        │  │  - GET /mesures          │ │
                        │  │  - POST /consignes       │ │
                        │  │  - GET /consignes        │ │
                        │  └──────────────────────────┘ │
                        └────────────────────────────────┘
                                        │
                        ┌───────────────▼───────────────┐
                        │  Interface Web (Navigateur)   │
                        │  - HTML5/CSS3/JavaScript      │
                        │  - Responsive Design          │
                        │  - PC/Tablette/Smartphone     │
                        │                                │
                        │  Pages:                        │
                        │  - Dashboard temps réel        │
                        │  - Historique graphique        │
                        │  - Configuration pièce         │
                        │  - Valeurs de référence        │
                        │  - Panneau de contrôle         │
                        └────────────────────────────────┘
```

---

## 🔧 Composants et Technologies

### 1. Hardware

#### Arduino Nano 33 BLE Sense
- **Rôle**: Capteur principal dans la pièce
- **Capteurs intégrés**:
  - Température (HTS221)
  - Humidité (HTS221)
- **Capteur externe I²C**:
  - TSL2561: Luminosité
- **Communication**: Bluetooth BLE (vers Nano IoT)
- **Alimentation**: USB ou batterie + régulateur 5V

#### Arduino Nano IoT
- **Rôle**: Passerelle WiFi et contrôleur
- **Capteurs I²C connectés**:
  - MCP9808: Température extérieure
  - Écran LCD 16x2 (I2C)
- **Actuateurs**:
  - Carte relai (4 relais minimum)
- **Communication**:
  - Bluetooth BLE (réception depuis Nano Sense)
  - WiFi (envoi/réception serveur)
  - I²C (capteurs et LCD)

#### Capteurs
| Composant | Interface | Fonction | Adresse I²C |
|-----------|-----------|----------|-------------|
| MCP9808 | I²C | Température extérieure (-40°C à +125°C, ±0.25°C) | 0x18 |
| TSL2561 | I²C | Luminosité (0.1 - 40,000 lux) | 0x39 |
| LCD 16x2 | I²C | Affichage état/consignes | 0x27 ou 0x3F |
| HTS221 | Intégré Nano Sense | Temp/Humidité interne | N/A |

#### Carte Relai
- 4 canaux minimum (chauffage, ventilation, volets, lumières)
- Contrôle 220V AC via signaux 5V DC
- Connexion GPIO Arduino Nano IoT

---

### 2. Protocoles de Communication

#### I²C (Inter-Integrated Circuit)
- **Usage**:
  - Nano IoT ↔ MCP9808
  - Nano IoT ↔ LCD
  - Nano Sense ↔ TSL2561
- **Caractéristiques**:
  - Bus série synchrone 2 fils (SDA, SCL)
  - Vitesse: 100 kHz (standard) ou 400 kHz (fast)
  - Adressage: 7 bits
- **Considérations**:
  - Pull-up resistors 4.7kΩ sur SDA/SCL
  - Vérifier conflits d'adresses
  - Distance max: ~1m

#### Bluetooth Low Energy (BLE)
- **Usage**: Nano Sense → Nano IoT
- **Données transmises**:
  - Température intérieure
  - Humidité
  - Luminosité
- **Caractéristiques**:
  - Portée: 10-50m (selon obstacles)
  - Consommation faible
  - Mode central (IoT) / périphérique (Sense)
- **Implémentation**:
  - Service BLE personnalisé
  - Caractéristiques pour chaque mesure
  - Format: 4 octets (float) par valeur

#### WiFi
- **Usage**: Nano IoT ↔ Serveur
- **Protocole applicatif**: HTTP/HTTPS
- **Format données**: JSON
- **Requêtes**:
  - POST: Envoi mesures toutes les X secondes
  - GET: Réception consignes (polling ou webhook)
- **Sécurité**:
  - WPA2 sur routeur
  - Optionnel: HTTPS, authentification API

---

### 3. Backend (Serveur)

#### EasyPHP DevServer
- **Composants**:
  - Apache 2.4.x: Serveur HTTP
  - PHP 7.4/8.x: Logique backend
  - MySQL 8.x: Base de données
  - phpMyAdmin: Interface admin BD

#### Base de Données MySQL

**Schéma conceptuel:**

```sql
-- Table: pieces
CREATE TABLE pieces (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    surface DECIMAL(6,2),
    etage INT,
    description TEXT,
    date_creation TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Table: valeurs_reference
CREATE TABLE valeurs_reference (
    id INT AUTO_INCREMENT PRIMARY KEY,
    piece_id INT NOT NULL,
    temp_min DECIMAL(4,1),
    temp_max DECIMAL(4,1),
    hum_min DECIMAL(4,1),
    hum_max DECIMAL(4,1),
    lux_min DECIMAL(7,1),
    lux_max DECIMAL(7,1),
    tolerance DECIMAL(3,1) DEFAULT 1.0,
    date_modification TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (piece_id) REFERENCES pieces(id) ON DELETE CASCADE
);

-- Table: mesures
CREATE TABLE mesures (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    piece_id INT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    temperature_int DECIMAL(4,1),
    temperature_ext DECIMAL(4,1),
    humidite DECIMAL(4,1),
    luminosite DECIMAL(7,1),
    INDEX idx_piece_timestamp (piece_id, timestamp),
    FOREIGN KEY (piece_id) REFERENCES pieces(id) ON DELETE CASCADE
);

-- Table: consignes
CREATE TABLE consignes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    piece_id INT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    type VARCHAR(50) NOT NULL, -- 'CHAUFFAGE', 'VENTILATION', 'VOLET', 'LUMIERE'
    action VARCHAR(50) NOT NULL, -- 'ON', 'OFF', 'AUGMENTER', 'DIMINUER'
    valeur DECIMAL(5,2),
    executee BOOLEAN DEFAULT FALSE,
    date_execution TIMESTAMP NULL,
    FOREIGN KEY (piece_id) REFERENCES pieces(id) ON DELETE CASCADE
);

-- Table: logs_systeme (optionnel, pour debug)
CREATE TABLE logs_systeme (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    niveau VARCHAR(20), -- 'INFO', 'WARNING', 'ERROR'
    source VARCHAR(100),
    message TEXT
);
```

#### API REST PHP

**Structure des endpoints:**

```
/api/
  ├── pieces/
  │   ├── index.php          [GET] Liste toutes les pièces
  │   ├── create.php         [POST] Créer nouvelle pièce
  │   └── {id}/
  │       ├── get.php        [GET] Détails d'une pièce
  │       └── update.php     [PUT] Modifier pièce
  │
  ├── mesures/
  │   ├── create.php         [POST] Arduino → Serveur (nouvelles mesures)
  │   ├── latest.php         [GET] Dernières mesures d'une pièce
  │   └── history.php        [GET] Historique (filtres: date début/fin)
  │
  ├── references/
  │   ├── get.php            [GET] Valeurs de référence d'une pièce
  │   └── update.php         [POST] Modifier valeurs de référence
  │
  └── consignes/
      ├── create.php         [POST] Web → Serveur (nouvelle consigne)
      ├── pending.php        [GET] Consignes non exécutées (Arduino polling)
      └── execute.php        [POST] Marquer consigne comme exécutée
```

**Format JSON des requêtes/réponses:**

```json
// POST /api/mesures/create.php
{
  "piece_id": 1,
  "temperature_int": 22.5,
  "temperature_ext": 15.2,
  "humidite": 45.0,
  "luminosite": 320.5
}

// Réponse
{
  "success": true,
  "mesure_id": 12345,
  "alertes": [
    {
      "type": "temperature_int",
      "valeur": 22.5,
      "reference": {"min": 18, "max": 22},
      "depassement": 0.5
    }
  ]
}

// POST /api/consignes/create.php
{
  "piece_id": 1,
  "type": "CHAUFFAGE",
  "action": "AUGMENTER",
  "valeur": 1.0
}

// GET /api/consignes/pending.php?piece_id=1
{
  "consignes": [
    {
      "id": 42,
      "type": "CHAUFFAGE",
      "action": "AUGMENTER",
      "valeur": 1.0,
      "timestamp": "2025-11-03T16:30:00Z"
    }
  ]
}
```

---

### 4. Frontend (Interface Web)

#### Technologies
- **HTML5**: Structure sémantique
- **CSS3**: Styles, animations, responsive
- **JavaScript (ES6+)**: Logique client
- **Bibliothèques suggérées**:
  - Chart.js: Graphiques historiques
  - Fetch API: Requêtes AJAX
  - Bootstrap 5 ou Tailwind CSS: Framework CSS responsive

#### Pages et Fonctionnalités

**1. Dashboard (index.html)**
```
┌────────────────────────────────────────────┐
│ 🏠 Smart Building - Salle A102             │
├────────────────────────────────────────────┤
│                                            │
│  📊 Mesures en temps réel                 │
│  ┌─────────────┬─────────────┬──────────┐ │
│  │ 🌡️ Temp Int │ 💧 Humidité │ 💡 Lux   │ │
│  │   22.5°C    │    45%      │   320    │ │
│  │   ↑ +0.3°C  │    ↓ -2%    │   ↑ +15  │ │
│  └─────────────┴─────────────┴──────────┘ │
│                                            │
│  🌡️ Temp Ext: 15.2°C                      │
│                                            │
│  ⚠️ Alertes:                               │
│  - Température intérieure > référence     │
│                                            │
│  🎛️ Actions rapides:                      │
│  [🔥 Chauffage -1°C] [🪟 Fermer volets]   │
│                                            │
│  📈 Graphique 24h (mini)                  │
│  [Voir historique complet →]              │
└────────────────────────────────────────────┘
```

**2. Historique (historique.html)**
- Graphiques Chart.js (ligne, barres)
- Filtres: période (24h, 7j, 30j, personnalisé)
- Export CSV/Excel
- Mise en évidence dépassements (couleur rouge)

**3. Configuration Pièce (config-piece.html)**
- Formulaire: nom, surface, étage, description
- CRUD pièces multiples

**4. Valeurs de Référence (references.html)**
```
┌────────────────────────────────────────────┐
│ Valeurs de référence - Salle A102          │
├────────────────────────────────────────────┤
│                                            │
│  Température intérieure:                   │
│  Min: [18] °C    Max: [22] °C             │
│                                            │
│  Humidité:                                 │
│  Min: [40] %     Max: [60] %              │
│                                            │
│  Luminosité:                               │
│  Min: [200] lux  Max: [800] lux           │
│                                            │
│  Tolérance: [± 1.0] unités                │
│                                            │
│  [Enregistrer]                             │
└────────────────────────────────────────────┘
```

**5. Panneau de Contrôle (controle.html)**
- Boutons/sliders pour consignes
- Types: Chauffage, Ventilation, Volets, Lumières
- Confirmation avant envoi
- Historique consignes envoyées

#### Responsive Design
```css
/* Mobile First */
@media (max-width: 768px) {
  /* 1 colonne, boutons pleine largeur */
}

@media (min-width: 769px) and (max-width: 1024px) {
  /* Tablette: 2 colonnes */
}

@media (min-width: 1025px) {
  /* Desktop: 3-4 colonnes, sidebar */
}
```

---

## 🔄 Flux de Données Complets

### 1. Flux de Mesures (Arduino → Serveur → Web)

```
[Nano Sense]
    │ Lit capteurs internes (T°C int, humidité)
    │ Lit TSL2561 via I²C (luminosité)
    │ Format BLE: {temp_int: 22.5, hum: 45, lux: 320}
    │
    ▼ Bluetooth BLE
    │
[Nano IoT]
    │ Reçoit données BLE
    │ Lit MCP9808 via I²C (T°C ext)
    │ Agrège toutes les données
    │ Format JSON: {piece_id: 1, temp_int: 22.5, temp_ext: 15.2, ...}
    │
    ▼ HTTP POST via WiFi
    │
[Serveur PHP]
    │ Reçoit POST /api/mesures/create.php
    │ Valide données
    │ INSERT INTO mesures
    │ Vérifie dépassements vs valeurs_reference
    │ Retourne JSON avec alertes
    │
    ▼ Stockage BD
    │
[MySQL]
    │ Données persistées
    │
    ▼ Requête GET depuis Web
    │
[Interface Web]
    │ Fetch /api/mesures/latest.php
    │ Affiche en temps réel
    │ Mise à jour auto toutes les 5-10s (AJAX polling)
```

### 2. Flux de Consignes (Web → Serveur → Arduino → Relai)

```
[Interface Web]
    │ Utilisateur clique "Chauffage +1°C"
    │ POST /api/consignes/create.php
    │
    ▼ HTTP POST
    │
[Serveur PHP]
    │ Valide consigne
    │ INSERT INTO consignes (executee=FALSE)
    │ Retourne success
    │
    ▼ Stockage BD
    │
[MySQL]
    │ Consigne en attente
    │
    ▼ Arduino polling (GET toutes les 5-10s)
    │
[Nano IoT]
    │ GET /api/consignes/pending.php?piece_id=1
    │ Reçoit consigne non exécutée
    │ Parse JSON
    │ Active relai correspondant
    │ Affiche sur LCD: "Chauffage +1°C"
    │ POST /api/consignes/execute.php?id=42
    │
    ▼ Activation physique
    │
[Carte Relai]
    │ Relai X activé → Appareil contrôlé
```

---

## 📅 Planning Détaillé (16 semaines)

### Répartition du temps (2 personnes × 10-25h/semaine)

**Phase 1: Fondations (Semaines 1-2)**
- ✅ Setup environnements (Arduino IDE, EasyPHP, VS Code)
- ✅ Installation bibliothèques Arduino
- ✅ Tests connexion matériel
- ✅ Modélisation BD et création schéma SQL
- ✅ Architecture système documentée
- **Effort**: 30-40h

**Phase 2: Composants Individuels (Semaines 3-4)**
- 🔧 Code Arduino MCP9808 (I²C)
- 🔧 Code Arduino TSL2561 (I²C)
- 🔧 Code Arduino LCD (I²C)
- 🔧 Code Arduino capteurs Nano Sense intégrés
- 🔧 Tests unitaires chaque composant
- **Effort**: 40-50h

**Phase 3: Communications (Semaines 5-6)**
- 📡 Bluetooth BLE: Nano Sense → Nano IoT
- 📡 WiFi: Nano IoT → Serveur (test avec serveur mock)
- 📡 Protocole messages (format JSON)
- 📡 Gestion erreurs et reconnexion
- **Effort**: 50-60h

**Phase 4: Backend Serveur (Semaines 7-8)**
- 🖥️ Configuration EasyPHP
- 🖥️ Création base de données
- 🖥️ API REST PHP (tous endpoints)
- 🖥️ Tests Postman/Insomnia
- 🖥️ Logging et gestion erreurs
- **Effort**: 50-60h

**Phase 5: Intégration Arduino-Serveur (Semaine 9)**
- 🔗 Pipeline complet: Capteurs → BLE → WiFi → BD
- 🔗 Tests end-to-end mesures
- 🔗 Optimisation fréquence envoi
- 🔗 Gestion des cas d'erreur
- **Effort**: 30-40h

**Phase 6: Interface Web (Semaines 10-11)**
- 🎨 HTML/CSS pages (dashboard, historique, config, contrôle)
- 🎨 JavaScript fetch API
- 🎨 Chart.js graphiques
- 🎨 Responsive design (mobile/tablette/desktop)
- 🎨 UX/UI professionnel
- **Effort**: 60-80h

**Phase 7: Système de Contrôle (Semaine 12)**
- 🎛️ Carte relai + code Arduino
- 🎛️ Affichage LCD (statut + consignes)
- 🎛️ Web → Serveur → Arduino → Relai
- 🎛️ Tests consignes complètes
- **Effort**: 30-40h

**Phase 8: Tests et Optimisation (Semaine 13)**
- ✅ Tests d'intégration complets
- ✅ Tests charge (plusieurs mesures/minute)
- ✅ Tests déconnexion/reconnexion
- ✅ Optimisation performances
- ✅ Corrections bugs
- **Effort**: 40-50h

**Phase 9: Documentation (Semaines 14-15)**
- 📝 Rapport détaillé:
  - Procédures installation
  - Explications code (C, Python si utilisé, PHP, JS)
  - Modélisation BD
  - Justifications ergonomie
- 📝 Schémas et diagrammes
- 📝 Manuel utilisateur
- **Effort**: 50-60h

**Phase 10: Présentation et Vidéo (Semaine 16)**
- 🎬 Préparation présentation orale
- 🎬 Création vidéo 1 minute (scénario, tournage, montage)
- 🎬 Démonstration live système
- 🎬 Répétitions
- **Effort**: 20-30h

**TOTAL ESTIMÉ**: 450-600h (bien dans la fourchette 320-800h)

---

## ⚠️ Risques et Mitigations

### Risques Techniques

| Risque | Probabilité | Impact | Mitigation |
|--------|-------------|--------|------------|
| Conflits adresse I²C | Moyenne | Moyen | Scanner bus I²C, modifier adresses si possible |
| Perte connexion BLE | Haute | Élevé | Reconnexion auto, buffer local sur Nano Sense |
| WiFi instable | Moyenne | Élevé | Reconnexion auto, queue de messages, retry logic |
| Consommation Nano Sense | Moyenne | Moyen | Alimentation stable, optimiser fréquence BLE |
| Performance BD (beaucoup de mesures) | Faible | Moyen | Index sur timestamp, archivage ancien data |

### Risques Projet

| Risque | Probabilité | Impact | Mitigation |
|--------|-------------|--------|------------|
| Sous-estimation temps interface web | Moyenne | Moyen | Commencer tôt, utiliser frameworks CSS |
| Complexité Bluetooth BLE | Moyenne | Élevé | Tutoriels, exemples Arduino, tests précoces |
| Problèmes matériel (composant défectueux) | Faible | Élevé | Commander pièces de rechange, tests rapides |
| Scope creep (fonctionnalités extra) | Haute | Moyen | Définir MVP, prioriser, timeboxing strict |

---

## 🎯 Critères de Succès

### Fonctionnels (Must-Have)
- ✅ Mesure T°C int/ext, humidité, luminosité
- ✅ Communication I²C, BLE, WiFi fonctionnelle
- ✅ Stockage BD MySQL
- ✅ Interface web consultation mesures + historique
- ✅ Définition valeurs de référence
- ✅ Alertes dépassements visuels
- ✅ Envoi consignes web → Arduino
- ✅ Activation carte relai
- ✅ Affichage LCD

### Non-Fonctionnels
- ✅ Interface "professionnelle" (design soigné)
- ✅ Responsive (PC/tablette/smartphone)
- ✅ Code commenté et structuré
- ✅ Gestion erreurs robuste
- ✅ Documentation complète

### Livrables
- ✅ Système fonctionnel démontrable
- ✅ Rapport détaillé
- ✅ Vidéo 1 minute
- ✅ Présentation orale + démo live

---

## 💡 Recommandations Stratégiques

### 1. Répartition des Tâches (2 personnes)

**Personne A - Spécialisation Hardware/Embedded**
- Arduino (Nano Sense + Nano IoT)
- Capteurs I²C
- Bluetooth BLE
- Carte relai
- Écran LCD

**Personne B - Spécialisation Software/Web**
- Serveur PHP
- Base de données MySQL
- Interface web (HTML/CSS/JS)
- API REST
- Graphiques Chart.js

**Coordination**:
- Définir protocoles données ensemble (JSON format)
- Tests d'intégration ensemble
- Documentation partagée

### 2. Approche Itérative (Agile)

**Sprint 1 (S1-2)**: MVP Architecture + BD
- Créer BD, API basique, test Arduino simple

**Sprint 2 (S3-4)**: Capteurs fonctionnels
- Tous capteurs lisent données correctement

**Sprint 3 (S5-6)**: Communications établies
- BLE et WiFi connectés

**Sprint 4 (S7-8)**: Backend complet
- Toute API REST opérationnelle

**Sprint 5 (S9)**: Intégration 1
- Arduino → Serveur → BD

**Sprint 6 (S10-11)**: Frontend
- Interface web fonctionnelle

**Sprint 7 (S12)**: Contrôle bidirectionnel
- Web → Arduino → Relai

**Sprint 8 (S13)**: Polish & Tests
- Stabilisation

**Sprint 9-10 (S14-16)**: Documentation & Présentation

### 3. Tests Incrémentaux

**Éviter l'effet "Big Bang"** (tout intégrer à la fin)

- Tester chaque composant individuellement
- Intégrer progressivement (I²C → BLE → WiFi)
- Créer tests automatisés quand possible
- Logger tout (Serial Monitor, console.log, logs PHP)

### 4. Outils de Développement

**Gestion de version**: Git + GitHub/GitLab
- Branches: `main`, `dev`, `feature/xxx`
- Commits fréquents avec messages clairs

**Documentation**: Markdown
- README.md avec setup instructions
- ARCHITECTURE.md
- API.md

**Communication équipe**: Discord/Slack + réunions hebdo

**Tests API**:
