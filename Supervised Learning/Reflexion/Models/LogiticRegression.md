# Le modèle Logistic Regression (Régression Logistique)

## Principe de fonctionnement
La Régression Logistique est un algorithme statistique de classification linéaire. Dans le cadre de notre projet, le modèle établit une équation mathématique distincte pour chacune de nos 4 maladies. Lorsqu'on lui soumet une nouvelle IRM, il calcule un score de probabilité à travers ces 4 équations et attribue l'image à la classe ayant obtenu le pourcentage le plus élevé.

Sur le plan géométrique, pour traiter nos images constituées de milliers de pixels, l'algorithme ne trace pas de simples droites sur un graphique en 2D. Il déploie ce que l'on appelle des "hyperplans", c'est-à-dire des frontières de décision plates qui s'entrecroisent dans un espace à très haute dimension.

## Avantages
* **Rapidité et légèreté :** C'est un modèle mathématiquement simple, extrêmement rapide à entraîner et peu gourmand en puissance de calcul. Il sert de parfait modèle de référence (baseline) pour valider nos données.
* **Explicabilité transparente :** Contrairement à l'effet "boîte noire" des réseaux de neurones, on peut facilement observer le poids mathématique accordé à chaque pixel, rendant ses décisions facilement interprétables.

## Inconvénients
* **La limite de la linéarité (Rigidité géométrique) :** C'est sa faiblesse majeure. Un hyperplan reste par définition plat et rigide. Si les IRM de deux maladies se ressemblent trop et que leurs points se mélangent dans l'espace (comme pour les maladies 1 et 2), le modèle est incapable de tracer des courbes pour isoler les groupes. L'hyperplan tranchera inévitablement de manière droite dans la masse de points, ce qui génère un plafond de performance et des erreurs de classification impossibles à corriger avec cet algorithme.