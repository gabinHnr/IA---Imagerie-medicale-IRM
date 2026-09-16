# Analyse et réflexion derrière le modèle KMeans

## Fonctionnement de KMeans
Le modèle KMeans est un modèle de clustering (regroupement en clusters). Il va donc chercher à regrouper nos témoignages selon leur similarité.
Pour cela, KMeans utilise des **centroïdes**. Chaque témoignage est associé au centroïde dont il est le plus proche, le modèle déplace ensuite les centroïdes afin de réduire la distance entre les points et leur centroïde.

L'objectif est de minimiser une valeur appelée **inertie**.

## Raisonnement
Pour utiliser KMeans sur nos témoignages, nous devons d'abord transformer nos textes en données numériques, nous avons donc utilisé un `TfidfVectorizer` pour transformer les textes en vecteurs numériques.

Une fois en possession de nos vecteurs, nous allons entraîner le modèle.
Le paramètre principal est :
    - n_clusters

Nous allons donc tester plusieurs nombres de clusters, de 2 à 49, afin de comparer les résultats, pour mesurer les résultats, nous utilisons le `silhouette_score`, ce score est compris entre -1 et 1. Plus il est proche de 1, plus les clusters sont bien séparés.

Nous regardons également **l'inertie** afin d'utiliser la méthode du coude (Elbow Method).

## Analyse
Après avoir réalisé les différents tests, nous obtenons un meilleur nombre de clusters grâce au `silhouette_score`.
Cependant, le score reste relativement faible et proche de 0, cela signifie que les clusters ne sont pas très clairement séparés.

Nous avons également utilisé l'Elbow Method pour observer l'évolution de l'inertie en fonction du nombre de clusters.
Cette méthode permet de rechercher un "coude" dans le graphique afin de trouver un nombre de clusters intéressant.

Dans notre cas, les résultats du silhouette score sont plus intéressants que ceux de l'Elbow Method.
Nous avons donc choisi de nous baser principalement sur le silhouette score.

Pour visualiser les résultats, nous utilisons également une PCA afin de réduire les nombreux vecteurs TF-IDF à seulement 3 dimensions.
Nous pouvons ainsi représenter les témoignages et les centroïdes dans un graphique 3D.

## Conclusion
En conclusion, KMeans permet de regrouper nos témoignages, mais les faibles scores de silhouette montrent que les groupes ne sont pas très clairement séparés.

Le modèle peut donc être utilisé pour explorer les similarités entre les témoignages, mais il ne permet pas d'obtenir des catégories très distinctes dans notre cas.
