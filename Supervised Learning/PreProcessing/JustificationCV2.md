# Justification de l'utilisation de la bibliothèque cv2

## Qu'est-ce que cv2 ?

cv2 est une bibliothèque Python qui permet de manipuler des images (traitement d'images et vision par ordinateur). C'est l'une des bibliothèques les plus connues pour utiliser OpenCV en Python.

Ses utilités principales sont les suivantes :

    Modifier la taille (Redimensionnement) : Permet simplement, avec quelques commandes, de redimensionner une image proprement.

    Manipuler les couches de couleur : cv2 permet d'analyser, de modifier et de changer les couches de couleurs qui constituent une image (Attention : cv2 ne prend pas du RGB par défaut, mais du BGR).

    Rogner (Cropping) : Une image peut être coupée ou raccourcie, mais on peut également sélectionner une partie précise à garder.

Ce sont les grandes utilisations de base de cv2.

## Utilisation dans le projet

Pour le projet, nous utilisons donc deux de ces trois grandes capacités.

Tout d'abord, nous utilisons la modification de taille. On passe dans chaque image de notre dataset et on la redimensionne avec la bonne taille, tout en gardant les proportions.

Ensuite, nous utilisons la manipulation de couleur pour passer toutes les images en niveaux de gris avec cv2.cvtColor(img, cv2.COLOR_BGR2GRAY). Nous faisons cela pour éviter de se retrouver avec des images qui ont 3 canaux de couleur (RGB) et certaines images avec 1 seul canal de gris. Les scanners du domaine médical ne sortent normalement que des images avec un seul canal de gris.

Pour le projet, nous avons besoin de stocker ces données sous forme de np.array. Pour cela, pas besoin de faire de conversion supplémentaire plus bas : les fonctions comme cv2.cvtColor ou cv2.imread permettent automatiquement de récupérer un tableau qui est exactement un np.array.

Nous appliquons également un .flatten() à ce tableau pour obtenir une liste à 1 dimension (plutôt que d'avoir une ligne de pixels par ligne, on prend la deuxième ligne de l'image et on la colle après la première, et ainsi de suite).

### À part pour ces deux utilisations, nous n'utilisons pas cv2 pour autre chose.


Librairie autorisé par Jayce.