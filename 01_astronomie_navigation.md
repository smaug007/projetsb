# Astronomie & Navigation Céleste - Résumé d'Examen

## 1. Systèmes de Temps et Formules

### Équations de Temps de Base
- **TSV (Temps Solaire Vrai)**: TSV = TSN + ET
- **ET (Équation du Temps)**: Correction entre le temps solaire moyen et le temps solaire vrai
- **TSN (Temps Solaire Moyen)**: Temps solaire moyen

### Relations de Temps
```
TSV = TSN + ET
TSN = TSV - ET
ET = TSV - TSN
```

---

## 2. Systèmes de Coordonnées

### Coordonnées Terrestres
- **Latitude (φ)**: Position Nord-Sud (+ pour Nord, - pour Sud)
  - Exemple: φ = 48° + (48/60)° = 48.8° (signe + car Nord)
  
- **Longitude (λ)**: Position Est-Ouest (+ pour Est, - pour Ouest)
  - Exemple: λ = +(λe + (45/60)°) = +λe,15° (signe + pour Est)

### Calcul du Temps Géographique
- **Déclinaison solaire**: Varie tout au long de l'année
  - Plage: -23° à +23°
  - Peut être déterminée à l'aide de la formule de Casper avec une bonne précision

### Formules de Navigation et Identification
- Formule de navigation au point Q: **UPLY(Q) = UPLY, PLPL/Y ± ORSTA/L**
- Identification: **IL = P - O = P7** (formule de référence)
- Position temporelle: **Ip > I** ou rapport de temps
- Calculs spécifiques d'orientation et de navigation céleste
- Utilisation des rapports angulaires pour déterminer la position

---

## 3. Calculs de Position Solaire

### Angle Horaire (ω)
```
ω = (360°/24) × (TSV - 12) = 15°(TSV - 12) = 15°(15.1167 - 12)
ω = 46.7505°
```

### Temps Spéciaux
- **Greenwich**: À 4h 45' 14" UT le 1er octobre
- Les calculs impliquent la conversion entre différents fuseaux horaires et références

### Formules Additionnelles pour l'Angle Horaire
- **ULPY(Q) ≡ UPLY₁ - PLPV/UPLYL ± ORSTA/L**
- **Orélation**: Ulpy = 0.5S/S (conditions spéciales)
- **ω = arccos(-tan ω tan(-0.02)** (formule alternative)
- **HDPA (T) = HDPL × τPD⁴¹⁴ = 8 min 53s**
- Utilisation des variations temporelles pour les calculs de position

---

## 4. Azimut et Direction

### Calcul de l'Azimut
L'angle d'azimut est exprimé en degrés à partir d'une direction de référence.

Composantes clés de la formule:
- Implique des fonctions trigonométriques (sin, cos)
- Dépend de la latitude, de l'angle horaire et de la déclinaison solaire
- Tenir compte des projections sur différents plans

### Méthode du Méridien Solaire
```
sin(Ψ) = cos(φ)cos(ω)/cos(β)

tan(Ψ) = cos(φ)cos(ω)/(cos(φ)sin(ω))
```

Où:
- Ψ = angle d'azimut
- φ = latitude
- ω = angle horaire
- β = paramètre d'angle

### L'azimut local - Formule de Came
```
sin(Ψ) = cos(δ)sin(ω)/cos(β)

au lever et au coucher cos β = 0:
soit    sin(Ψ) = 1 ⟹ cos β cos ω = cos δ (cos ω)
```

**L'angle horaire mesuré à partir du midi:**
```
ω = (360°/24)(TSVc - 12) = 15°(TSVc - 12) ⟹ 15°(15.1167 - 2) = δ
β = 45°

Le PSVc on l'azimut est négatif le matin et positif le soir
donc sin(Ψ) = cos(δ)cos(ω)/cos(-22,10)cos(75.4)
Ψ = ± 45.84°
```

---

## 5. Diagrammes Clés et Relations Géométriques

### Heures de Lever/Coucher
- **THL** (Temps Heure Lever): Heure du lever du soleil
- **THC** (Temps Heure Coucher): Heure du coucher du soleil

Méthode de calcul:
```
THL = TSN + (-ωL+C)/15 → -ET = [formule]
THC = TSNC + ωL+C/15 → -ET = [formule]
```

### Diagramme de la Trajectoire Solaire
- Montre la relation entre:
  - Ligne d'horizon
  - Équateur
  - Trajectoire solaire
  - Angles de référence (φ, δ, β, ω)

### Considérations de Symétrie
- **Lever et coucher sont placés symétriquement par rapport à midi**

---

## 6. Calcul de la Durée du Jour

### Durée du jour
```
Tj = 24/2 - arccos(tan ω tan φ)/180

Tj = 10.18 hr = 10h 18 min
```

**Formule alternative:**
```
Tj = 24/π × arccos(tan φ tan λ)/180

Tj = 11h 63 min
```

---

## 7. Applications Pratiques

### Différences de Temps Local
- Méridien solaire: Différent de l'heure locale
- Cette différence est appelée "équation du temps différentielle par rapport au temps GPS"
- Varie tout au long du jour et de l'année

### Calculs d'Octobre
**Spécificités du 19 octobre:**
- La France a 2 heures d'avance sur le temps de référence
- Le temps administratif local est avancé de 2 heures par rapport à la référence (Greenwich/méridien de référence)
- Calculs de décalage de temps géographique requis

### Relations d'Angles
```
S = π/2 - φ
x + 5 = π
donc:
x + 5 - S = x + 5 ⟹ S - δ = 5
S - δ = π/2 - φ → δ = π/2 + δ - φ
```

---

## 8. Règles Géométriques

### Formule d'Angle d'Incidence
**Formule générale pour l'angle d'incidence:**
```
ω = 15°(λ2 - 9) = 45°
β = 40°
α = 30°
```

Relations géométriques multiples pour dériver les angles en fonction de la position et du temps.

---

## 9. Vitesse Angulaire et Calculs de Coordonnées

### Formule de Vitesse Angulaire
```
ωpv = 5πn(δ)sin(φ) + ωn(δ) + ωn(δ)ωp(φ)ωn(δ)ωn(δ) + ωn(δ)sin(φ)
ωpv = sin³(δ)sin(φ)ωn(ω) + ωn(δ)[ωp(φ)ωn(δ)ωn^(40) + 5πn(δ)sin(φ)]
```

**Résultat:** ωp = 0.694

### Exercice 3: Coordonnées Terrestres de Biarritz
Le calcul implique:
- φ₁ = φ₂ × (coordonnées de Biarritz)
- Calculs de rapport entre systèmes de coordonnées
- Résultat: **123.8, 814 W/m²**

---

## 10. Décalage Horaire - Exercice Sénégal

### Contexte du Problème
Il est **10 h 30** et il y a pas de décalage horaire au **Sénégal** donc:

**Données:**
```
T0 = T1 - UL - CL ⇒ T0 = TL
TL = 12h'
TU = 12h'
```

### Det T3n
```
TU = T3n + (t/15) ⇒ T3n = TU + t/15
```

**Calcul de la Longitude:**
```
T3n = 12h + ((-18.05)/15) = 10.93h = 10h 53 min
```

### Det T3V - Calcul de B
```
B = 360 × (π/366) = 360 × (355/366) = 329.5°
```

**Équation du Temps (ET):**
```
ET (en min) = -0.0002 + 0.04289 cos(329.5) + 7.3509 sin(329.5) 
              - 3.2265 × cos(2 × 329.5) - 9.3912 sin(2 × 329.5) 
              - 0.0903 cos(3 × 329.5) - 0.3364 × sin(3 × 329.5) 
            = 11.08 mn = 11 min
```

**Temps Solaire Vrai:**
```
ET = T3V - T3n ⇒ T3V = ET + T3n
⇒ T3V = 11 mn + 10h53mn
T3V = 11h06 mn
```

### Det ω = angle horaire
```
ω = (360/24) × (T3V - 12) = 15 × (11 + (t/60) - 12) = -13.5°
```

### Calcul Heure Lever et Coucher
```
T3V = 12 - (ω/15) = 12 - (11/15) + 12 = 6,1465 h = 6 h 25min
```

---

## 11. TD8 - Navigation et Calculs de Position Solaire

### Coordonnées terrestres
- **15° 3' 2'' Nord**
- **46° 3' Ouest de Greenwich**

**Calculs de position:**
```
Latitude φ ⇒ φ = 15° + (3/60)° = 15.05° (car Nord)

Longitude λ ⇒ λ = -(46 + (3/60)°) = -46.05° (car Ouest)
```

### Déclinaison solaire au 1 décembre

**Rang du jour:**
```
m = 31 + 28 + 30 + 30 + 30 + 30 + 30 + 31 + 30 + 31 + 30
m = 335
```

**Calcul de la déclinaison:**
```
δ = -23.45° × sin[(360/365)(364 + 335)] ⟹ -22.10°
```

---

## Formules Essentielles à Mémoriser

### Temps
- **TSV = TSN + ET**
- **ω = 15°(TSV - 12)**
- **Tj = 24/π × arccos(tan φ tan δ)/180**

### Position
- **φ** : Latitude (+ Nord, - Sud)
- **λ** : Longitude (+ Est, - Ouest)
- **δ** : Déclinaison solaire (-23° à +23°)

### Azimut
- **sin(Ψ) = cos(δ)sin(ω)/cos(β)**
- **tan(Ψ) = cos(φ)cos(ω)/(cos(φ)sin(ω))**

---

## Points Clés à Retenir

1. ✅ Les conversions entre systèmes de temps (TSV, TSN, ET)
2. ✅ Le calcul de l'angle horaire à partir du TSV
3. ✅ La détermination de la position (latitude/longitude)
4. ✅ Les formules d'azimut et leur application
5. ✅ Le calcul de la durée du jour
6. ✅ L'équation du temps avec ses composantes trigonométriques
7. ✅ Les décalages horaires et fuseaux horaires
