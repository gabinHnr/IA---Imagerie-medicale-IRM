# Justification de la librairie OpenCV (cv2)

## Principe

OpenCV (`cv2`) est une librairie incontournable pour le traitement d'images. Elle permet de charger et de manipuler des images sous forme de matrices mathématiques (des tableaux numériques) directement exploitables par les algorithmes de Machine Learning.

## Utilité dans le projet

Dans ce projet, son utilisation est strictement utile au prétraitement de nos données visuelles (les IRM) avant leur passage dans nos modèles supervisés (Régression Logistique, SVM, MLP). Son rôle se concentre sur trois opérations fondamentales de standardisation :

* **L'acquisition des données :** L'ouverture et la lecture des fichiers images pour les traduire en pixels bruts.
* **L'uniformisation spatiale (Redimensionnement) :** Les algorithmes de Machine Learning exigent que toutes les données d'entrée possèdent rigoureusement la même forme mathématique. `cv2` nous permet de redimensionner toutes les images vers un format standard unique, quelles que soient leurs résolutions d'origine.
* **L'optimisation des canaux de couleur :** La modification des couches colorimétriques (comme le passage en niveaux de gris). En imagerie médicale, la couleur (RGB) est souvent un bruit inutile qui multiplie par trois le poids de l'image. Réduire l'IRM à un seul canal d'intensité lumineuse permet d'alléger drastiquement la charge mémoire et d'accélérer l'entraînement de nos modèles sans perdre d'information clinique.

*(Note : Librairie explicitement autorisée par Jayce pour ce projet).*