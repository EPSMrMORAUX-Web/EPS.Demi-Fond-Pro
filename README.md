# 🏃 EPS – Course Bac Pro

Application web autonome pour la **gestion et notation des évaluations de course** en EPS (Bac Pro). Fonctionne entièrement en local dans le navigateur, sans installation, sans serveur, sans connexion internet.

---

## 📋 Présentation

L'application couvre deux évaluations distinctes selon le niveau :

| Niveau | Épreuve | Notation |
|--------|---------|----------|
| **1ère Bac Pro** | 3 × 500m | Performance (10pts) + Stratégie/Projet (7pts) + Échauffement (3pts) = /20 |
| **Terminale Bac Pro** | 800m | AFLP1 Perf (7pts) + AFLP2 Maîtrise (5pts) + AFLP5 Comportement + AFLP6 Projet = /20 |

---

## 🚀 Utilisation

1. Ouvrir le fichier `EPS_800m_Evaluation.html` dans un navigateur (Chrome, Firefox, Edge)
2. Choisir le niveau depuis la page d'accueil : **1ère** ou **Terminale**
3. Importer une classe ou saisir les élèves manuellement
4. Renseigner les temps pendant ou après la séance
5. Exporter les résultats en Excel ou PDF

> ⚠️ Aucune installation requise. Tout fonctionne dans un seul fichier HTML.

---

## 🗂️ Structure de l'application

```
Page d'accueil
├── 🏁 Module 1ère – 3×500m
│   ├── Onglet Import
│   ├── Onglet Saisie
│   ├── Onglet Chrono
│   ├── Onglet Résultats
│   └── Onglet Barème
└── ⏱ Module Terminale – 800m
    ├── Onglet Import
    ├── Onglet Saisie
    ├── Onglet Chrono
    ├── Onglet Résultats
    └── Onglet Barème
```

---

## ✏️ Fonctionnalités détaillées

### 🏫 Gestion des classes

- Créer, renommer et supprimer des classes (ex : *2nde Pro 4*, *Terminale BAC Pro*)
- **Import Excel automatique** : le nom du fichier `.xlsx` devient automatiquement le nom de la classe
- Filtrer les élèves par classe dans tous les onglets

### 👤 Gestion des élèves

- Import depuis un fichier Excel (colonnes : A=Nom, B=Prénom, C=Sexe G/F)
- Ajout manuel avec sélection de classe
- Numéro attribué automatiquement à chaque élève (ordre alphabétique)
- Basculer Garçon/Fille en un clic
- Marquer Absent ou Dispensé (réversible)
- Organisation par **vagues** (1 à 4), assignation automatique disponible

### ✏️ Saisie des performances

#### Module 1ère (3×500m)
- Saisie des 3 temps individuels (C1, C2, C3) — format `mm:ss` ou `m` (ex : `2` = 2:00)
- Temps total calculé automatiquement
- Indicateur visuel : case **verte** dès qu'un temps est rempli
- Saisie du **projet de course** pour C2 vs C1 et C3 vs C2 :
  - ↑ Plus rapide / ≈ Égal / ↓ Plus lent
  - Case de **modification** si l'élève change son projet en cours de séance
  - Note automatiquement réduite selon le moment de la modification (C1 ou C2)
- Note d'échauffement (0–3 pts) saisie directement
- Override manuel de la note de stratégie si nécessaire

#### Module Terminale (800m)
- Saisie Tour 1 (400m) et Temps Total (800m) — `3` = 3:00 automatiquement
- Tour 2 calculé automatiquement (Total – Tour 1)
- Différentiel T1–T2 avec code couleur (vert/orange/rouge)
- Projet de course annoncé (en secondes)
- Répartition AFLP5+AFLP6 au choix de l'élève : **6/2 / 4/4 / 2/6**
- Saisie AFLP5 (comportement) directement dans la carte

### ⏱️ Chrono rapide

#### 1ère (3×500m)
- Chrono global en temps réel
- Clic sur **C1 / C2 / C3** d'un élève pour enregistrer son temps au moment du clic
- Indicateurs de couleur par course (bleu C1, orange C2, vert C3)
- Arrêt automatique quand tous les élèves sont complets

#### Terminale (800m)
- Chrono global en temps réel
- **1er clic** sur un élève = T1 (400m)
- **2e clic** = Temps total (800m)
- Arrêt automatique quand tous les élèves sont complets

### 📊 Notation automatique

#### 1ère – Barème stratégie (7 pts)

| Liaisons correctes | Sans modif | Modif au C1 | Modif au C2 |
|---|---|---|---|
| 2 correctes | **7 pts** | 5.5 pts | 4 pts |
| 1 correcte | **3 pts** | 2 pts | 1 pt |
| 0 correcte | 0 pt | — | — |

> Tolérance : ±2s pour valider l'égalité, minimum 1s pour valider une direction.

#### Terminale – Calcul /20

```
Note /20 = AFLP1 (7pts) + AFLP2 (5pts) + AFLP5 + AFLP6
         = Sous-total (12pts) + Comportement/Projet (8pts)
```

Répartition AFLP5/AFLP6 choisie par l'élève :
- **6/2** : priorité comportement (AFLP5 max 6, AFLP6 max 2)
- **4/4** : équilibré (4+4, valeur par défaut)
- **2/6** : priorité projet (AFLP5 max 2, AFLP6 max 6)

### 💾 Sauvegarde

- Sauvegarde **automatique** dans le `localStorage` du navigateur
- Les données persistent entre les sessions sans aucune action de l'enseignant
- Bouton de réinitialisation avec confirmation

### 📤 Export

- **Export Excel (.xlsx)** : tableau complet avec tous les temps, notes et statuts
- **Export PDF** : aperçu plein écran avec bouton d'impression (A4 paysage)
  - Feuille de chrono (avec cases à remplir)
  - Feuille de résultats complète

---

## 🎨 Interface

- Design sombre optimisé pour une **utilisation terrain** (lisibilité maximale)
- Compatible **tablette et ordinateur**
- Code couleur systématique :
  - 🟢 Vert : Tour 1 rempli / Liaison correcte / Note ≥ 14
  - 🔵 Bleu : Total rempli / Vague 1
  - 🟠 Orange : Modification de projet / Note ≥ 10
  - 🔴 Rouge : Absence / Liaison incorrecte / Note < 7
- Saisie en chaîne : `Entrée` passe automatiquement au champ suivant
- Carte élève compacte avec toutes les infos visibles d'un coup

---

## 📁 Fichier unique

L'intégralité de l'application tient dans **un seul fichier HTML** (~128 KB) :

```
EPS_800m_Evaluation.html   ← tout-en-un : HTML + CSS + JavaScript
```

Aucune dépendance locale. La seule librairie externe est **SheetJS** (chargée depuis un CDN) pour la lecture/écriture de fichiers Excel.

---

## 🔧 Personnalisation rapide

| Ce que vous voulez changer | Où modifier |
|---|---|
| Barème performance Garçons 500m | Constante `B5G` dans le `<script>` |
| Barème performance Filles 500m | Constante `B5F` |
| Barème performance Garçons 800m | Constante `BG` |
| Barème performance Filles 800m | Constante `BF` |
| Barème régularité 800m | Constante `BREG` |
| Barème écart projet 800m | Constante `BPROJ` |

---

## 📝 Format du fichier Excel d'import

| Colonne A | Colonne B | Colonne C |
|-----------|-----------|-----------|
| NOM (majuscules) | Prénom | Sexe (G ou F) |
| DUPONT | Camille | F |
| MARTIN | Lucas | G |

> Le nom du fichier Excel est automatiquement utilisé comme nom de classe.

---

## 🛠️ Technologies utilisées

- **HTML5 / CSS3 / JavaScript vanilla** — aucun framework
- **[SheetJS (xlsx)](https://sheetjs.com/)** — import/export Excel
- **localStorage** — persistance des données côté navigateur
- **CSS Grid / Flexbox** — mise en page responsive

---

## 📄 Licence

Usage interne EPS – Bac Pro. Application développée pour un usage pédagogique en établissement scolaire.
