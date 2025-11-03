# 🏢 Projet Smart Building - Système de Télémesure

> Projet de fin d'études - Programme Smart Building  
> École Polytechnique d'Orléans - 2025/2026

## 📋 Description

Système de télémesure pour bâtiment intelligent permettant la surveillance et le contrôle automatisé de l'environnement intérieur (température, humidité, luminosité) avec interface web interactive.

## 🎯 Objectifs du Projet

- **Mesure multi-capteurs** : Température (intérieure/extérieure), humidité, luminosité
- **Communication multi-protocoles** : I²C, Bluetooth BLE, WiFi
- **Stockage de données** : Base de données MySQL avec historique
- **Interface web** : Consultation temps réel et contrôle à distance
- **Système de contrôle** : Activation relais selon consignes utilisateur

## 🔧 Technologies Utilisées

### Hardware
- **Arduino Nano 33 BLE Sense** - Capteurs dans la pièce
- **Arduino Nano IoT** - Passerelle WiFi et contrôleur
- **Capteurs** :
  - MCP9808 (Température extérieure I²C)
  - TSL2561 (Luminosité I²C)
  - HTS221 intégré (Température/Humidité interne)
- **Actionneurs** :
  - Module relai 4 canaux
  - Écran LCD 16x2 I²C

### Software
- **Embedded** : Arduino (C/C++)
- **Backend** : PHP 7.4+, MySQL 8.0
- **Frontend** : HTML5, CSS3, JavaScript (ES6+)
- **Serveur** : Apache (EasyPHP DevServer)
- **Protocoles** : I²C, Bluetooth BLE, WiFi (HTTP/REST)

## 📁 Structure du Projet

```
projetsb/
├── docs/                          # Documentation complète
│   ├── 00-PLAN_THEORIQUE_COMPLET.md
│   ├── 01-DETAILS_TECHNIQUES.md
│   ├── 02-MAPPING_COURS_PROJET.md
│   └── cours/                     # Documents de cours
│
├── arduino/                       # Code Arduino (à venir)
│   ├── nano_sense/               # Code pour Nano Sense (BLE périphérique)
│   └── nano_iot/                 # Code pour Nano IoT (BLE central + WiFi)
│
├── server/                        # Backend PHP (à venir)
│   ├── config/                   # Configuration BD
│   ├── api/                      # API REST
│   │   ├── mesures/
│   │   ├── consignes/
│   │   └── pieces/
│   └── database/                 # Scripts SQL
│
├── web/                          # Frontend (à venir)
│   ├── index.html               # Dashboard
│   ├── css/                     # Styles
│   ├── js/                      # JavaScript
│   └── assets/                  # Images, icônes
│
└── README.md                     # Ce fichier
```

## 🚀 Architecture Système

```
┌─────────────────┐         ┌──────────────────┐
│  Arduino Nano   │   BLE   │  Arduino Nano    │
│  33 BLE Sense   │◄───────►│  IoT             │
│                 │         │                  │
│ • Temp interne  │         │ • Temp externe   │
│ • Humidité      │         │ • LCD            │
│ • Luminosité    │         │ • Relais         │
└─────────────────┘         └────────┬─────────┘
                                     │ WiFi
                            ┌────────▼─────────┐
                            │  Serveur Web     │
                            │  (PHP + MySQL)   │
                            └────────┬─────────┘
                                     │ HTTP
                            ┌────────▼─────────┐
                            │  Interface Web   │
                            │  (Dashboard)     │
                            └──────────────────┘
```

## 📊 Flux de Données

1. **Capteurs → Arduino Sense** : Lecture I²C (TSL2561) + capteurs intégrés
2. **Sense → IoT** : Transmission BLE (température, humidité, luminosité)
3. **IoT → Serveur** : HTTP POST JSON via WiFi
4. **Serveur → Base de Données** : Stockage MySQL
5. **Web → Serveur** : Consultation GET + Envoi consignes POST
6. **Serveur → IoT** : Polling consignes par Arduino
7. **IoT → Relais** : Activation selon consignes

## 🗄️ Base de Données

### Tables Principales
- `pieces` - Configuration des pièces monitorées
- `valeurs_reference` - Seuils de température, humidité, luminosité
- `mesures` - Historique des relevés
- `consignes` - Commandes de contrôle (chauffage, volets, etc.)

## 🌐 API REST

### Endpoints
- `POST /api/mesures/create.php` - Arduino → Serveur (nouvelles mesures)
- `GET /api/mesures/latest.php` - Dernières mesures
- `GET /api/mesures/history.php` - Historique
- `POST /api/consignes/create.php` - Web → Serveur (nouvelle consigne)
- `GET /api/consignes/pending.php` - Consignes non exécutées (Arduino polling)

## 📅 Planning

- **Phase 1 (S1-2)** : Fondations - Setup + Base de données
- **Phase 2 (S3-4)** : Tests composants individuels
- **Phase 3 (S5-6)** : Communications (I²C, BLE, WiFi)
- **Phase 4 (S7-8)** : Backend serveur
- **Phase 5 (S9)** : Intégration Arduino-Serveur
- **Phase 6 (S10-11)** : Interface web
- **Phase 7 (S12)** : Système de contrôle
- **Phase 8 (S13)** : Tests et optimisation
- **Phase 9 (S14-15)** : Documentation
- **Phase 10 (S16)** : Présentation et vidéo

**Deadline** : 20 février 2026

## 👥 Équipe

Projet réalisé en binôme dans le cadre du programme Smart Building 5A.

## 📚 Documentation

Toute la documentation détaillée se trouve dans le dossier `/docs`:
- Plan théorique complet
- Détails techniques et exemples de code
- Mapping avec cours suivis
- Guides d'implémentation

## 🔧 Installation (À Venir)

Instructions d'installation complètes seront ajoutées au fur et à mesure du développement.

### Prérequis
- Arduino IDE 2.x
- EasyPHP DevServer 17.x
- Git
- Routeur WiFi personnel

## 📝 Livrables Finaux

1. **Système fonctionnel** avec démonstration live
2. **Rapport détaillé** :
   - Procédures d'installation
   - Explication code (C, PHP, JavaScript)
   - Modélisation base de données
   - Justification ergonomie
3. **Vidéo de présentation** (~1 minute)
4. **Présentation orale** avec démonstration

## 📄 License

Projet académique - École Polytechnique d'Orléans

---

**Status** : 🚧 En développement - Phase théorique  
**Dernière mise à jour** : 3 novembre 2025
