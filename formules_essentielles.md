# Fiche de Formules Essentielles - Révision Rapide

## 🌍 Astronomie & Navigation Céleste

### Systèmes de Temps
```
TSV = TSN + ET
TSN = TSV - ET
ET = TSV - TSN
```

### Coordonnées
- **Latitude (φ):** + pour Nord, - pour Sud
- **Longitude (λ):** + pour Est, - pour Ouest
- **Déclinaison (δ):** -23° à +23°

### Angle Horaire
```
ω = 15°(TSV - 12)
ω = (360°/24) × (TSV - 12)
```

### Équation du Temps
```
B = 360 × (n/366)

ET = -0.0002 + 0.04289·cos(B) + 7.3509·sin(B)
     - 3.2265·cos(2B) - 9.3912·sin(2B)
     - 0.0903·cos(3B) - 0.3364·sin(3B)
```

### Durée du Jour
```
Tj = (24/π) × arccos(tan φ × tan δ) / 180
```

### Azimut
```
sin(Ψ) = cos(δ)·sin(ω) / cos(β)

tan(Ψ) = cos(φ)·cos(ω) / (cos(φ)·sin(ω))
```

### Relations Géométriques
```
S = π/2 - φ
S - δ = π/2 - φ → δ = π/2 + δ - φ
```

---

## 🔥 Systèmes Thermiques & Énergétiques

### Capacité Thermique
```
Qth = m × Cp × ΔT
Cth = ρ × V × Cp
```

### Constante de Temps
```
τth = Rth × Cth
```

### Équation Différentielle
```
ΔT(t) = Ke^(-t/τth) + Km·Φm

Ke = -Km·Φm (condition initiale)
```

### Échange de Chaleur
```
∑Q = 0

Q = m × Cp × (Tf - Ti)

Tf = (m₁·T₁ + m₂·T₂) / (m₁ + m₂)
```

### Résistance Thermique
```
Rth = ΔT / Φ       [°C/W]
```

### Perte de Chaleur
```
Q = hc × ΔT × t
```

### Rayonnement Solaire
```
Gext = (24·Isc/π) × [1 + 0.033·cos(360n/365)]

kt = G / Gext   (indice de clarté)

Gr = rayonnement diffus
Gb = rayonnement direct
G = Gr + Gb
```

### Ensoleillement
```
a = 0.409 + 0.516·sin(ω - π/3)
b = 0.60 + 0.4 + 0.476·sin(ω - π/3)

Gi = (cos υ/cos φ) × G
```

---

## ☀️ Systèmes Photovoltaïques

### Conditions NOCT
- Éclairement: **800 W/m²**
- Température extérieure: **20°C**
- Vitesse du vent: **1 m/s**
- Montage: **1.5 m**

### Dimensionnement Modules
```
N(max) = Upmax(onduleur) / Umpp(module à Tmin)

N(min) = Upmin(onduleur) / Umpp(module à Tmax)
```

### Coefficients de Température
```
Umpp(T) = Umpp(STC) + β × ΔT

β ≈ -0.105 V/K  (ou -10.5 mV/K)
α ≈ +8.12 mA/K  (pour Isc)
αp ≈ -0.45%/K   (pour puissance)
```

### Sections de Câbles

**Formule générale:**
```
Scable = (ρ × L × I × 2) / (ΔV × U)

ΔV = (ρ × L × I × 2) / (Scable × U)
```

**Où:**
- ρ = résistivité (Cuivre: 0.0176 Ω·mm²/m)
- L = longueur du câble [m]
- I = courant [A]
- 2 = aller-retour
- ΔV = chute de tension maximale (souvent 3%)
- U = tension [V]

**Vérifications:**
```
ΔV_totale < 3%
ΔV_DC < 1%  (recommandé)
ΔV_AC < 2%  (recommandé)
```

### Courant Admissible
```
Iza ≥ 1.25 × Isc

Pour 2 strings en parallèle:
Iza ≥ 1.25 × 2 × Isc = 2.5 × Isc
```

### Fusibles DC
```
1.4 × Isc < In < 2 × Isc

Où:
- In = courant assigné du fusible
- Isc = courant de court-circuit
```

### Disjoncteurs AC
```
Ib ≤ In ≤ Iz

Où:
- Ib = courant d'emploi
- In = courant assigné disjoncteur
- Iz = courant admissible câble
```

### Production Énergétique
```
E = Ep × S × η × PR

Où:
- Ep = irradiation annuelle [kWh/m²/an]
- S = surface modules [m²]
- η = rendement modules
- PR = Performance Ratio (0.7-0.8)
```

### Puissance Installée
```
Pc = Nmodules × Punitaire

Pc = Nsérie × Nparallèle × Pmodule
```

### Dimensionnement Batteries
```
Wh_batterie = Capacité(Ah) × Tension(V)

Nbatteries = Besoin(Wh) / Wh_batterie
```

**Pour système multi-tension:**
```
Nsérie = Vsystème / Vbatterie
Nparallèle = Besoin / (Nsérie × Wh_batterie)
Ntotal = Nsérie × Nparallèle
```

### Autonomie
```
Autonomie(j) = Capacité_totale(Wh) / Consommation_jour(Wh)
```

### Densité de Foudroiement
```
Si Ng > 2.5 → Parafoudre OBLIGATOIRE

Ng = densité de foudroiement [coups/km²/an]
```

### Résistivité Conducteurs
- **Cuivre:** ρ = 0.0176 Ω·mm²/m (à 20°C)
- **Aluminium:** ρ = 0.029 Ω·mm²/m (à 20°C)

---

## 📊 Valeurs de Référence Importantes

### Constantes Physiques
- **Isc** (constante solaire): 1360-1367 W/m²
- **Cp eau:** 4.18 kJ/(kg·°C)
- **ρ eau:** 1000 kg/m³

### Températures de Référence PV
- **STC** (Standard Test Conditions): 25°C, 1000 W/m²
- **NOCT:** 20°C, 800 W/m²
- **Tmin** calculs: -10°C (Europe)
- **Tmax** calculs: +70°C

### Plages Typiques
- **Performance Ratio (PR):** 0.70 - 0.85
- **Rendement modules:** 15% - 22%
- **Chute tension max:** 3% (total)
- **Facteur sécurité courant:** 1.25

---

## 🎯 Astuces de Calcul Rapide

### Conversions Utiles
```
1 kWh = 3,600,000 J = 3.6 MJ
1°/15 = 4 minutes
15° = 1 heure
π radians = 180°
```

### Ordres de Grandeur
- **Irradiation France:** 1000-1400 kWh/m²/an
- **Production PV résidentiel:** 800-1200 kWh/kWc/an
- **Consommation moyenne maison:** 3000-5000 kWh/an
- **Module standard:** 250-400 Wc
- **Tension module:** 30-40V (Umpp)
- **Courant module:** 8-10A (Impp)

### Vérifications Rapides

**Tension système PV:**
- ✓ Umpp,min > Upv,min (onduleur)
- ✓ Umpp,max < Upv,max (onduleur)
- ✓ Voc,max < Umax,abs (onduleur)

**Courant système PV:**
- ✓ Imp,total < Imax (onduleur)
- ✓ Isc × 1.25 < Iz (câble)
- ✓ 1.4·Isc < In < 2·Isc (fusible)

**Câbles:**
- ✓ ΔV < 3% (total)
- ✓ Iza ≥ 1.25 × Isc

---

## ⚡ Formules par Type de Problème

### Type 1: Position Solaire
1. Calculer φ et λ (coordonnées)
2. Calculer jour n et B
3. Calculer δ (déclinaison)
4. Calculer ET (équation du temps)
5. Calculer TSV
6. Calculer ω (angle horaire)
7. Calculer Ψ (azimut) et β (hauteur)

### Type 2: Thermique
1. Identifier les masses et températures
2. Appliquer ∑Q = 0
3. Calculer Tf ou Q
4. Si dynamique: calculer τth = Rth × Cth
5. Utiliser ΔT = Ke^(-t/τth) + constante

### Type 3: Dimensionnement PV
1. Calculer Nmax (température min)
2. Calculer Nmin (température max)
3. Choisir N entre Nmin et Nmax
4. Vérifier tension à toutes températures
5. Calculer section câbles (ΔV < 3%)
6. Vérifier Iza ≥ 1.25 × Isc
7. Choisir fusibles (1.4·Isc < In < 2·Isc)

### Type 4: Production
1. Identifier Ep (irradiation)
2. Calculer surface ou puissance
3. Appliquer E = Ep × S × η × PR
4. Ou E = Pc × Heures_équivalentes × PR

---

## 🔴 Erreurs à Éviter

1. ❌ Oublier le signe des coordonnées (N/S, E/O)
2. ❌ Mélanger degrés et radians
3. ❌ Oublier le facteur 2 (aller-retour) dans câbles
4. ❌ Négliger les coefficients de température
5. ❌ Oublier le PR dans calculs de production
6. ❌ Confondre Isc et Impp
7. ❌ Oublier le 1.25 pour courant admissible
8. ❌ Vérifier tension à UNE SEULE température
9. ❌ Additionner tensions en parallèle (c'est le courant!)
10. ❌ Additionner courants en série (c'est la tension!)

---

## ✅ Checklist Avant Examen

- [ ] Je connais les formules de temps (TSV, ET, ω)
- [ ] Je sais calculer coordonnées et déclinaison
- [ ] Je maîtrise les calculs thermiques (Qth, τth)
- [ ] Je connais les conditions NOCT
- [ ] Je sais dimensionner les modules (Nmax, Nmin)
- [ ] Je maîtrise les calculs de câbles (section, ΔV)
- [ ] Je connais 1.25 × Isc et 1.4 < In < 2
- [ ] Je sais vérifier Ib ≤ In ≤ Iz
- [ ] Je peux calculer la production annuelle
- [ ] Je connais les ordres de grandeur

---

**💡 Conseil final:** Gardez cette fiche à portée de main pendant vos révisions et l'examen (si autorisé) !

**Bonne chance ! 🎓✨**
