# Projet d'Analyse de Données Médicales : Classification d'IRM et Clustering de Témoignages

## 1. Présentation du Projet
Ce projet de Data Science propose une double approche analytique sur des données médicales. Il est structuré autour de deux axes majeurs traitant chacun des problématiques distinctes (Computer Vision et Natural Language Processing) :

*   **Apprentissage Supervisé (Vision par Ordinateur) :** Classification d'images IRM de patients pour identifier 4 pathologies distinctes. Cette partie inclut le prétraitement des images via OpenCV, la prévention des fuites de données (Data Leakage) via `GroupShuffleSplit`, et la comparaison d'algorithmes (Logistic Regression, SVM, MLPClassifier) optimisés via `GridSearchCV`.
*   **Apprentissage Non-Supervisé (NLP) :** Regroupement (Clustering) de témoignages textuels de patients pour identifier des profils symptomatiques. Cette partie exploite la vectorisation TF-IDF, la réduction de dimension (TruncatedSVD) pour contrer le fléau de la dimension, et compare les approches KMeans, Spectral Clustering et DBSCAN.

---

## 2. Prérequis et Installation

Pour garantir le bon fonctionnement des scripts et des notebooks, il est impératif d'isoler l'environnement d'exécution. Le projet fournit un fichier `requirements.txt` listant les dépendances exactes (notamment `scikit-learn`, `pandas`, `numpy`, `matplotlib` et `opencv-python`).

### Création et activation de l'environnement virtuel (VENV)

Ouvrez un terminal à la racine du projet et exécutez les commandes suivantes :

**Sur Windows :**
```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

**Sur linux/ Mac :**
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## 3. Architecture du Projet

Le projet sépare rigoureusement les scripts d'acquisition, de prétraitement, d'entraînement et la documentation théorique.

```
├── README.md                 
├── requirement.txt                        # Liste des dépendances Python
├── DownloadCSV.py                         # Script d'acquisition des données (images IRM)
├── kidneyData.csv                         # Dataset brut des images IRM (Vision)
├── Supervise.csv                          # Fichier cible et métadonnées (Vision)
├── Student_Dataset.csv                    # Dataset brut des témoignages patients (NLP)
├── Student_Clean.csv                      # Fichier des témoignages patients nettoyé (NLP)
├── Matrice.npy                            # Matrices des images générées 
├── CT-KIDNEY-DATASET-Normal-Cyst-Tumor-Stone/  # Images IRM téléchargées
├── Supervised Learning/
│   ├── librairies/
│   │   └── CV2.md                         # Justification technique d'OpenCV
│   ├── Models/
│   │   ├── LogisticRegression.ipynb
│   │   ├── MLPClassifier.ipynb
│   │   ├── SVM.ipynb
│   │   └── SupervisedModels.ipynb         # Notebook principal supervisé
│   ├── PreProcessing/
│   │   ├── JustificationCV2.md
│   │   ├── PosteAnalayse.ipynb            # Analyse du dataset supervisé
│   │   └── PreProcessing.ipynb            # Génération de Supervise.csv et Matrice.npy
│   └── Reflexion/
│       ├── Models/
│       │   ├── LogiticRegression.md       # Explication de la Régression Logistique
│       │   ├── MLPClassifier.md           # Explication du MLPClassifier
│       │   └── SVM.md                     # Explication du fonctionnement du SVM
│       └── PreProcessing/
│           └── Justification_Choix.md     # Justification du choix du dataset
└── Unsupervised Learning/
    ├── librairies/
    │   └── Stop_Words.md                  # Justification technique du filtrage sémantique
    ├── Models/
    │   ├── DBSCAN.ipynb
    │   ├── ModelKMeans.ipynb
    │   ├── ModelSpectralClustering.ipynb
    │   └── UnsupervisedModels.ipynb       # Notebook principal non supervisé
    ├── PreProcessing/
    │   ├── Graphs.ipynb
    │   ├── PostAnalyse.ipynb              # Analyse du dataset de témoignages
    │   └── PreProcessing.ipynb            # Génération de Student_Clean.csv
    └── Reflexion/
        ├── Models/
        │   ├── DBSCAN.md
        │   ├── KMeans.md
        │   ├── KMeans_ExplicationCode.md
        │   └── SpectralClustrering.md
        └── PreProcessing/
            ├── Analyse_Graphique.md
            └── Analyse_Post_PreProcessing.md
```
*(Note : L'arborescence ci-dessus est indicative, veuillez ajuster les noms de dossiers selon votre structure exacte).*


## 4. Pipeline d'Exécution (Ordre Strict)

Pour reproduire les résultats, l'exécution doit suivre l'ordre chronologique de la pipeline de données. Ne lancez pas les Notebooks sans avoir généré les données au préalable.
### Étape 1 : Acquisition des données

Exécutez le script de téléchargement pour récupérer le dataset d'images IRM nécessaire à la partie supervisée.

```bash
python3 download.py
```

### Étape 2 : Prétraitement (Vision)

Afin d'éviter de saturer la RAM lors de l'entraînement, les images sont redimensionnées, converties en niveaux de gris via cv2, puis transformées en tableaux mathématiques.
Lancez le script de preprocessing qui va générer le fichier Matrice.npy.

```bash
python src/preprocessing.py
```

### Étape 3 : Entraînement et Analyse

Une fois le fichier Matrice.npy généré et les CSV présents, vous pouvez ouvrir et exécuter les Notebooks de bout en bout :

    Notebook_Supervise.ipynb

    Notebook_NonSupervise.ipynb

## 5. Standard de Qualité : Gestion des Erreurs (Code 84)

La robustesse de ce code est assurée par une gestion d'erreur stricte des entrées/sorties (I/O).
Conformément aux exigences techniques, si un fichier source critique vient à manquer lors de l'exécution, le programme ne crashe pas silencieusement. Il intercepte l'erreur via un bloc try/except, signale le fichier manquant à l'utilisateur, et force la fermeture du programme avec un exit code 84.

Cette sécurité est implémentée sur :

    L'ouverture des fichiers .csv de données.

    L'ouverture du dossier contenant les images brutes.

    Le chargement du fichier pré-calculé Matrice.npy.