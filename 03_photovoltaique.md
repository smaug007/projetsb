# Systèmes Photovoltaïques - Résumé d'Examen

## 1. NOCT (Normal Operating Cell Temperature)

### Définition et Objectif
**NOCT** est l'application pour Normal Operating Cell Temperature. Ceci définit les conditions d'essai préférées pour les cellules solaires, représentant des conditions plus proches de la réalité que les conditions d'essai standard.

### Conditions d'Essai NOCT
- **Niveau d'éclairement solaire:** 800 W/m²
- **Température extérieure:** 20°C
- **Vitesse du vent:** 1 m/s
- **Montage des cellules:** 1.5 m

### Sélection et Analyse de Modules
Considérer les modules orientés vers une entrée sud dans la structure.

**Information Clé:**
La température admissible pour l'onduleur doit s'aligner avec:
- Nombre de modules en série maintenant la tension dans la plage de température
- **N (Module-max):** Vmpp·ψ(Vmpp) [à +40°C] = 350/20 = 17.5 ≈ **18.55**
- **N (module-min):** Vmpp·inf(Vmpp) [à +70°C] = 100/20 = 5.75 ≈ **14.84**

**Considération de Plage de Température:**
Pour la plage de température de fonctionnement de 11°C de l'onduleur, il faut connecter un module en série à l'onduleur: **5 modules minimum**

---

## 2. Courbes Caractéristiques I-V et Performance

### Analyse de Courbe I-V de Module Photovoltaïque
La courbe caractéristique montre la relation entre le courant et la tension pour un module PV.

**Points Clés sur la Courbe:**
- **Isc** (Courant de Court-Circuit): ~3 mA
- **Voc** (Tension en Circuit Ouvert): Tension maximale à courant zéro
- **Point de Puissance Maximale (Umpp, Impp)**: Point de fonctionnement pour une énergie optimale

### Paramètres de Performance à Différentes Températures

**Aux Conditions d'Essai Standard:**
- **Tension à vide (Tension en Circuit Ouvert) Uo (à +40°C):** 23.4V
- **Courant à puissance max Impp (à 40°C):** 2.34A
- **Tension à vide Uo (à +40°C):** 30.5V
- **Courant de court circuit Icc (à 45°C):** 5.14A
- **Coef de T° de tension Tc(Uo):** β = -10.5 mV/K
- **Coef de T° du courant Tc(Icc):** β = 8.12 mA/K
- **Coef de la T° de la puissance Tc [Pnom]:** αp = -0.45%/K

### Calculs de Point de Fonctionnement

**Coefficients de Fonctionnement:**
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

## 3. Configurations de Systèmes Photovoltaïques

### Connexion en Série (Sans Bypass)
Pour les panneaux PV fonctionnant à différents points sans bypass:
```
V₁ - V₂ = -25.07 - 12.16V  avec z = 1.68A

Avec bypass: z = 5.02 + V₁ = V₂ = 45.07 = 12.16V
```

### Configuration Sans Bypass
```
Sans embrança:
+ Ph = I₁ × V₁ × 2 = 1.68 × 3.02 = 5.07, 0.5W
+ Ph = V₂ = 541.4W

Avec embrança:
+ I₁ = I₂ V₁ = 144.3 × V₁ × 0.64 = 33.24½
+ V₂ = V₂V₂ = -9.07W ⇒ Ph+P₂ = 12.47W
```

**Conclusion:** Le générateur/récepteur et dissipateur d'énergie - le produit est divisé par 4.

### Placement de Diodes en Série
Pour les diodes associées aux bornes de chaque panneau, placer des diodes en série à travers le mélange en parallèle de panneaux:

**Configurations de Circuit:**
- Configurations de panneaux solaires montrées avec diodes de bypass
- Arrangements série et parallèle pour une puissance de sortie optimale

### Calculs Additionnels HD3V et Z₁/Z₂

**Deux panneaux en série:**
- **Diagramme:** 
  - Avantage → v = Vₚ + V₂ = 2Vₚ + 20.1 + λω = -λ,Tλ,I: droite A₁
  - Vₚ + Z₂(Eₐ) Z₃(Eₐ, S₁,β,S₁): v = vₚ + V₂ ⇒ Iₚ,L[Icc + I] = 4λ,X + λλ₀I: droite A₃
  - I = Icc (S₁,β,S₁) Z₁ = v → Il n'y a plus de produits

### Systèmes avec Batteries

**Capacité:**
- Batterie modèle: 200Ah 12 V 64Kg (Annexes)
  - Whord = 12 × 210 = 2520Wh
  - Nb = Vsf / Whord = 25,b1I × 16 / 2520 = 10 batteries

**Poids total:** Nb × 64 = 640Kg

**Durée de vie:**
D'après les docs constructeur, on peut utiliser 1000 cycles avec ces batteries. En effectuant 2 cycles par jour pendant les 2 mois d'été soit:
```
Nu = 1000 / (2 × 2 × 61) = 82 années
```

---

## 4. Installation Photovoltaïque - Schémas et Architecture

### Configuration du Système PV Complet

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

### Onduleur Photovoltaïque
- Conversion DC → AC
- Respect de la gamme de tension d'entrée
- Courant nominal et maximal admissible
- Caractéristiques du fusible DC et de l'onduleur

---

## 5. Dimensionnement des Modules Photovoltaïques

### Calcul du Nombre de Modules Maximum

**Formule de Base:**
Le nombre maximum de modules en série est défini par:
```
N(modules max) = Upmax(Tmin) / Upmax(+40°C) = 600 / 36.2+75 = 16.54
```

### Considérations de Température

1. **Température Maximale (+40°C):**
   - Tension à l'entrée de l'onduleur peut atteindre +40°C
   - Le temps max en entrée d'onduleur doit respecter la limite

2. **Plage de Fonctionnement:**
   - Il faut que les modules soient branchés pour que la tension d'entrée de l'onduleur ne dépasse jamais la plage de fonctionnement
   - Temps d'entrée ne doit pas dépasser certain seuil

### Justifications - Calculs

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

### Dispositif de Supervision
Un dispositif de supervise déconnecte le générateur lorsque:
- La tension d'un panneau chute sous **12Vdc⁺**
```
Vdémon = 11 × 12V = 32V
Vdémon = 11 [ηₚ + βΔT] = 11 [21,b-33 × 10⁻³(60-25)] = -31,1X
```

---

## 6. Dimensionnement des Conducteurs et Câbles

### Section de Câble - Calcul de Chute de Tension

**Méthodologie Générale:**
Pour calculer la section des câbles qui charge jusqu'au circuit, il faut vérifier la chute de tension puis respecter la norme en vigueur.

### Partie A - Calcul du Cable

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

### Partie B - Section Parallèle

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
Pour calculer la chute de tension sur l'ensemble du circuit cette ΔV, il faut ajouter les chutes de tension. Dans notre cas, la chute de tension totale ΔC vaut **0.74%** ce qui est **< à 3%**.

### Vérification du Courant

**Courant Admissible:**
En fonctionnement normal, le courant susceptible de circuler dans des câbles est égal à **1.25 × Isc**, et on ne se préoccupe pas des surintensités de retour car isolant. Le courant admissible des cables doit respecter la condition suivante:

```
Iza ≥ 1.25Isc = 1.25 × 8.4 = 10.54 ≈ 14A (Annexe 3.5)
```

**Conditions Critiques:**
Concernant les câbles entre la boite de jonction et l'onduleur, une seule peut pas se produire du courant retour. Cependant, les courants des 2 strings s'ajoutent, le courant susceptible de circuler de ces câbles est **2 × 1.25 × Isc** en choisissant des **fusibles**:

```
Iza ≥ 1.25 × 2Isc = 2 × 1.25 × 8.4 = 20.54 ≈ 36A (Annexe 3.5)
```

---

## 7. Choix des Équipements de Protection DC

### Selection des Fusibles DC

**Critères de Sélection pour les Fusibles:**
1. Le courant assigné des fusibles doit être conforme au type de l'OTC (Annexe 1.5 = 2.14 ≃ -1) respecter la condition SVTC
2. Le courant assigné (In) des fusibles devra être conforme au juge de l'OTC (1.5 = 2.14 ≃ -1) respecter la condition SVTC:

```
1.45 IaL < In < 2 Iba
1.4 × 8.14 < In ≃ (28 × 8.14) ⇒ 11.36A < In < 16.74
```

**Choix Final:**
Le seul fusible qui répond à cette condition est de **13A**. Le courant admissible du fusible va permettre donc à l'onduleur la protection contre les surintensités.

### Conditions SVTC
Le courant assigné (In) des fusibles doit être conformé au juge suivant:
- Dans la condition SVTC: **1.5 = 2.14 ≃ -1 respecter la condition SVTC**
- Le courant doit respecter: **1.4 IaL < In < 2 Iba**

```
1.4 Isc < In < 2Isc
```

---

## 8. Dimensionnement du Mètre de Modules (Abri Photovoltaïque)

### Détermination du Mètre de Modules

**Dimensions de Base:**
```
Mètre = 14,04 × 3.05 = 35.76 m²
```

### Dimension de Pente

**Calculs Géométriques:**
```
SA = (1.628 × 0.94) = 1.369 m²
SB = ((1.628 + 0.022) × (0.94 + 0.015)) = 1.141 m²
```

**Nombre de Colonnes et Lignes:**
Pour vérifier le mètre provisoire de panneaux NP portrait:
- **Nbtre de colonnes max:** 16,04 / (1.628 + 0.045) = 16.38
- **Nbtre de lignes max:** 3.38 / (1.628 + 0.022) = 2.141

**Calcul Final:**
On peut monter **2 × 16 = 32 modules** (2 rangées de 16 modules)

**Paysage:**
- **Nbtre de colonnes max:** 16,04 / (1.628 + 0.045) = 8.48
- **Nbtre de lignes max:** 8.38 / (0.84 + 0.015) = 4.65

**Résultat:** **4 × 8 = 32 modules** (4 rangées de 8 modules)

### Calcul du Poids de l'Ensemble des Panneaux

**Poids Total:**
```
32 × 16.2 = 518 kg
```

### Puissance Utile

**Calcul de Puissance:**
```
Pc = 32 × 185 Wc = 5920 Wc = 6000 Wc ⇒ Onduleur monophasé
```

---

## 9. Résistivité du Matériau Conducteur et Longueur

### Choix de la Résistivité

**Côte DC:** La présence de parafoudre se justifie selon deux paramètres:
- La densité de foudroiement **Ng**
- La longueur des câbles DC
- L'usage du bâtiment par lequel sont implantées les modules photovoltaïques

**Somme de Toutes les Distances de Câbles:**
On doit déterminer la somme de toutes les distances de câbles:
- D'une part: le champ photovoltaïque et la boite de jonction
- D'autre part: la boite de jonction et l'onduleur

**Longueurs:**
```
L1 = 10m       L3 = 1m
L2 = 15m       L = 26m
```

La longueur **L** est la somme de toutes les longueurs.

### En Traversée du Matériau Conducteur (Cuivre ou Aluminium)

**Formule de Section:**
```
ΔV = (b/Vm) × (L/ΔV) × (cos T × 2Ib)

⇒ δ = (b/Vm) × (L/ΔV) × cos T × 2Ib = (ΔL/236) × (25/0.02 × 0.3 × 2 × 0.538 × 25/0.022) × cos 0.018 × 1 = 8.62 mm²
```

---

## 10. Vérification du Courant pour Circuits AC

### Vérifier le Courant

**Principe de Base:**
En général, la section commerciale c.a.d 4mm² - un câble de 4mm² peut supporter: **45A**. Il convient parfaitement car le courant sortie de l'onduleur monophasé est de **32A**.

### Calculer le Courant Assigné (In) des Disjoncteurs AC

**Critères pour le Disjoncteur:**
Pour qu'un disjoncteur assure la protection contre les surcharges, il convient de définir trois types de courant:
- **Ib:** Le courant maximal d'emploi des conducteurs
- **In:** Le courant assigné du disjoncteur en courant nominal du disjoncteur
- **Iz:** Le courant maximal admissible des conducteurs

**Conditions à Respecter:**
```
Ib < In < Iz = Ib
Iz > In ≥ Ib
```

Le courant à l'entrée de l'onduleur monophasé est de **32A**.

---

## 11. Calculs d'Autonomie et Stockage

### Autonomie
```
Nsst × Wh/1 × Nj × Nps × (1/1) × X = -10 × 2515 × x₀,₉1X × 0,55
Cnominal × Vnominal    √6,15

→ 15,b1I KWh/jour
```

### Calculs d'Énergie

**Wgp(1):**
```
Wgp = Ns₁ × Wh
              1,1
Wgp = lK₁Ls(γ₁,γ₂) × (γₙₘ × γ₁) × (μ₀⁺μ₁)
                               1,1
```

**Module de liaison (Annexe 3-1γ):**
- Wgp (γγ) = 25,b1I Kwh1γ/jour (en somme toutes les valeurs des batteries) fig.5

**Calculs Wfond:**
```
Wfond = Wmonde + Wappes stockage
Wsst = X₁5,b1₁ × W11b1γ
Wfond = Wmonde + Wapres stockage = 16,b11Kwh1γ + 15,111Kwh
```

**Ca l'onduleur:**
```
Wonde onduleur = 0,₉1 × (16,b1I + 1,5,b1I) = 32,₉₃Kwh
= rho d'apport = Wpnde onduleur = 22,35 = 8,35Xb
               √6,15fγcγₙ₁γ     √6,15
```

---

## 12. Analyse Thermique et Performance

### Spécifications de Cathode
**Spécifications:**
- Largeur de Mont Mélian: **45**
- Longueur: **6**
- Altitude: **856 m à 1200 m**

### Calcul de Température Moyenne
**Température moyenne de l'air:**
- Tair moy (°C) = **11.4**

**Température moyenne de l'eau:**
- Teau moy (°C) = **16, 42**

### Rayonnement Solaire Annuel
```
Ep = 1310 kWh/m²/an
```

### Calcul d'Énergie Électrique
```
E = (Eg/Ep) × Ep × PA × PR(Ec) = (5.32 × 1310 × 0.75 × 0.538)/2
E = 5655 kWh/an
```

**Ratio de Performance:**
- PR = performance système
- TRICO = coefficient Trigénération

### Spécifications Techniques - Conditions NOCT

| Paramètre | Valeur |
|-----------|--------|
| Coef de T° Isc | -0.5 mV/°C → augmente de B° |
| Coef de T° Isc | 3.12 mA/°C |
| Influence sur Puissance T° | |
| Coef de T° P | 0.45%/°C |

---

## 13. Densité de Foudroiement

### Détermination de la Densité de Foudroiement (Annexe 3.3F)

**Installation photovoltaïque où doit se monter un sonnet:**
La densité de foudroiement: Ng = 31

**Formule de densité:**
La densité de foudroiement pour un bâtiment se calcule selon l'équation:
```
Ng = (Ng × Sg - Ng)/10

Ng = (Ng × 31)/10 = 3/1
```

**Densité de foudroiement:**
- x = 5 est nécessaire de prévoir un parafoudre côté DC
- La densité de foudroiement Ng étant supérieure à 2,5 et est donc obligatoire d'installer des parafoudres côté DC

---

## Formules Essentielles à Mémoriser

### Dimensionnement
- **N(modules max) = Upmax(Tmin) / Upmax(+40°C)**
- **Scable = (ρ × L × Isc × 2) / (ΔV × 16 Umpp)**
- **Iza ≥ 1.25 × Isc**

### Protection
- **1.4 Isc < In < 2Isc** (fusibles)
- **Ib < In < Iz** (disjoncteurs)

### Performance
- **E = (Eg/Ep) × Ep × PA × PR(Ec)**
- **Pc = Nombre modules × Puissance unitaire**

### Température
- **Umpp = [Umpp,STC + ρmp × ΔT]**
- **Coefficient T° : -0.45%/°C**

---

## Points Clés à Retenir

1. ✅ Conditions NOCT (800 W/m², 20°C, 1 m/s)
2. ✅ Courbes I-V et points de fonctionnement
3. ✅ Configurations série et parallèle
4. ✅ Dimensionnement nombre de modules
5. ✅ Calculs de sections de câbles (ΔV < 3%)
6. ✅ Courant admissible (1.25 × Isc)
7. ✅ Protection fusibles et disjoncteurs
8. ✅ Densité de foudroiement et parafoudres
9. ✅ Architecture complète DC/AC
10. ✅ Calculs d'autonomie et batteries
