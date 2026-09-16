# Analyse et réflexion derrière le modèle DBSCAN

## Fonctionnement de DBSCAN
Le modèle DBSCAN est un modèle de clustering (regroupement en cluster), il va donc se servir de upsilon pour faire des zones autour de points (nos témoignages qu'on a vectorise).
Tout autre point dans cette zone appartient donc au même cluster.
Pour placer ces points, le modèle se sert de la distance entre deux points.

## Raisonnement
Pour ce modèle, nous avons donc dû faire un `TfidfVectorizer`, c’est-à-dire vectoriser nos textes en utilisant Tfidf qui se base sur les récurrence et garde une proportion.

Une fois en possession de nos vecteurs, on va donc entraîner le modèle.
Deux paramètres sont essentiels:
    - Eps
    - min_samples

Nous allons donc modifier ces paramètres pour réaliser de multiples tests et avoir une plage de résultats plus importante.

Pour mesurer notre modèle et surtout savoir si notre valeur est bonne, on va utiliser le `silhouette_score`, un indicateur de cluster qui va permettre d'avoir un core compris entre -1 et 1.
Plus ce score tend vers 1, plus le résultat est pertinent.

## Analyse
Après avoir réalisé la fonction et la boucle avec les valeurs des paramètres qui changent, on obtient un premier résultat.
On obtient énormément de réponses avec 0 cluster et 1010 points de bruit.
Seuls quelques 'silhouette_score' ressortent mais sont proches de 0.

Après quelques ajustements des paramètres, les résultats restent toujours proches de 0.

Pour comprendre précisément le problème, nous allons regarder les répartitions dans les clusters.
On ajoute :
```
 valeurs, comptes = np.unique(labels, return_counts=True)
        print("Répartition des clusters :")
        for val, compte in zip(valeurs, comptes):
            print(f"Cluster {val} : {compte} points")
```

En ajoutant ces tests, on comprend le problème, l'effet de chaîne (Chaining effect).

L'effet de chaining est assez simple, un cluster prend le dessus sur les autres. C’est-à-dire que plus de 80% des points vont se retrouver dedans car DBSCAN place les points comme un système de pont.
Le point A et B sont proches donc dans le même cluster, le point C est proche de B mais à cause du système il se retrouve aussi proche de A, et ainsi de suite. A la fin, on se retrouve avec énormément de points dans le même cluster car proches les uns des autres comme un pont.


## Conclusion
En conclusion, le modèle DBSCAN n'est pas adapté à notre cas d'usage. Nous retomberons toujours sur cet effet de chaîne.


## Autre point
Le modèle DBSCAN ne possède pas de loss fonction dû au fait qu'il est simplement un modèle qui applique des règles mathématiques, il ne fait pas de système de fausse réponse et minimise son équation