# Analyse et reflexion derriere le model DBSCAN

## Fonctionnement de DBSCAN
Le model DBSCAN est un model de clustering (regroupement en cluster), il va donc se servir de upsilone pour faire des zone autour de point (nos temoignage qu'on a vectorise).
Tout autre point dans cette zone appartient donc au meme cluster.
Pour placer ces points le model se sert de la distance entre deux points.

## Raisonnement
Pour ce model nous avons donc du faire un `TfidfVectorizer`, c'est a dire vectoriser nos texts en utilisant Tfidf qui se base sur els recurrence et garde une proportion.

Une fois en possession de nos vecteur on va donc entrainer le model.
Deux parametres sont essentiel:
    - eps
    - min_samples

Nous allons donc modifier ces parametres pour relaiser de multiple test et avoir une plage de resultat plus important.

Pour mesurer notre model et surtout savoir si notre valeur est bonne on va utiliser le `silhouette_score`, un indicateur de cluster qui va permettre d'avoir un core compris entre -1 et 1.
PLus ce score tend vers 1 plus le resultat est pertinent.

## Analyse
Apres avoir realiser la fonction et la boucle avec les valeurs des parametres qui changent on obtiens un premier resultat.
On Obtiens enorment de reponse avce 0 cluster et 1010 points de bruit.
Seul quelque `silhouette_score` ressortent mais sont proches de 0.

Apres quelques ajustement des parametres les resultats restent toujours proches de 0.

Pour comprnedre precisement le probleme nous allons regarder les repartitions dans les clusters.
On ajoute :
```
 valeurs, comptes = np.unique(labels, return_counts=True)
        print("Répartition des clusters :")
        for val, compte in zip(valeurs, comptes):
            print(f"Cluster {val} : {compte} points")
```

En ajoutant ces test on comprend le probleme, l'effet de chaine (Chaining effect).

L'effet de chaining est assez simple, un cluster prend le dessus sur les autres. C'est a dire que plus de 80% des points vont se retrouver dedans car DBSCAN place les points comme un system de pont.
Le point A et B sont proche donc dans le meme cluster, le point C est proche de B mais a cause du system il se retrouve aussi proche de A, et ainsi de suite. A la fin on se retrouve avec enormement de points dans le meme cluster car proche les un des autres comme un pont.


## Conclusion
En conclusion, le model DBSCAN n'est pas adapte par notre cas d'usage. Nous retomberont toujours sur cette effet de chaine.