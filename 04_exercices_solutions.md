# Exercices et Solutions - Préparation Examen

## Table des Matières
1. [Astronomie & Navigation](#astronomie--navigation)
2. [Systèmes Thermiques](#systèmes-thermiques)
3. [Systèmes Photovoltaïques](#systèmes-photovoltaïques)

---

## Astronomie & Navigation

### Exercice 1: Coordonnées Terrestres et Déclinaison

**Énoncé:**
Calculer les coordonnées terrestres et la déclinaison solaire au 1er décembre pour une position donnée.

**Données:**
- Position: 15° 3' 2'' Nord, 46° 3' Ouest de Greenwich
- Date: 1er décembre

**Solution:**

**1. Latitude φ:**
```
φ = 15° + (3/60)° = 15.05° (signe + car Nord)
```

**2. Longitude λ:**
```
λ = -(46 + (3/60)°) = -46.05° (signe - car Ouest)
```

**3. Rang du jour (1er décembre):**
```
m = 31 + 28 + 30 + 30 + 30 + 30 + 30 + 31 + 30 + 31 + 30
m = 335 jours
```

**4. Déclinaison solaire:**
```
δ = -23.45° × sin[(360/365)(364 + 335)]
δ ≈ -22.10°
```

**5. Durée du jour:**
```
Tj = 24/π × arccos(tan φ tan δ)/180
Tj = 11h 63 min
```

---

### Exercice 2: Calcul de l'Équation du Temps

**Énoncé:**
Calculer l'équation du temps pour le jour 355 de l'année au Sénégal.

**Données:**
- Jour: n = 355
- Longitude: -18.05° (pas de décalage horaire)

**Solution:**

**1. Calcul de B:**
```
B = 360 × (n/366) = 360 × (355/366) = 329.5°
```

**2. Équation du Temps (ET):**
```
ET (en min) = -0.0002 + 0.04289 cos(329.5) + 7.3509 sin(329.5) 
              - 3.2265 × cos(2 × 329.5) - 9.3912 sin(2 × 329.5) 
              - 0.0903 cos(3 × 329.5) - 0.3364 × sin(3 × 329.5)
            
ET ≈ 11.08 min ≈ 11 min
```

**3. Temps Solaire Moyen (TSn):**
```
TSn = TU + (λ/15) = 12h + ((-18.05)/15) = 10.93h = 10h 53 min
```

**4. Temps Solaire Vrai (TSV):**
```
TSV = ET + TSn = 11 min + 10h 53min = 11h 06 min
```

**5. Angle horaire ω:**
```
ω = 15°(TSV - 12) = 15 × (11.1 - 12) = -13.5°
```

---

### Exercice 3: Azimut Solaire

**Énoncé:**
Calculer l'azimut solaire pour les conditions données.

**Données:**
- TSVc = 15.1167h
- φ = latitude donnée
- δ = -22.10°

**Solution:**

**1. Angle horaire:**
```
ω = 15°(TSVc - 12) = 15°(15.1167 - 12) = 46.75°
```

**2. Altitude solaire:**
```
β = 45° (donné)
```

**3. Azimut (formule de Came):**
```
sin(Ψ) = cos(δ)sin(ω)/cos(β)
sin(Ψ) = cos(-22.10°)cos(75.4°)/cos(β)

Ψ ≈ ± 45.84°
```

**Note:** L'azimut est négatif le matin et positif le soir.

---

## Systèmes Thermiques

### Exercice 4: Capacité Thermique d'un Réservoir

**Énoncé:**
Calculer la capacité calorifique thermique d'un réservoir chauffé.

**Données:**
- Ta = 20°C (température ambiante)
- Ti = 45°C (température initiale)
- Φₘ = 70W (puissance de chauffage)
- Volume d'eau: 0.2 m³

**Solution:**

**1. Capacité calorifique thermique:**
```
Qth = hc × dT/dt
Qth = ρ × V × Cp = 9Vc + 4.18 × 10³ × 0.2 × 10³
Qth = 836 kJ/°C
```

**Réponse:** La capacité thermique est de **836 kJ/°C**.

---

### Exercice 5: Constante de Temps Thermique

**Énoncé:**
Calculer la constante de temps thermique du système.

**Données:**
- Rth = 0.64°C/W (résistance thermique)
- Cth = 836 kJ/°C (capacité thermique)

**Solution:**

**1. Constante de temps:**
```
τth = Rth × Cth
τth = 0.64 × 836 × 10³
τth = 535 × 10³ s = 149 h ≈ 3.5 min
```

**Réponse:** La constante de temps est de **3.5 minutes**.

---

### Exercice 6: Échange de Chaleur

**Énoncé:**
Calculer la température d'équilibre après mélange.

**Données:**
- Eau chaude: ha = 80 kg à 80°C
- Eau froide: hf = 120 kg à 20°C
- Capacité calorifique: Cp = 4.18 kJ/(kg·°C)

**Solution:**

**1. Bilan énergétique (∑Q = 0):**
```
ha × Cp × (Tf - Ta) + hf × Cp × (Tf - Tf,initial) = 0

Tf = (ha × Ta + hf × Tf,initial)/(ha + hf)
Tf = (80 × 80 + 120 × 20)/(80 + 120)
Tf = (6400 + 2400)/200
Tf = 44°C
```

**Réponse:** La température d'équilibre est de **44°C**.

---

### Exercice 7: Coût Énergétique

**Énoncé:**
Calculer le coût annuel de chauffage.

**Données:**
- Puissance: P = 2100W
- Utilisation: 8h/jour
- Tarif électricité: 0.13 €/kWh

**Solution:**

**1. Énergie journalière:**
```
E = P × t = 2100 × 8 = 16,800 Wh = 16.8 kWh
```

**2. Coût journalier:**
```
Coût/jour = 16.8 × 0.13 = 2.184 €
```

**3. Coût annuel:**
```
Coût/an = 2.184 × 365 = 797.16 € ≈ 800 €
```

**Réponse:** Le coût annuel est d'environ **800 €**.

---

## Systèmes Photovoltaïques

### Exercice 8: Dimensionnement de Modules

**Énoncé:**
Calculer le nombre maximum de modules en série pour un onduleur.

**Données:**
- Upmax onduleur = 600V
- Umpp module (+40°C) = 36.075V
- Coefficient de température: β = -0.105 V/K

**Solution:**

**1. Nombre de modules maximum:**
```
N(modules max) = Upmax(onduleur) / Umpp(+40°C)
N(modules max) = 600 / 36.075
N ≈ 16.63 → 16 modules maximum
```

**Vérification à -10°C:**
```
Umpp(-10°C) = Umpp(STC) + β × ΔT
Umpp(-10°C) ≈ 29.175V

Tension totale = 16 × 29.175 = 466.8V < 600V ✓
```

**Réponse:** On peut installer **16 modules en série maximum**.

---

### Exercice 9: Section de Câble

**Énoncé:**
Calculer la section de câble pour un string PV.

**Données:**
- ρ (cuivre) = 0.0176 Ω·mm²/m
- L = 25m
- Isc = 8.54A
- ΔV max = 3%
- Umpp = 37.414V

**Solution:**

**1. Section minimale:**
```
Scable = (ρ × L × Isc × 2) / (ΔV × Umpp)
Scable = (0.0176 × 25 × 8.54 × 2) / (0.03 × 37.414)
Scable ≈ 6.68 mm²
```

**2. Section commerciale:** On choisit **10mm²**

**3. Vérification chute de tension:**
```
ΔV = (0.0176 × 25 × 8.54 × 2) / (10 × 37.414)
ΔV ≈ 0.20% < 3% ✓
```

**Réponse:** Section de câble recommandée: **10mm²**.

---

### Exercice 10: Fusibles DC

**Énoncé:**
Choisir le calibre des fusibles DC.

**Données:**
- Isc = 8.4A (courant de court-circuit)
- Critères: 1.4 Isc < In < 2 Isc

**Solution:**

**1. Plage de courant:**
```
1.4 × 8.4 < In < 2 × 8.4
11.76A < In < 16.8A
```

**2. Fusibles disponibles:** 10A, 13A, 16A, 20A

**3. Choix:**
- 10A < 11.76A → ✗ Trop faible
- 13A → ✓ Dans la plage (11.76A < 13A < 16.8A)
- 16A → ✓ Dans la plage mais proche de la limite
- 20A > 16.8A → ✗ Trop élevé

**Réponse:** Choisir fusible de **13A** (recommandé) ou **16A**.

---

### Exercice 11: Courant Admissible

**Énoncé:**
Vérifier le courant admissible d'un câble.

**Données:**
- Isc = 8.4A
- Section câble = 4mm²
- Iza (tableau) = 45A pour 4mm²

**Solution:**

**1. Courant maximum en fonctionnement:**
```
Imax = 1.25 × Isc = 1.25 × 8.4 = 10.5A
```

**2. Vérification:**
```
Iza ≥ Imax
45A ≥ 10.5A ✓
```

**Réponse:** Le câble de 4mm² est **adapté** (45A >> 10.5A).

---

### Exercice 12: Production Annuelle

**Énoncé:**
Calculer la production annuelle d'une installation PV.

**Données:**
- Ep = 1310 kWh/m²/an (irradiation)
- Surface panneaux = 32 × 1.94 m² = 62.08 m²
- Rendement = 18%
- PR (Performance Ratio) = 0.75

**Solution:**

**1. Énergie théorique:**
```
E_th = Ep × Surface × Rendement
E_th = 1310 × 62.08 × 0.18
E_th = 14,627 kWh/an
```

**2. Énergie réelle:**
```
E_réelle = E_th × PR
E_réelle = 14,627 × 0.75
E_réelle ≈ 10,970 kWh/an
```

**Réponse:** Production annuelle estimée: **~11,000 kWh/an**.

---

### Exercice 13: Dimensionnement Batterie

**Énoncé:**
Calculer le nombre de batteries nécessaires.

**Données:**
- Besoin journalier: 25.61 kWh/jour
- Tension système: 48V
- Batterie: 200Ah, 12V
- Rendement: 0.85

**Solution:**

**1. Capacité batterie unitaire:**
```
Wh_batterie = 200Ah × 12V = 2400Wh
```

**2. Besoin corrigé:**
```
Besoin = 25.61 × 1000 / 0.85 = 30,129 Wh
```

**3. Nombre de batteries en parallèle (12V):**
```
Nb_parallèle = 30,129 / 2400 ≈ 12.55 → 13 batteries
```

**4. Pour système 48V:**
```
Nb_série = 48/12 = 4 batteries en série
Nb_total = 13 × 4 = 52 batteries
```

**Réponse:** Il faut **52 batteries** (13 strings de 4 batteries).

---

## Conseils pour l'Examen

### Stratégie de Résolution

1. **Lire attentivement l'énoncé**
   - Identifier les données
   - Repérer ce qui est demandé
   - Noter les unités

2. **Vérifier les unités**
   - Convertir si nécessaire
   - Cohérence des résultats

3. **Schématiser si possible**
   - Circuits électriques
   - Trajectoires solaires
   - Bilans énergétiques

4. **Vérifications**
   - Ordre de grandeur
   - Cohérence physique
   - Respect des contraintes

### Points de Vigilance

- ⚠️ **Signes des coordonnées** (Nord/Sud, Est/Ouest)
- ⚠️ **Conversions d'unités** (°, radians, kWh, Wh)
- ⚠️ **Coefficients de température** (négatifs pour tension)
- ⚠️ **Facteurs de sécurité** (1.25 pour courants)
- ⚠️ **Limites de température** (-10°C, +70°C pour PV)

### Formules à Avoir en Tête

**Navigation:**
- ω = 15°(TSV - 12)
- TSV = TSN + ET
- Tj = 24/π × arccos(tan φ tan δ)/180

**Thermique:**
- τth = Rth × Cth
- Q = m × Cp × ΔT
- ∑Q = 0 (conservation)

**Photovoltaïque:**
- Scable = (ρ × L × I × 2) / (ΔV × U)
- Iza ≥ 1.25 × Isc
- 1.4 Isc < In < 2 Isc

---

Bon courage pour vos révisions ! 🎓
