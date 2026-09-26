# Justification du choix du DataSet 

## Le dataset
Le dataset choisi est `CT KIDNEY DATASET: Normal-Cyst-Tumor and Stone` disponible à --> `https://www.kaggle.com/datasets/nazmul0087/ct-kidney-dataset-normal-cyst-tumor-and-stone`.

Le dataset contient 4 catégories (kyste, sain, cailloux, tumeur).
Les proportions sont respectivement de 3709, 5077, 1377 et 2283.
Le dataset contient 12446 images et tag de type.

## Pourquoi ?
L'objectif du projet est de pouvoir faire du clustering donc trouver des groupes selon les images que nous allons donner.
Nous avions le choix entre deux types de dataset, un premier ne contenant que des sujets sains et d'une maladie, et de l'autre un dataset multi-problème qui contient plusieurs cas de maladie. 

Nous avons donc décidé de partir sur le deuxième type de dataset, il nous semblait plus pertinent d'avoir plusieurs maladies.
De plus, ajouter une nouvelle maladie à détecter sera plus simple par la suite si l'IA devait évoluer car on se base déjà sur plusieurs maladies/problèmes de santé.