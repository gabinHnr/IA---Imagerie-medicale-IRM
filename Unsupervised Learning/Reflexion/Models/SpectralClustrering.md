# Analyse et réflexion derrière le modèle SpectralClustering

## Fonctionnement de SpectralClustering

Le modèle SpectralClustering est un modèle de clustering qui va chercher à regrouper les témoignages selon leurs similarités, contrairement à KMeans, il ne se base pas directement sur la distance entre un point et un centroïde, il va plutôt analyser les relations entre les différents points afin de créer des groupes de points fortement liés entre eux.

## Raisonnement

Pour utiliser ce modèle, nous devons comme pour KMeans transformer nos textes en données numériques avec un `TfidfVectorizer`, une fois nos vecteurs obtenus, nous allons tester plusieurs nombres de clusters, de 2 à 49.

Pour comparer les résultats, nous utilisons le `silhouette_score`, nous testons ensuite différentes valeurs de `n_init` avec le meilleur nombre de clusters afin de rechercher une configuration donnant un meilleur résultat.

## Analyse

Après avoir réalisé les différents tests, nous récupérons le nombre de clusters ayant obtenu le meilleur `silhouette_score`, nous utilisons ensuite cette valeur ainsi que la meilleure valeur de `n_init` pour entraîner notre modèle final.

Comme pour KMeans, le score de silhouette permet de voir si les clusters sont suffisamment séparés.

Nous utilisons également une PCA afin de réduire nos vecteurs TF-IDF à 3 dimensions et pouvoir représenter les résultats dans un graphique 3D, le graphique permet de visualiser la répartition des témoignages dans les différents clusters.

## Conclusion

En conclusion, SpectralClustering permet de regrouper les témoignages en analysant les relations entre les différents points.

Le `silhouette_score` nous permet de comparer les différentes configurations et de sélectionner celle qui correspond le mieux à nos tests.

La PCA permet ensuite de visualiser les résultats en 3D, même si les données originales possèdent plus de dimensions.