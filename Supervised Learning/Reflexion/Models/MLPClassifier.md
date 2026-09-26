# Le modèle MLPClassifier (Perceptron Multicouche)

## Principe de fonctionnement
Le MLPClassifier est un algorithme fondé sur l'architecture des réseaux de neurones artificiels. Contrairement à la Régression Logistique qui est contrainte par des géométries rigides, le MLP excelle dans la modélisation de frontières de décision hautement non-linéaires.

Concrètement, le modèle fait passer les milliers de pixels de chaque IRM à travers plusieurs "couches cachées" successives. Chaque couche agit comme un filtre qui apprend des caractéristiques de plus en plus complexes et abstraites (des simples variations de contraste jusqu'aux structures anatomiques complètes). En s'appuyant sur ces combinaisons, la dernière couche du réseau détermine avec précision à quelle maladie appartient l'image parmi nos 4 classes.

## Avantages
* **Apprentissage profond des caractéristiques :** Sa capacité à modéliser des relations mathématiques très complexes lui permet de distinguer finement des maladies dont les manifestations visuelles se superposent fortement (comme pour nos maladies 1 et 2).
* **Adaptabilité architecturale :** Le nombre de couches et de neurones (ex: 256, 128, 64) peut être ajusté sur-mesure pour correspondre exactement à la difficulté de notre jeu de données.

## Inconvénients
* **Risque de surapprentissage (Overfitting) :** En raison de son immense quantité de paramètres internes (les poids neuronaux), le modèle peut avoir tendance à apprendre les images d'entraînement par cœur plutôt que de comprendre la maladie, surtout si le volume de données est restreint.
* **Coût matériel et temporel :** Les milliers d'allers-retours nécessaires pour corriger ses erreurs (rétropropagation) rendent son entraînement lourd et particulièrement long.
* **Effet "Boîte Noire" :** Il est presque impossible de retracer et d'expliquer cliniquement à un médecin pourquoi le réseau de neurones a pris une décision spécifique, contrairement à un modèle statistique classique.