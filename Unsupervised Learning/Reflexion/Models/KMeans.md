# Clustering des témoignages médicaux

## Objectif

L'objectif de cette expérimentation est de regrouper automatiquement des témoignages médicaux présentant des caractéristiques similaires.

Comme les données sont textuelles, elles doivent d'abord être transformées en données numériques afin de pouvoir être utilisées par un algorithme de clustering.

Pour cela, j'ai utilisé la chaîne de traitement suivante :

**TF-IDF → KMeans → Silhouette Score → PCA → visualisation 3D**

---

## Préparation des données

J'ai commencé par charger le fichier Student_Clean.csv avec Pandas et récupérer la colonne contenant les témoignages.

Les valeurs manquantes ont été remplacées par des chaînes vides afin d'éviter des problèmes lors du traitement :

```python
df = pd.read_csv("../../Student_Clean.csv")
texts = df.iloc[:, 2].fillna("")
```

---

## Transformation des textes avec TF-IDF

J'ai utilisé TfidfVectorizer de Scikit-learn afin de transformer les témoignages en une représentation numérique.

```python
vectorizer = TfidfVectorizer(stop_words="english")
X = vectorizer.fit_transform(texts)
```

Le TF-IDF attribue un poids aux mots en fonction de leur importance dans chaque témoignage et dans l'ensemble des documents.

J'ai également retiré les stop words anglais afin de limiter l'influence des mots très fréquents qui apportent peu d'informations pour différencier les témoignages.

Cette transformation produit une matrice potentiellement composée de plusieurs milliers de dimensions, correspondant aux différents mots présents dans le vocabulaire.

---

## Recherche du nombre de clusters

KMeans nécessite de définir à l'avance le nombre de clusters.

J'ai donc testé différentes valeurs de K, de 2 à 49, afin de déterminer celle qui permettait d'obtenir le regroupement le plus pertinent.

### Elbow Method

J'ai d'abord essayé la Elbow Method.

Cette méthode consiste à observer l'évolution de l'inertie lorsque le nombre de clusters augmente. L'objectif est de trouver un "coude" à partir duquel ajouter des clusters apporte beaucoup moins d'amélioration.

Cependant, dans mes résultats, le coude était relativement difficile à identifier clairement.

### Silhouette Score

J'ai donc également testé le Silhouette Score pour chaque valeur de `K`.

Le Silhouette Score permet d'évaluer la qualité du regroupement en prenant en compte à la fois :

* la proximité des points avec leur propre cluster ;
* leur éloignement des autres clusters.

Le score varie entre -1 et 1. Plus il est élevé, plus les clusters sont généralement bien séparés et cohérents.

Dans mon cas, les résultats du Silhouette Score étaient plus intéressants et plus faciles à interpréter que ceux obtenus avec la Elbow Method.

J'ai donc choisi comme nombre de clusters la valeur obtenant le meilleur Silhouette Score.

```python
scores = {}

for n in range(2, 50):
    kmeans = KMeans(
        n_clusters=n,
        random_state=0,
        n_init="auto"
    )

    Y = kmeans.fit_predict(X)
    score = silhouette_score(X, Y)

    scores[f"{n}"] = score

highest_key = max(scores, key=scores.get)
```

---

## Application de KMeans

Une fois le meilleur nombre de clusters déterminé, j'ai créé le modèle KMeans final avec cette valeur :

```python
kmeans = KMeans(
    n_clusters=int(highest_key),
    random_state=0,
    n_init="auto"
)

Y = kmeans.fit_predict(X)
```

Chaque témoignage est alors associé à un cluster.

Le clustering est effectué directement sur les données TF-IDF. Les groupes sont donc construits à partir des caractéristiques textuelles des témoignages.

---

## Réduction des dimensions avec PCA

La représentation TF-IDF peut contenir un très grand nombre de dimensions.

Pour pouvoir représenter les résultats graphiquement, j'ai utilisé PCA (Principal Component Analysis) afin de réduire la représentation à trois dimensions :

```python
pca = PCA(n_components=3)
points_3d = pca.fit_transform(X_dense)
```

Cette réduction est uniquement utilisée pour la visualisation.

KMeans continue de travailler sur la représentation TF-IDF originale et complète. PCA ne réduit donc pas les données utilisées pour entraîner KMeans.

J'ai également appliqué la même transformation aux centroïdes :

```python
centroïdes_3d = pca.transform(kmeans.cluster_centers_)
```

Cela permet de représenter les centroïdes dans le même espace 3D que les témoignages.

---

## Visualisation

J'ai finalement représenté les résultats sous la forme d'un nuage de points en 3D.

Chaque point représente un témoignage et sa couleur correspond au cluster auquel il appartient.

Les centroïdes sont représentés par des X afin de pouvoir les distinguer des témoignages.

Cette représentation permet d'avoir une vision globale de la répartition des clusters.

Il faut cependant prendre en compte que cette représentation est une projection en 3D d'une représentation TF-IDF qui possède beaucoup plus de dimensions. La visualisation ne représente donc pas exactement toutes les distances présentes dans l'espace original.

---

## Résultats

Cette expérimentation m'a permis de mettre en place un système permettant de regrouper automatiquement les témoignages médicaux sans avoir besoin de définir les catégories manuellement.

La méthode utilisée est :

1. Chargement des témoignages.
2. Remplacement des valeurs manquantes.
3. Transformation des textes avec TF-IDF.
4. Test de plusieurs nombres de clusters.
5. Comparaison avec la Elbow Method.
6. Sélection du nombre de clusters à partir du meilleur Silhouette Score.
7. Entraînement du modèle KMeans final.
8. Réduction en trois dimensions avec PCA.
9. Visualisation des clusters et de leurs centroïdes.

Le Silhouette Score a finalement été privilégié à la Elbow Method, car il fournissait dans mon cas un critère plus clair pour comparer les différents nombres de clusters étant donné qu'en utilisant l'Elbow Method il n'y avait pas vraiment de "coude" sur le graphique.

## Limites

La principale limite de cette approche est que le clustering dépend fortement de la représentation TF-IDF.

Deux témoignages exprimant une idée similaire avec des mots très différents peuvent ne pas être suffisamment proches dans cet espace.

De plus, la visualisation en 3D avec PCA est une simplification de l'espace original et ne permet pas de représenter parfaitement toutes les relations entre les témoignages.

Cette première expérimentation permet néanmoins d'obtenir une première organisation automatique des témoignages et de mieux comprendre leur structure.





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
