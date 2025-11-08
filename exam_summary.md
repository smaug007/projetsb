# Résumé d'Examen - Astronomie & Navigation Céleste

## Vue d'ensemble des Concepts Clés

### 1. Systèmes de Temps et Formules

#### Équations de Temps de Base
- **TSV (Temps Solaire Vrai)**: TSV = TSN + ET
- **ET (Équation du Temps)**: Correction entre le temps solaire moyen et le temps solaire vrai
- **TSN (Temps Solaire Moyen)**: Temps solaire moyen

#### Relations de Temps
```
TSV = TSN + ET
TSN = TSV - ET
ET = TSV - TSN
```

#### Équation Différentielle de Température
```
cas particulier: Vm + Vm = cte → ΔTp = cte

d(ΔT)/dt + ΔTp = Km·Φm

0 ≠ ΔTp = Km·Φm → ΔTp = Km·Φm

Solution finale: ΔT = Ke^(-t/τm) + Km·Φm
```

### 2. Systèmes de Coordonnées

#### Coordonnées Terrestres
- **Latitude (φ)**: Position Nord-Sud (+ pour Nord, - pour Sud)
  - Exemple: φ = 48° + (48/60)° = 48.8° (signe + car Nord)
  
- **Longitude (λ)**: Position Est-Ouest (+ pour Est, - pour Ouest)
  - Exemple: λ = +(λe + (45/60)°) = +λe,15° (signe + pour Est)

#### Calcul du Temps Géographique
- **Déclinaison solaire**: Varie tout au long de l'année
  - Plage: -23° à +23°
  - Peut être déterminée à l'aide de la formule de Casper avec une bonne précision

#### Formules de Navigation et Identification
- Formule de navigation au point Q: **UPLY(Q) = UPLY, PLPL/Y ± ORSTA/L**
- Identification: **IL = P - O = P7** (formule de référence)
- Position temporelle: **Ip > I** ou rapport de temps
- Calculs spécifiques d'orientation et de navigation céleste
- Utilisation des rapports angulaires pour déterminer la position

### 3. Calculs de Position Solaire

#### Angle Horaire (ω)
```
ω = (360°/24) × (TSV - 12) = 15°(TSV - 12) = 15°(15.1167 - 12)
ω = 46.7505°
```

#### Temps Spéciaux
- **Greenwich**: À 4h 45' 14" UT le 1er octobre
- Les calculs impliquent la conversion entre différents fuseaux horaires et références

#### Formules Additionnelles pour l'Angle Horaire
- **ULPY(Q) ≡ UPLY₁ - PLPV/UPLYL ± ORSTA/L**
- **Orélation**: Ulpy = 0.5S/S (conditions spéciales)
- **ω = arccos(-tan ω tan(-0.02)** (formule alternative)
- **HDPA (T) = HDPL × τPD⁴¹⁴ = 8 min 53s**
- Utilisation des variations temporelles pour les calculs de position

### 4. Azimut et Direction

#### Calcul de l'Azimut
L'angle d'azimut est exprimé en degrés à partir d'une direction de référence.

Composantes clés de la formule:
- Implique des fonctions trigonométriques (sin, cos)
- Dépend de la latitude, de l'angle horaire et de la déclinaison solaire
- Tenir compte des projections sur différents plans

#### Méthode du Méridien Solaire
```
sin(Ψ) = cos(φ)cos(ω)/cos(β)

tan(Ψ) = cos(φ)cos(ω)/(cos(φ)sin(ω))
```

Où:
- Ψ = angle d'azimut
- φ = latitude
- ω = angle horaire
- β = paramètre d'angle

### 5. Diagrammes Clés et Relations Géométriques

#### Heures de Lever/Coucher
- **THL** (Temps Heure Lever): Heure du lever du soleil
- **THC** (Temps Heure Coucher): Heure du coucher du soleil

Méthode de calcul:
```
THL = TSN + (-ωL+C)/15 → -ET = [formule]
THC = TSNC + ωL+C/15 → -ET = [formule]
```

#### Diagramme de la Trajectoire Solaire
- Montre la relation entre:
  - Ligne d'horizon
  - Équateur
  - Trajectoire solaire
  - Angles de référence (φ, δ, β, ω)

### 6. Calcul de la Durée du Jour

#### Durée du jour
```
Tj = 24/2 - arccos(tan ω tan φ)/180

Tj = 10.18 hr = 10h 18 min
```

### 7. Notes Importantes et Conditions

#### Conditions Initiales
- Après le coucher du soleil (après coucher)
- Conditions limites: 
  - Ke^(t/τm) + Km·Φm = 0 → Ke = -Km·Φm
  - Dérivations de forme finale

#### Considérations de Symétrie
- **Lever et coucher sont placés symétriquement par rapport à midi**

### 8. Applications Pratiques

#### Différences de Temps Local
- Méridien solaire: Différent de l'heure locale
- Cette différence est appelée "équation du temps différentielle par rapport au temps GPS"
- Varie tout au long du jour et de l'année

#### Calculs d'Octobre
**Spécificités du 19 octobre:**
- La France a 2 heures d'avance sur le temps de référence
- Le temps administratif local est avancé de 2 heures par rapport à la référence (Greenwich/méridien de référence)
- Calculs de décalage de temps géographique requis

#### Relations d'Angles
```
S = π/2 - φ
x + 5 = π
donc:
x + 5 - S = x + 5 ⟹ S - δ = 5
S - δ = π/2 - φ → δ = π/2 + δ - φ
```

### 9. Règles Géométriques

#### Formule d'Angle d'Incidence
**Formule générale pour l'angle d'incidence:**
```
ω = 15°(λ2 - 9) = 45°
β = 40°
α = 30°
```

Relations géométriques multiples pour dériver les angles en fonction de la position et du temps.

### 10. Référence de Date d'Examen
**Date: 30/09/25**

Cadre de problème exemple:
- Déterminer les coordonnées terrestres (Montélimar)
- Référence diapositive 13
- Donnée: 44°34' Nord, 4°45' Est de Greenwich

### 11. Vitesse Angulaire et Calculs de Coordonnées

#### Formule de Vitesse Angulaire
```
ωpv = 5πn(δ)sin(φ) + ωn(δ) + ωn(δ)ωp(φ)ωn(δ)ωn(δ) + ωn(δ)sin(φ)
ωpv = sin³(δ)sin(φ)ωn(ω) + ωn(δ)[ωp(φ)ωn(δ)ωn^(40) + 5πn(δ)sin(φ)]
```

**Résultat:** ωp = 0.694

#### Exercice 3: Coordonnées Terrestres de Biarritz
Le calcul implique:
- φ₁ = φ₂ × (coordonnées de Biarritz)
- Calculs de rapport entre systèmes de coordonnées
- Résultat: **123.8, 814 W/m²**

---

## Systèmes Thermiques et Énergétiques

### 12. Capacité Thermique et Échange de Chaleur

#### Exercice 1: Calculs Thermiques (4 paramètres)
**Conditions Initiales:**
- Ta = 20°C (température ambiante)
- Ti = 45°C (température initiale)

#### Partie 1.1: Calcul de la Capacité Calorifique Thermique
Pour un réservoir chauffé (Φₘ = 70W):
```
Qth = dQ/dt = hc × dT/dt

→ Qth = hc = 9Vc + 4.18 × 10³ × 0.2 × 10³ = 836 kJ/°C
```

#### Applications Photovoltaïques - Calculs Supplémentaires

**A.5) Détermination de γₘₘ pour un panneau:**
```
γₘₘ = Vₚₛ / (Nₛₚ × (V₁ + V₂)) + E₀γc + Eγₚₛ
```

**Annexe 4:**
- **mPₚ**: Calcul basé sur formules de puissance
- **Pc/Annexe 4**: Ratios de performance
- **XP**: Valeurs de référence = +0.4376

**Formules de température:**
```
mPₚ = [λ + XP/Δ]⁻¹ × Pc/Annexe 4 = -12.376
```

**A.6) Détermination de Sᵤ:**
```
Sᵤ = (λ - λs) + (λ/ηₛₖ) × (1/ηₛₖ,mPₛ + Eγmc)/(ρ₁.ρ₂.ρ₃₀,Eγₚₛ)

Sᵤ = (λ - 0.5) + 0.5/0.13 [1 - 0.5 + (2λ + 0.13)/(0.148 × 0.0186 × 0.516)]

Sᵤ = -3S + 1.38
```

**A.7) Détermination de Sᵧ:**
Condition: **Sᵤ = S₃ⁿᶜ + [ω/ηₛₖ.mPₛ + Eγc.Eγₚₛ]/(Pcn.2ρ.1₀γₛ × 1/Eγₚₛ)**

Application numérique:
```
Sᵧ = 1 - (0.5 + 0.5/0.13) × [0³.10⁻³(60⁻25)]/[500 × 0.3161]
```

**A.8) ηₚ = Sᵤ/Sᵧ × 0.5g7 = 89 panneaux:**
- Configuration optimale pour système PV

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

---

### 13. Technologie des Cellules Solaires - NOCT (Normal Operating Cell Temperature)

#### Définition et Objectif
**NOCT** est l'application pour Normal Operating Cell Temperature. Ceci définit les conditions d'essai préférées pour les cellules solaires, représentant des conditions plus proches de la réalité que les conditions d'essai standard.

#### Conditions d'Essai NOCT
- **Niveau d'éclairement solaire:** 800 W/m²
- **Température extérieure:** 20°C
- **Vitesse du vent:** 1 m/s
- **Montage des cellules:** 1.5 m

#### Exercices Pratiques - Calculs NOCT

**A.5) Calculs basés sur annexes (A2S, S × x × 0.1S, S × x²(⁻³)):**
- Créé en ombrage avec un panneau
- Su = noyé de cellule x surface d'une cellule

**A.6):**
```
Annexe 4
mPₚ = [λ + XP/Δv]⁻¹ × Pc/Ammax.4 = -12.376
            A
        XP = + 0.4376
        1       Pc
```

**A.7) Puissance électrique restituée à la ligne durant les 10 mètres:**
Calcul basé sur les pertes en ligne et résistance

**A.12) Énergie électrique restituée la ligne durant l'année:**
```
E = 1350 kWh/m²/an × 1,94 m²/panneau
Pour l'énergie produite, il faut tenir compte du rendement global de la micro-centrale. Il n'agit de l'énergie par 1 heure d'été.
cos θ + 0.23, on doit tenir compte de l'horaire d'été d'hiver
```

**A.11.a) Accepté de l'irradiation au mois de juillet est:**
```
Japproximale = (180NΔΞΣ) × [17h·Δλ]/15
```

Pour l'énergie produite, il faut tenir compte du rendement global de la centrale qu'il s'avère de l'énergie par 1 heure d'ombre.

#### Sélection et Analyse de Modules
Considérer les modules orientés vers une entrée sud dans la structure.

**Information Clé:**
La température admissible pour l'onduleur doit s'aligner avec:
- Nombre de modules en série maintenant la tension dans la plage de température
- **N (Module-max):** Vmpp·ψ(Vmpp) [à +40°C] = 350/20 = 17.5 ≈ **18.55**
- **N (module-min):** Vmpp·inf(Vmpp) [à +70°C] = 100/20 = 5.75 ≈ **14.84**

**Considération de Plage de Température:**
Pour la plage de température de fonctionnement de 11°C de l'onduleur, il faut connecter un module en série à l'onduleur: **5 modules minimum**

---

### 14. Configurations de Systèmes Photovoltaïques

#### Partie 2.1: Connexion en Série (Sans Bypass)
Pour les panneaux PV fonctionnant à différents points sans bypass:
```
V₁ - V₂ = -25.07 - 12.16V  avec z = 1.68A

Avec bypass: z = 5.02 + V₁ = V₂ = 45.07 = 12.16V
```

#### Calculs Additionnels HD3V et Z₁/Z₂

**A.2) Deux panneaux sont en série:**
- **Diagramme:** 
  - Avantage → v = Vₚ + V₂ = 2Vₚ + 20.1 + λω = -λ,Tλ,I: droite A₁
  - Vₚ + Z₂(Eₐ) Z₃(Eₐ, S₁,β,S₁): v = vₚ + V₂ ⇒ Iₚ,L[Icc + I] = 4λ,X + λλ₀I: droite A₃
  - I = Icc (S₁,β,S₁) Z₁ = v → Il n'y a plus de produits

**Diagramme:**
```
        Avantage
  0 < I < -λ,Sλ
        ⇒ V₁ - V₀ - V₁ = 2λ - 0,bλI
        V₀ = ∞₁ - V₁ = 18 - b,bλI

  V = Vₚ + V₂ = λ0 - λ,Tλλ + λ₀ - 1.14λI     Droite A3
  
  λ₁,Tλλ ≥ I > λcc avec λcc = λ,bλ
        ⇒ E₁ = 0 (pas de λcc)
```

**2.B) Annexe:**
- pI∩λ
  - Intercepts en M₁ avec la droite λ₁
  - V = λλ,S + λλ,0I = S,₁₃I
    - I = λλ,S / λλ,₁S = 3,₀λI ⇒ V = -15,0₃V

**pI∩λ₂**
  - Intercepts en M₂ avec la droite λ₁
  - V = 133 + 30,bλI = S,₁₃I
    - I = 133 + 10(λ,b-I) = -133 - 30,bλI     droite λ₁
                           λ,₁₃λI
  - Tλ,bλI ≥ V₀ ≥ I et niγε plus de produits

**2.B) Annexe:**
```
pIIIλ
  - pI∩λ: V = λλ,S + λλ,0I = S,₁₃I
    Annexe²
```

**§2.20) I ≡ λ₁: Vsf:** (λλ,S + λλ,0I) × (-Xb,bλI × λ₃,S)
- λλ,bλVₚ; I = λS,₁₃I × IS,λS.²

**%λ₀) E₁λs = E₁λS¹(λIII):** 25,bλI Kwhλγ(jour (en somme toutes les valeurs des batteries) fig.5

**%λb) Capacité:**
- Batterie modèle: 200Ah 12 V 64Kg       Annexes
  - Whord = λ2 × 210 = 2520Wh
  - Nb = Vsf / Whord = 25,bλI × 16 / 2520 = 10 batteries

**%Nb = Nb × 64 = b40Kγ:**

D'après les docs, constituteur, on peut utiliser vous cycles avec ces batteries, en effectue 2 cycles y et pour γ et les 2 mois d'été soit:
```
Nu = λ000 / (2 × 2 × bλI) = 82 années
```

Voir tous de m' aγγès du constituter γγ le completer de la batterie - γγ les 10 mois constants

#### Partie 2.5: Configuration Sans Bypass
```
Sans embrança:
+ Ph = I₁ × V₁ × 2 = 1.68 × 3.02 = 5.07, 0.5W
+ Ph = V₂ = 541.4W

Avec embrança:
+ I₁ = I₂ V₁ = 144.3 × V₁ × 0.64 = 33.24½
+ V₂ = V₂V₂ = -9.07W ⇒ Ph+P₂ = 12.47W
```

**Conclusion:** Le générateur/récepteur et dissipateur d'énergie - le produit est divisé par 4.

#### Partie 2.6: Placement de Diodes en Série
Pour les diodes associées aux bornes de chaque panneau, placer des diodes en série à travers le mélange en parallèle de panneaux:

**Configurations de Circuit:**
- Configurations de panneaux solaires montrées avec diodes de bypass
- Arrangements série et parallèle pour une puissance de sortie optimale

---

### 15. Analyse Thermique de Cathode

#### Problème d'Exercice (Annexe 3.1)
**Spécifications de Cathode:**
- Largeur de Mont Mélian: **45**
- Longueur: **6**
- Altitude: **856 m à 1200 m**

#### Partie 1.2.1: Calcul de Température Moyenne
**Température moyenne de l'air:**
- Tair moy (°C) = **11.4**

**Température moyenne de l'eau:**
- Teau moy (°C) = **16, 42**

#### Partie 1.2.3: Rayonnement Solaire Annuel (Annexe 3.1)
```
Ep = 1310 kWh/m²/an
```

#### Partie 1.2.4: Calcul d'Énergie Électrique (Annexe 3.1)
```
E = (Eg/Ep) × Ep × PA × PR(Ec) = (5.32 × 1310 × 0.75 × 0.538)/2
E = 5655 kWh/an
```

**Ratio de Performance:**
- PR = performance salon
- TRICO = coef Trigeneratory

#### Partie 1.3: Spécifications Techniques - Conditions NOCT
Pour **coefficient de T° (Coefficient de température)**, utiliser Division B:

| Paramètre | Valeur |
|-----------|--------|
| Coef de T° Isc | -0.5 mV/°C → augmente de B° |
| Coef de T° Isc | 3.12 mA/°C |
| Influence sur Puissance T° | |
| Coef de T° P | 0.45%/°C |

---

### 16. Courbes Caractéristiques I-V et Performance des Modules

#### Analyse de Courbe I-V de Module Photovoltaïque
La courbe caractéristique montre la relation entre le courant et la tension pour un module PV.

**Points Clés sur la Courbe:**
- **Isc** (Courant de Court-Circuit): ~3 mA
- **Voc** (Tension en Circuit Ouvert): Tension maximale à courant zéro
- **Point de Puissance Maximale (Umpp, Impp)**: Point de fonctionnement pour une énergie optimale

#### Paramètres de Performance à Différentes Températures

**Aux Conditions d'Essai Standard:**
- **Tension à vide (Tension en Circuit Ouvert) Uo (à +40°C):** 23.4V
- **Courant à puissance max Impp (à 40°C):** 2.34A
- **Tension à vide Uo (à +40°C):** 30.5V
- **Courant de court circuit Icc (à 45°C):** 5.14A
- **Coef de T° de tension Tc(Uo):** β = -10.5 mV/K
- **Coef de T° du courant Tc(Icc):** β = 8.12 mA/K
- **Coef de la T° de la puissance Tc [Pnom]:** αp = -0.45%/K

#### Calculs de Point de Fonctionnement

**Coefficients de Fonctionnement Suivants:**
```
Umpp1 = [Uo + ρc ΔT]
Umpp2 = [Umpp + ρmp ΔT]
```

**Résolution des Résultats:**
- **Tension à vide Uo (à +20°C):** [-88.5 - 0.105 × (- 10⁻³ + 45⁴)] = **36.075V**
- **Tension à puissance max Umpp (à +40°C):** [-33.4 - 0.105 × (- 48 - 45⁴)] = **29, 175V**
- **Tension à puissance max Umpp (à 30°C):** [-33.4 - 0.105 × (30⁴ - 45⁴)] = **20, 775V**

**Fonctionnement du Module à Puissance Maximale:**
La tension du module à puissance maximale est entre 20.775 et 33.175V.

---

### 17. Différentiel de Température et Constantes de Temps

#### Équation Différentielle de Température
```
ΔT(t)/ρTh × Cth + 1/e = c × t/τth

La c × e^(-t/τth) = ln[1 - ΔT(t)/hTh × Φth]

e^(-t/τth) = ln[1 + ΔT(t)/hTh × Φth]

td = -2/τth × ln[1 - ΔT(t)/hTh·Φth·Cth] = 1.5h.
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

---

### 18. Installation Photovoltaïque - Schémas et Architecture

#### Configuration du Système PV Complet

**Composants Principaux:**

1. **Côté Production (DC):**
   - Modules photovoltaïques (rangées)
   - Boîte de jonction
   - Interrupteur sectionneur DC
   - Onduleur photovoltaïque
   - Cellule DC (Protection)
   
2. **Côté Réseau (AC):**
   - Compteur de non-consommation
   - Compteur de production
   - Coffret AC
   - Liaison au réseau
   - Parafoudre
   - Disjoncteur de raccordement
   - Phase, Neutre, PE (Protection Équipotentielle)

**Longueurs Caractéristiques:**
- Longueur L1 (côté DC)
- Longueur L2 (côté AC)
- Cable DC (+/-)
- Table DC (série et parallèle)

#### Onduleur Photovoltaïque
- Conversion DC → AC
- Respect de la gamme de tension d'entrée
- Courant nominal et maximal admissible
- Caractéristiques du fusible DC et de l'onduleur

---

### 19. Dimensionnement des Modules Photovoltaïques

#### Calcul du Nombre de Modules Maximum

**Formule de Base:**
Le nombre maximum de modules en série est défini par:
```
N(modules max) = Upmax(Tmin) / Upmax(+40°C) = 600 / 36.2+75 = 16.54
```

#### Exercice Supplémentaire - Calculs de Puissance et Autonomie

**§2.1) Un dispositif de supervise déconnecte le générateur lorsque:**
- La tension d'un panneau chute sous **λ2Vdc⁺**
```
Vdémon = λλ × λ2V = 32V
Vdémon = λλ [ηₚ + βΔT] = λλ [2λ,b-33 × 10⁻³(60-25)] = -3λ,λX
```

**Considérations de Température:**

1. **Température Maximale (+40°C):**
   - Tension à l'entrée de l'onduleur peut atteindre +40°C
   - Le temps max en entrée d'onduleur doit respecter la limite

2. **Plage de Fonctionnement:**
   - Il faut que les modules soient branchés pour que la tension d'entrée de l'onduleur ne dépasse jamais la plage de fonctionnement
   - Temps d'entrée ne doit pas dépasser certain seuil

#### Justifications (§3)

**Calcul de Tension:**
```
Upmax(+70°C) = 16 × 22.175 = 88.21.4 > Upvmpp = 100V
Upmax(-10°C) = 16 × 29.175 = #66.8 < Upvmpp = 550V
```

**Calcul du Courant:**
```
Ipmpp,d (un string) = 3.34A ⇒ IS.58A ≠ 22A par 2 strings
```

**Montage en Parallèle:**
- On acquiert les unités en tension et courant
- Montés en parallèle pour acquérir des sorties de courant
- Dimensionnement en fonction de l'onduleur monophasé

---

### 20. Dimensionnement des Conducteurs et Câbles

#### Section de Câble - Calcul de Chute de Tension

**Méthodologie Générale:**
Pour calculer la section des câbles qui charge jusqu'au circuit, il faut vérifier la chute de tension puis respecter la norme en vigueur.

#### Calculs Supplémentaires pour Installations Complexes

**§ Autonomie:**
```
Nsst × Wh/1 × Nj × Nps × (λ/λ) × X = -10 × 25λS × x₀,₉λX × 0,₅₅
Cnominal × Vnominal    √b,λS

→ λS,bλI KWh/jour
```

**§ Du × Nj:** 
```
(λ/90) × X × Nj = (λ/90) × X = 0,₆bλ × 0,6λ = 0,₅₅X
Cnominal                √b,λS
```

**§1.16) Wgp(λ):**
```
Wgp = Ns₁ × Wh
              1,1
Wgp = lK₁Ls(γ₁,γ₂) × (γₙₘ × γ₁) × (μ₀⁺μ₁)
                               1,1
```

**Dimensionnage:**
- W₁gp ~ 12 mètr/J les panneaux sur un portée (γₕ₁γ')

**§1.17)** 
```
mPₚ,Npsq = λK₁ × 3λλ   Npₛ₁ λγλ₂₁λ
∀λλγₙ₁       γλX,bλ × 6fγγγₑₚₛ
```

**§1.18) Module de liaison (Annexe 3-λγ):**
- Wgp (γγ) = 25,bλI Kwhλγ/jour (en somme toutes les valeurs des batteries) fig.5

**§1.19)**
```
Wfond = Wmonde + Wappes stockage
Wsst = X₁S,bλ₁ × Wλλbλγ
Wfond = Wmonde + Wapres stockage = 16,bλλKwhλγ + λS,λλλKwh
```

**Ca l'onduleur:**
```
Wonde onduleur = 0,₉₁ × (16,bλI + λ,S,bλI) = 32,₉₃Kwh
= rho d'apport = Wpnde onduleur = 22,35 = 8,35Xb
               √b,λ5fγcγₙ₁γ     √b,λS
```

Par dessénien (requis fig. 2)

**Tableaux de Calcul:**

| Zone | Paramètre | Valeur |
|------|-----------|--------|
| AD (Aluminium) | ρL × xl | S = μL/x |
| U | U⁰ |  |

#### Partie A - Calcul du Cable

**Formule de Section:**
```
Scable = (ρ × L × Isc) / (ΔV × Ucmax) = (ρ × L × Isc × 2) / (ΔV × 16 Umpp)

= (0.038×16 × 23 × 2 × 8.54) / (0.03 × 37.414) = 0.16mm²
```

**Proposition et Vérification:**
On propose une section de câble de **4mm²**, on calcule ensuite la chute de tension sur la partie du circuit A:

```
ΔV = (ρ × L × Isc × 2) / (Scable × 16 Umpp) = (0.038×16 × 25 × 2 × 8.54) / (4 × 37.414) = 0.52%
```

#### Partie B - Section Parallèle

**Calcul de Section:**
```
Scable = (ρ × L × 2Isc × 2) / (ΔV × 16 Umpp) = (0.038×16 × 6 × 2 × 8.54) / (0.03 × 37.414) = 0.52mm²
```

**Proposition:**
On propose une section de câble de **10mm²**, on calcule ensuite la chute de tension sur la partie du circuit B:

```
ΔV = (ρ × L × 2Isc × 2) / (Scable × 16 Umpp) = (0.038×16 × 16 × 2 × 8.54) / (4 × 37.414) = 0.44%
```

**Vérification Globale:**
Pour calculer la chute de tension sur l'ens du circuit cette ΔV, il faut ajouter les chutes de tension aursi dans notre cas. La chute de tension totale ΔC vaut **0.74%** ce qui est **< à 3%**.

#### §2.3) Vérification du Courant

**Courant Admissible:**
En fonctionnement normal, le courant susceptible de circuler dans des câbles est égal à **1.25 × Isc**, et en ne se préoccupe pas des surintensités de retour car isolant. Si le fait, le courant admissible des cables doit respecter la condition suivante:

```
Iza ≥ 1.25Isc = 1.25 × 8.4 = 10.54 ≈ 14A (Annexe 3.5)
```

**Conditions Critiques:**
Concernant les câbles entre la boite de jonct. et l'onduleur, une seule peut pas se produire du courant retour. Cependant, les courants des 2 strings s'ajoutent comme impraticable, le courant susceptible de circuler de ces câbles est **2 × 0.25 × Isc** en choisir de des **fusibles**:

```
Iza ≥ 1.25 × 2Isc = 2 × 1.25 × 8.4 = 20.54 ≈ 36A (A annexe 3.5)
```

---

### 21. Choix des Équipements de Protection DC

#### Selection des Fusibles DC

**Critères de Sélection pour les Fusibles:**
1. Le courant assigné des fusibles doit être conforme au type de l'OTC (Annexe 1.5 = 2.14 ≃ -1) respecter la condition SVTC
2. Le courant assigné (In) des fusibles devra être conformé au juge de l'OTC (1.5 = 2.14 ≃ -1) respecter la condition SVTC:

```
1.45 IaL < In < 2 Iba
1.4 × 8.14 < In ≃ (28 × 8.14) ⇒ 11.36A < In < 16.74
```

**Choix Final:**
Le seul fusible qui répond à cette condition est de **13A**. Le courant admissible du fusible va permettre donc à l'onduleur la protection contre les surintensités.

#### §2.2) Protection et Longueur Totale

**Calcul du Courant (Long par image, prt des circuit A poreux):**
```
Ltotal + 25m et B (2 + 25H₁ = 16m²)
```

**Partie A:** Les charg. string prévale de courrant Impp = 3.34A 
**Partie B:** La mise en parallèle de 2 strings donne un courant **Impp = 15.68A**

**Conditions de Température:**
En fonctionnement normal (Ø courant susceptible de circuler dans les câbles est égal à **1.25 × Isc**, et en ne se préoccupe pas de surintensité de retour car isolant)

---

### 22. Dimensionnement du Mètre de Modules (Abri Photovoltaïque)

#### §1.2) Détermination du Mètre de Modules

**Dimensions de Base:**
```
Mètre = 14,04 × 3.05 = 35.76 m²
```

#### §2.2) Dimension de Pente %

**Calculs Géométriques:**
```
5A = (1.628 × 0.94) = 1.369 m²
5B = ((1.628 + 0.022) × (0.94 + 0.015)) = 1.141 m²
```

**Nombre de Colonnes et Lignes:**
Pour vérifier le mètre provisoire de panneaux NP portrait:
- **Nbtre de colonnes max:** 16,04 / (1.628 + 0.045) = 16.38
- **Nbtre de lignes max:** 3.38 / (1.628 + 0.022) = 2.141

**Calcul Final:**
On peut monter **2 × 16 = 32 modules** (2 rangées de 8 modules)

**Paysage:**
- **Nbtre de colonnes max:** 16,04 / (1.628 + 0.045) = 8.48
- **Nbtre de lignes max:** 8.38 / (0.84 + 0.015) = 4.65

**Résultat:** **4 × 8 = 32 modules** (4 rangées de 8 modules)

#### §1.4) Calcul du Poids de l'Ens des Panneaux

**Poids Total:**
```
32 × 16.2 = 518 kg
```

#### §1.7) Puissance Utile

**Calcul de Puissance:**
```
Pc = 32 × 185 Wc = 5920 Wc = 6000 Wc ⇒ Onduleur monophasé
```

---

### 23. Câbles et Courant Admissible - Conditions SVTC

#### Calcul du Courant Assigné (In) des Fusibles DC

Le courant assigné (In) des fusibles doit être conformé au juge suivant:
- Dans la condition SVTC: **1.5 = 2.14 ≃ -1 respecter la condition SVTC**
- Le courant doit respecter: **1.4 IaL < In < 2 Iba**

**Calculs:**
```
I3B ≥ 1.425 × 2 × 8.4 = 21A < 36A (annexe 3.5)
```

**Choix:**
Le courant assigné (In) des fusibles DC - le courant assigné des fusibles doit être conformé au juge de l'OTC (1.5 = 2.14 ≃ -1) respecter la condition SVTC:

```
1.4 I sc < In < 2I sc
```

---

### 24. Résistivité du Matériau Conducteur et Longueur

#### Choix de la Résistivité

**Côte DC:** La présence de parafoudre se justifie selon deux paramètres:
- La densité de foudroiement **Ng**
- La longueur des câbles DC
- L'usage du bâtiment par lequel sont implantées les modules photovoltaïques

**Somme de Toutes les Distances de Câbles:**
On doit termeêtre - la somme de toutes les distances de câbles apparant:
- D'une part: le chp photovoltaïque et la boite de joncts
- D'autre part: la boite de joncts et l'onduleur

**Longueurs:**
```
L1 = 10m       L3 = 1m
L2 = 15m       L = 26m
```

La longueur **L** est la somme de toutes les longueurs.

---

### 25. Résistivité et Facteur de Puissance

#### En Traversée du Matériau Conducteur (Cuivre ou Aluminium)

**Formule de Section:**
```
ΔV = (b/Vm) × (L/ΔV) × (cos T × 2Ib)

⇒ δ = (b/Vm) × (L/ΔV) × cos T × 2Ib = (ΔL/236) × (25/0.02 × 0.3 × 2 × 0.538 × 25/0.022) × cos 0.018 × 1 = 8.62 mm²
```

**Application Numérique:**
```
δ = (b/Vm) × (L/ΔV) × (cos T × 2I × cos(L,T)/ΔI) = 8.62 mm²
```

---

### 26. Vérification du Courant pour Circuits AC

#### §2.2.3) Vérifier y le Courant

**Principe de Base:**
En général, la section commerciale c.a.d 4mm² - un câble de 4mm² peut supporter: **45A**. Il convient parfaitemt car le courant sortie de l'onduleur monophasé est de **32A**.

#### §2.2.4) Calculer le Courant Assigné (In) des Dijonteurs AC

**Critères pour le Disjoncteur:**
Pour qu'un disjoncteur assure la protection contre les surcharges, il convient de définir trois types de courant:
- **Ib:** Le courant maximal d'emploi des conducteurs
- **In:** Le courant assigné du disjoncteur en courant nominal du disjoncteur
- **Iz:** Le courant sort à respecter maximal admissible des conducteurs

**Conditions à Respecter:**
```
Ib < In < Iz = Ib
Iz > In ≥ Ib
```

Le courant à l'entrée de l'onduleur monophasé est de **32A**.

---

### 27. Décalage Horaire au Sénégal - Exercice Pratique

#### Contexte du Problème
Il est **10 h 30** et il y a pas de décalage horaire au **Sénégal** donc:

**Données:**
```
T0 = T1 - UL - CL ⇒ T0 = TL
TL = 12h'
TU = 12h'
```

#### Exercice Additionnel - Filteur et Fonctionnement

**Filteur 2:**
```
Wgp(γ₁) = 0,2S × λX16 cos¹[(mPₛ+½)-μ₀] × mPₚ × Nγ × Sᵤ
                    1,1
```

**§λλ) À certains moments, on exige assez d'énergie et à:**
- d'autres moments pas assez nécessaire de stocker (S,S, %)
  - (K)

**§λλS) On peut stocker l'énergie entre δλh δ et λ2h δὖ puis entre:**
- 13h δ et 13h δS

**§λλ) On utilise le résultat de la quest** μ puis on effectue une intégrale sur les plages.

```
Wgp(γ₁) = 2 × [∫₁₁₁·₅ λXλ₂₂+λaλλγ mPₛ dγ]
```

**§λλS) Wsσ =** 25,bλI Kwhλγ/jour (en somme toutes les valeurs des batteries) fig.5

**§λ16)**
```
E₁λs = 2λ,X ÷ λS,bλI = -α,₉₁
        16.65

Wnord = λ2 × λλ0 = λ520Wh

Nb = Vsf × 16 = 25,bλI × 16 = 10 batterie
    Whard        2520
```

**§λλ) On se place μᵧ une consé γγγηα§§fγγγ fig. Pγ = 16γδw:**

#### §.5) Det T371
```
TU = T3n + (t/15) ⇒ T3n = TU + t/15
```

**Calcul de la Longitude:**
```
22 T3n = 12h + ((-18.05)/15) = 10.93h = 10h 53 min
```

#### §.6) Det T3V

**Calcul de B:**
```
B = 360 × (π/366) = 360 × (355/366) = 329.5°
```

**Équation du Temps (ET):**
```
ET (en min) = -0.0002 + 0.04289 cos(329.5) + 7.3509 sin(329.5) - 3.2265 × cos(2 × 329.5) - 9.3912 sin(2 × 329.5) - 0.0903 cos(3 × 329.5) - 0.3364 × sin(3 × 329.5) = 11.08 mn = 11 min
```

**Temps Solaire Vrai:**
```
ET = T3V - T3n ⇒ T3V = ET + T3n
⇒ T6V = 11 mn + 10h53mn
T3V = 11h06 mn
```

#### §.7) Det ω = angle horaire

**Formule:**
```
ω = (360/24) × (T3V - 12) = 15 × (11 + (t/60) - 12) = -13.5
```

#### §.8) Calcul Heure Lever et Coucher

**Formulation:**
```
T3V = 12 - (ω/15) = 12 - (11/15) + 12 = 6,1465 h = 6 h 25min
```

---

## Exercices Corrigés en Classe - Addition aux Concepts

### 28. Conditions de Fonctionnement et Applications GPS (TD & OST AL 2025)

#### Exercice - Deux Conditions
**Données initiales:**
- Ip = Ig
- Im < Ig

**Pour une application correcte:**
Le courant nominal Ig doit être disjoncteur dont être compris entre:
```
-11 < Im < 45A
```

**Densité de foudroiement:**
- x = 5 est nécessaire de prévoir un parafoudre côté DC
- La densité de foudroiement Ng étant supérieure à 2,5 et est donc obligatoire d'installer des parafoudres côté DC

---

### 29. TD8 - Navigation et Calculs de Position Solaire

#### A. Tipo méthode V600° et angle horaire du soleil

**1.4.1) Coordonnées terrestres:**
- **15° 3' 2'' Nord**
- **46° 3' Ouest de Greenwich**

**Calculs de position:**
```
Latitude φ ⇒ φ = 15° + (3/60)° = 15.05° (car Nord)

Longitude λ ⇒ λ = -(46 + (3/60)°) = -46.05° (car Ouest)
```

**Pour le croquis: page d'étude (LECLIMA/2024)**

---

#### 1.4.2) Déclinaison solaire au 1 décembre

**Rang du jour:**
```
m = 3A + 28 + 30 + 30 + 30 + 30 + 30 + 5A + 30 + 5A + 30
m = 335
```

**Calcul de la déclinaison:**
```
δ = -23.45° × sin[(360/365)(364 + 335)] ⟹ -22.1/10°
```

---

#### 1.4.3) Durée du jour
```
arcos (tan φ tan λ)/360

Tj = 24/π × arcos(tan φ tan λ)/180

Tj = 11h 63h = 11h 63 min
```

---

### 30. Détermination de la Densité de Foudroiement d'aide de l'Annexe 3.3F

**Installation photo voltages où doit se monter un sonnet:**
La densité de foudroiement: Ng = 31

**Formule de densité:**
La densité de foudroiement pour un bâtiment trapaise se calcule selon l'équation:
```
Ng = (Ng × Sg - Ng)/10

Ng = (Ng × 3A)/10 = 3/1
```

#### Exercice Pratique - Cours K (23 NOVEMBRE 2024 et VENDREDI 10/10/25)

**TD5**

**λ.λ) détermination maintenance:**
Energie mécanique de base eau pour Wₚ:
```
Wₚₛ = 1/30 [∫₁₀⁰ (λS,S¹ + λ₁,₅J×(λS,₁,I) + (λ,₁X(bλ,₁))] + 1/31 (50,λ + 5λ,λ × Wλ,₁ + λb,λ))

= b,₃λKwh
```

**W₀:**
```
W₀ = 1/2 × 1/30 [∫₁₀⁰ (13λ,λ + 260,λ + 36S,λ + 35S) + 3λ₃ + λ₁0 + 23λ + 23S)]

= 38,λ₃Kwh
```

**Wλ = W₀ - Wb = 38,λX - b,₃λ = 33,λSkwh = W₀**

**λ.₁) Wmλp = 2λX₀ = 2λ × λbδS² = 32,5Kwh ~ W₀**

**λ.3) Annexe 2 (fig 13):**
L'angle optimal varie entre 10° et 30° sur l'année. On l'utilise à la centrale est installée n'est on peut diriger un angle noyé de 21° (la moyenne entre la valeur maxime et minimum de la moyenne de juillet et août).

**λλ) Eγγ = 1/2 (35λλδγ₁ + 685) Sg¹¹T Kwhδm⁻¹γour**

**Retour de long:** Le calcul simple pour la formule de capacité.
```
trhug = √S/Ng = 3 + m
```

Et il n'est pas nécessaire de mettre en place des parafoudres côte DC sauf en cas exceptionnel améliorer la qualité de fiabilité de l'installation.

**2.5.1) AC (côté continu):** On a passé l'onduleur

**2.5.2) Calcul de courant d'emploi en deux sites du courant:**
```
tophasé        U2 = √3 V Ucost = (3×Pr)/(3×U×cost) = (3+V)/(cost) = 0

monophasé      P = VιI cost ⇒ Icost ⇒ P = VιI cost = [(7×cos) + (√3×300)]/√3

S = √3VI = cos ω → sin ω → cos(sin υ)
δ = √3I = √3 × -√3 V²

Avec x résonnante linéaire des conducteurs (rtm)
  b: coefficient 2 en triphasé et x en monophasée
  ρ: résonnant ébair lors du calcul
```

---

### 31. Calcul d'Angle Solaire et Trajectoire

#### A.10) Azimut
**Définition:**
La position du soleil est exprimée en jets de l'angle azimut Ψ:
- Angle que fait la projets de la direction du soleil avec le direct du nord
- Cet angle est mesuré positivement vers l'ouest
- L'angle de l'altitude solaire β angle que fait la directe du soleil avec sa projets

**Diagramme de trajectoire:**
[Schéma montrant: lever, coucher, l'équateur, et les angles correspondants]

---

#### L'azimut local est donné par la formule de Came
```
sin(Ψ) = cos(δ)sin(ω)/cos(β)

au lever et au coucher cos β = 0:
soit    sin(Ψ) = 1 ⟹ cos β cos ω = cos δ (cos ω)
```

**L'angle horaire mesure à partir du midi et:**
```
L'azimut    ω = (360°/24)(TSVc - 12) = 15°(TSVc - 12) ⟹ 15°(15.1167 - 2) = δ
L'azimut    β = 45°

Le PSVc on l'azimut est negative le matin et positif le soir
donc zéro sin(Ψ) = 1 cos(δ)cos(ω)cos(-22,10)cos(75.4) ⇒
                                    sin ω = -ω cos cos
                                    Ψ = ± 45.84°
```

---

### 32. Rayonnement Solaire et Calculs d'Incidence

#### 2.3) Avant d'atteindre le sol: le rayonnement solaire est atténué par l'atmosphère et les nuages

Le rapport entre le rayonnement du sol et le rayonnement extraterrestre est appelé indice de clarté:
```
kt = Φ + Φ0
```

---

#### 2.5) mt: le rapport de la valeur horaire au total quotidien de l'ensoleillement sur le plan horizontal global

Cet angle horaire est l'angle horaire du soleil à son coucher exprimé en radians et il est l'angle horaire du soleil pour le milieu de l'heure. Pour laquelle le calcul est fait.

S'exprime en radians et avec sa formule de leur et d'ordure par l'ensoleillement diffus:
```
a = 0.409 + 0.516sin(ω - π/3) = 0.67

b = 0.60 + 0.4 + 0.476sin(ω - π/3) = 0.33

Ay = (b/24) × (arcosω - ω)cosωcosω/sinω - ω cosωcω = 0.192
```

**Ai = (b/24) × (cos ω - cos ω cos(0) sin(ω)/sin ω - ω cosω) ⇒ Ai = π/4a**

---

#### 2.6) Ai et Az

**Calculs:**
```
Gi = (cosυ)/cosφ × G - 0.1177 × 4 + 4.45 = 0.538 kW kL¹ m⁻¹ jour

Gb = G - Gi = 0.389 - 0.316 = 0.213 kW kL¹ m⁻¹ jour
```

---

#### 2.8) L'ensoleillement horaire
```
Gp = Gi(cosφ/cosφ) + Gi((A+cosβ)/2) + Gp((A-cosβ)/2)

Gz = 0.242 × [(cos 20.363)/(cosφ 35.34)] + 0.546 × ((A+cosβ)/2) + 0.37 × (0.2 × ((A-cosβ)/2))

Gz = 0.7636 kW kL¹ m⁻¹ jour
```

---

### 33. 2e Gisemt Solaire - Calculs Détaillés

#### 2.1) Calculons le rayonnement solaire broit
```
Gext = (24 × Isc/π) [A + 0.033cos(360n/365)]

ΔN:   Gext = (24 × 1360/π) [A + 0.033 cos(2π × 305°/365)]

      Gext = 10.32h × 1.39 → W kL¹m⁻¹/jour = 10.724.823 kW kL¹m⁻¹jour
```

---

#### 2.2) Calcul du rayonnement Gb

```
Gb = (24 × Isc/π) [A + 0.033 cos(2π/365)] [(cosφ cos 8 sin ω + (ω × sin))/(365)]

Gb = (24 × 1350/π) [A + 0.033 cos(2π/365)] [(cos 45.05° cos 15.05° sin 15.05° + ω × 1/22.414)]

sin Γ1 × 4 + Γ1 cos Γ1 san Γ2 5.05° × -22.10°)

= 7.334 kW kL¹ m⁻¹ jour
```

---

#### 2.5) L'indice kt
```
kt = G/Gext = (41×/1534) = 0.56
```

---

#### 2.4) Calcul la moyenne mensuelle du rayonnement solaire diffus kt
```
Gr = Πm3Λ + Πm3Kr + kY Kr

Gr = 41.38 Λ + 84 Kr - 61.48 + 0.936 Kr

Gr = 0.536 Gr = A.48 kW kL¹ m⁻¹ jour

Le rayonnement solaire ηa μι être arrivé en deux composantes:
L'incollation direct, émise pas le disque solaire et l'ensoleillement degis émise pas le reste du la voute céleste. On présume le contenu donc de calculer la moyenne mensuelle de l'ensoleillement degis quotidien.
```

---

### 34. Problèmes Pratiques - Applications Numériques

#### Retro du charge

**1. Instruction pratique pour la position de litres aux des éléctricités:**
- Alteration li proprioception + étrendre de la valuer reprenables de l'horizon 
- Observation propriose émis l'ont et un charge le poste de litres 
- Si le hoc proprire sont de la propre éta Πéve le charge 
- Li de le hoc propriré éta fixer + élecne + chexe applayer + et

**2. Caractéristique du charge:**
- Le hoc L = 5 m
- Plan incliné selon du et du recevour les petits de élecne
- Il semible du niveau du fam applaye dans le de l'onore prépare de charge
- La surface + de ca fonction: π3 m

**3. Instructions sur l'utilisation et réclamements de change:**
- Écrire la propriété per le petite des litres aux des éléctricités
- Eltration li proprint + pour le des éterés + proprée
- Définitions proprine part une le proprie que crocue + l'appariation
- Métraxe de la proprotion: δ + de des + propre
- La proprie proping + et la profore trope 3 le la caprare
- Pour de profore proping + la de et proprie + la applaye + sur la profose caprare partie li el le un le proprée + lhore
- H₀ ± proprant et + propre + proppent de litres des change

---

## Liste de Contrôle Récapitulative pour l'Examen

### Astronomie & Navigation Céleste
- [ ] Comprendre les conversions de système de temps (TSV, TSN, ET)
- [ ] Savoir calculer les coordonnées (latitude/longitude)
- [ ] Maîtriser les calculs d'angle horaire (ω = 15°(TSV - 12))
- [ ] Pouvoir calculer l'azimut à partir des données de position
- [ ] Comprendre les calculs de temps de lever/coucher du soleil
- [ ] Connaître la formule de durée du jour
- [ ] Comprendre les relations géométriques dans la sphère céleste
- [ ] Pratiquer les conversions de système de coordonnées
- [ ] Mémoriser les formules clés pour la position solaire
- [ ] Comprendre le concept d'équation du temps et son calcul
- [ ] Maîtriser les formules de vitesse angulaire (ωpv)
- [ ] Savoir calculer l'équation du temps avec la formule complète
- [ ] Appliquer les décalages horaires internationaux (ex: Sénégal)

### Systèmes Thermiques & Énergie
- [ ] Comprendre les calculs de capacité thermique (Qth)
- [ ] Maîtriser l'analyse du régime permanent
- [ ] Savoir résoudre les équations différentielles homogènes
- [ ] Calculer les constantes de temps (τth = Rth × Cth)
- [ ] Appliquer les équations d'échange de chaleur
- [ ] Comprendre les équations différentielles de température
- [ ] Pratiquer les calculs d'analyse de coûts

### Systèmes Photovoltaïques
- [ ] Comprendre les conditions NOCT (Normal Operating Cell Temperature)
- [ ] Savoir lire et interpréter les courbes caractéristiques I-V
- [ ] Calculer la performance des modules à différentes températures
- [ ] Comprendre les coefficients de température pour les modules PV
- [ ] Maîtriser les configurations PV en série et parallèle
- [ ] Savoir quand et comment utiliser les diodes de bypass
- [ ] Calculer la puissance de sortie dans différentes configurations
- [ ] Comprendre les critères de sélection de modules pour onduleurs
- [ ] Appliquer les calculs de tension et courant pour les arrays PV
- [ ] Calculer la production d'énergie annuelle (kWh/an)
- [ ] Dimensionner le nombre de modules maximum (Nmax = Upmax(Tmin) / Upmax)
- [ ] Calculer les sections de câbles avec chute de tension (ΔV)
- [ ] Vérifier le courant admissible (Iza ≥ 1.25 × Isc)
- [ ] Choisir les fusibles DC selon les critères (1.4 Isc < In < 2 Isc)
- [ ] Calculer les dimensions et nombre de modules par rangée
- [ ] Déterminer le poids total de l'installation
- [ ] Calculer la puissance utile totale (Pc)
- [ ] Comprendre l'architecture complète d'une installation PV
- [ ] Maîtriser les schémas DC et AC
- [ ] Calculer la résistivité et section des conducteurs
- [ ] Choisir les disjoncteurs AC (Ib < In < Iz)
