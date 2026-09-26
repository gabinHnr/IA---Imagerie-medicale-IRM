# Le modèle SVM (Support Vector Machine)

## Principe de fonctionnement
Le SVM (Machine à Vecteurs de Support) est un algorithme de classification puissant dont l'objectif est de tracer une frontière de décision optimale entre différentes classes (ici, nos 4 maladies). 

Contrairement à d'autres modèles géométriques, il ne cherche pas simplement une ligne de séparation, mais il cherche à **maximiser la marge**, c'est-à-dire la zone de sécurité entre la frontière et les images les plus proches de chaque maladie (ces images repères sont appelées les "vecteurs de support"). 

Pour des données intriquées (comme le chevauchement de nos maladies 1 et 2), le SVM utilise l'**astuce du noyau (Kernel Trick)**. Cela lui permet de déformer l'espace mathématique pour tracer des frontières non-linéaires (des courbes, des bulles de protection) au lieu de simples lignes droites.

## Avantages
* **Efficacité en haute dimension :** Il est extrêmement robuste face à un nombre massif de variables, ce qui est parfait pour traiter les milliers de pixels de nos IRM.
* **Précision chirurgicale :** Grâce à la maximisation de la marge, il offre une excellente séparation sur les données complexes.

## Inconvénients
* **Gourmand en ressources (Scalabilité) :** Le temps de calcul et la consommation mémoire explosent lorsque le nombre d'images augmente considérablement.
* **Sensibilité aux paramètres :** Ses performances dépendent fortement d'un réglage minutieux en amont (le choix du noyau et la gestion des erreurs mathématiques).