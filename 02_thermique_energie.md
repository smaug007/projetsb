# Systèmes Thermiques & Énergétiques - Résumé d'Examen

## 1. Équations Différentielles de Température

### Équation Fondamentale
```
cas particulier: Vm + Vm = cte → ΔTp = cte

d(ΔT)/dt + ΔTp = Km·Φm

0 ≠ ΔTp = Km·Φm → ΔTp = Km·Φm

Solution finale: ΔT = Ke^(-t/τm) + Km·Φm
```

### Équation Différentielle Complète
```
ΔT(t)/ρTh × Cth + 1/e = c × t/τth

La c × e^(-t/τth) = ln[1 - ΔT(t)/hTh × Φth]

e^(-t/τth) = ln[1 + ΔT(t)/hTh × Φth]

td = -2/τth × ln[1 - ΔT(t)/hTh·Φth·Cth] = 1.5h
```

---

## 2. Capacité Thermique et Échange de Chaleur

### Exercice 1: Calculs Thermiques (4 paramètres)

**Conditions Initiales:**
- Ta = 20°C (température ambiante)
- Ti = 45°C (température initiale)

#### Partie 1.1: Calcul de la Capacité Calorifique Thermique
Pour un réservoir chauffé (Φₘ = 70W):
```
Qth = dQ/dt = hc × dT/dt

→ Qth = hc = 9Vc + 4.18 × 10³ × 0.2 × 10³ = 836 kJ/°C
```

#### Partie 1.2: Analyse du Régime Permanent
**Observation:** Quand 2th δ = -60¹14h + 70 joules/seconde
**Donnée:** Φₘ = 70W

En régime permanent, on peut écrire le bilan thermique:
```
dT/dt = Φₘ/Rth → dT/dt/Δt = -60-70/120 = 0.64°C/W

τth = Rth × Cth = 0.64 × 836 × 10³ = 535 × 10³ = 149 R = 3.5 min
```

#### Partie 1.3: Détermination de la Durée pour Amener l'Eau à 45°C
En utilisant les équations de dynamique thermique:
```
Φth = dT/dt × Rth + cth × d(ΔT)/dt

Rth × cth × d(ΔT)/dt + ΔT = hth × Φth
```

C'est une équation différentielle homogène du premier ordre car homogène en ΔT.

Pour l'équation homogène:
```
Bth × cth × d(ΔT)/dt + ΔT = 0  ⟹  cth + Rth × cth × th = 0

→ cth × d(ΔT)/dt + ΔT = 0  ⟹  ΔTh = Ke^(-t/τth)
```

#### Partie 1.4: Analyse des Coûts
**Calcul du coût journalier:**
```
P = R/Eh ⟹ Q = P × t = 2100 × 5 = 12 kWh/h
```

On déduit aussi le coût:
- **Coût journalier = 0.13 × 8 × 12 = 2.19367**
- **Coût annuel = 2.19367 × 365 = 800.67€**

#### Partie 1.5: Analyse d'Échange de Chaleur
Sortie préliminaire du bâtiment:
- **Nh = 80%** à **80°C à 65°C** (T1) qui entre
- **Th2** sortie à **65°C** (T1) qui sort en T° d'équilibre Th

**Calcul d'Échange de Chaleur:**
L'échange de chaleur se produit rapidement entre l'eau chaude et l'eau froide:
```
∑Q = 0 ⟹ Qa + Qf = 0
ha × Qa × ΔTa + hf × Qf × ΔTf = 0

⟹ Tf = (ha × Qo + hf × Tf)/(ha + hf) = (80 × 145 + 120 × 45)/200 = 45°C
```

#### Partie 1.8: Perte de Chaleur du Bâtiment
De 6h 20 à 12h 30, sur 6h d'écoulée: La T° a chuté de 45°C à 40°C, résultant en une perte de chaleur:
```
Q = hc ΔT = 80 × 4 × 18 × 10⁻¹ (40 - 45) = -4180 kJ
```

---

## 3. Conditions Limites et Initiales

### Conditions Initiales
- Après le coucher du soleil (après coucher)
- Conditions limites: 
  - Ke^(t/τm) + Km·Φm = 0 → Ke = -Km·Φm
  - Dérivations de forme finale

---

## 4. Constantes de Temps

### Calcul de la Constante de Temps
```
τth = Rth × Cth
```

**Exemple:**
- Rth = 0.64°C/W
- Cth = 836 kJ/°C
- τth = 0.64 × 836 × 10³ = 535 × 10³ s = 149 h = 3.5 min

---

## 5. Rayonnement Solaire et Calculs d'Incidence

### Avant d'atteindre le sol
Le rayonnement solaire est atténué par l'atmosphère et les nuages.

Le rapport entre le rayonnement du sol et le rayonnement extraterrestre est appelé indice de clarté:
```
kt = Φ + Φ0
```

### mt: Rapport de la valeur horaire
Le rapport de la valeur horaire au total quotidien de l'ensoleillement sur le plan horizontal global.

Cet angle horaire est l'angle horaire du soleil à son coucher exprimé en radians et il est l'angle horaire du soleil pour le milieu de l'heure pour laquelle le calcul est fait.

S'exprime en radians et avec sa formule de lever et d'ordre par l'ensoleillement diffus:
```
a = 0.409 + 0.516sin(ω - π/3) = 0.67

b = 0.60 + 0.4 + 0.476sin(ω - π/3) = 0.33

Ay = (b/24) × (arcosω - ω)cosωcosω/sinω - ω cosωcω = 0.192
```

**Formule:**
```
Ai = (b/24) × (cos ω - cos ω cos(0) sin(ω)/sin ω - ω cosω) ⇒ Ai = π/4a
```

### Calculs Ai et Az
```
Gi = (cosυ)/cosφ × G - 0.1177 × 4 + 4.45 = 0.538 kW kWh⁻¹ m⁻¹ jour

Gb = G - Gi = 0.389 - 0.316 = 0.213 kW kWh⁻¹ m⁻¹ jour
```

### L'ensoleillement horaire
```
Gp = Gi(cosφ/cosφ) + Gi((A+cosβ)/2) + Gp((A-cosβ)/2)

Gz = 0.242 × [(cos 20.363)/(cosφ 35.34)] + 0.546 × ((A+cosβ)/2) + 0.37 × (0.2 × ((A-cosβ)/2))

Gz = 0.7636 kW kWh⁻¹ m⁻¹ jour
```

---

## 6. Gisement Solaire - Calculs Détaillés

### Calculons le rayonnement solaire extraterrestre
```
Gext = (24 × Isc/π) [1 + 0.033cos(360n/365)]

ΔN:   Gext = (24 × 1360/π) [1 + 0.033 cos(2π × 305°/365)]

      Gext = 10.32h × 1.39 → W kWh⁻¹m⁻¹/jour = 10.724.823 kW kWh⁻¹m⁻¹jour
```

### Calcul du rayonnement Gb
```
Gb = (24 × Isc/π) [1 + 0.033 cos(2π/365)] [(cosφ cos δ sin ω + (ω × sin))/(365)]

Gb = (24 × 1350/π) [1 + 0.033 cos(2π/365)] [(cos 45.05° cos 15.05° sin 15.05° + ω × 1/22.414)]

sin Γ1 × 4 + Γ1 cos Γ1 sin Γ2 5.05° × -22.10°)

= 7.334 kW kWh⁻¹ m⁻¹ jour
```

### L'indice kt
```
kt = G/Gext = (41×/1534) = 0.56
```

### Calcul la moyenne mensuelle du rayonnement solaire diffus kt
```
Gr = Πm3Λ + Πm3Kr + kY Kr

Gr = 41.38 Λ + 84 Kr - 61.48 + 0.936 Kr

Gr = 0.536 Gr = 1.48 kW kWh⁻¹ m⁻¹ jour

Le rayonnement solaire peut être divisé en deux composantes:
L'insolation directe, émise par le disque solaire et l'ensoleillement diffus émis par le reste de la voûte céleste. On présume le contenu donc de calculer la moyenne mensuelle de l'ensoleillement diffus quotidien.
```

---

## 7. Exercice Pratique - Cours K (TD5)

### Détermination maintenance
Energie mécanique de base eau pour Wp:
```
Wps = 1/30 [∫₁₀⁰ (15,5¹ + 11,5J×(15,1,I) + (1,1X(b1,1))] + 1/31 (50,1 + 51,1 × W1,1 + 1b,1))

= 6,31Kwh
```

### W₀
```
W₀ = 1/2 × 1/30 [∫₁₀⁰ (131,1 + 260,1 + 365,1 + 355) + 313 + 110 + 231 + 235)]

= 38,13Kwh
```

**Calculs:**
```
W1 = W₀ - Wb = 38,1X - 6,31 = 33,15Kwh = W₀

Wm1p = 2180 = 21 × 1645² = 32,5Kwh ~ W₀
```

### Annexe 2 (fig 13)
L'angle optimal varie entre 10° et 30° sur l'année. On l'utilise à la centrale est installée n'est on peut diriger un angle moyen de 21° (la moyenne entre la valeur maxime et minimum de la moyenne de juillet et août).

**Calcul:**
```
E11 = 1/2 (3514641 + 685) S911T Kwh6m⁻¹jour
```

---

## Formules Essentielles à Mémoriser

### Thermique
- **Qth = hc × dT/dt**
- **τth = Rth × Cth**
- **ΔT = Ke^(-t/τth) + Km·Φm**

### Échange de Chaleur
- **∑Q = 0** (conservation de l'énergie)
- **Q = hc ΔT** (perte de chaleur)

### Rayonnement
- **kt = G/Gext** (indice de clarté)
- **Gext = (24 × Isc/π) [1 + 0.033cos(360n/365)]**

---

## Points Clés à Retenir

1. ✅ Capacité thermique et calculs Qth
2. ✅ Régime permanent et constante de temps τth
3. ✅ Équations différentielles homogènes
4. ✅ Échange de chaleur entre fluides
5. ✅ Calculs de coûts énergétiques
6. ✅ Rayonnement solaire et indice de clarté
7. ✅ Gisement solaire et calculs d'ensoleillement
