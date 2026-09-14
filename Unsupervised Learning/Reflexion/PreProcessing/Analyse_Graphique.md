# Analyse de la fréquence des mots

## Description

Création d'un graphique représentant la fréquence d'utilisation des mots dans les témoignages médicaux du dataset.

L'objectif est d'identifier les mots les plus fréquemment utilisés dans les témoignages afin d'avoir une première vision des termes présents dans les textes.

Pour améliorer la lisibilité des résultats, les stop words en anglais ainsi que certains termes peu pertinents sont supprimés avant de calculer les fréquences.

Les 20 mots les plus fréquents sont ensuite représentés sous forme de graphique en barres avec Matplotlib.

## Technologies utilisées

* **Python**
* **Pandas** : lecture et traitement du fichier CSV
* **Matplotlib** : création du graphique
* **stop-words** : suppression des mots courants en anglais

## Fonctionnement

1. Chargement du fichier `Student_Dataset.csv`.
2. Récupération des textes contenant les témoignages médicaux.
3. Nettoyage du texte et conversion en minuscules.
4. Suppression des mots courants en anglais (stop words).
5. Suppression de quelques termes supplémentaires considérés comme peu pertinents.
6. Comptage du nombre d'occurrences de chaque mot.
7. Sélection des 20 mots les plus fréquents.
8. Création d'un graphique en barres représentant les résultats.

## Résultat

Le graphique permet de visualiser rapidement les 20 mots les plus fréquemment utilisés dans les témoignages médicaux du dataset.

Cette analyse constitue une première étape d'analyse des données textuelles et peut notamment servir à identifier les termes récurrents présents dans les témoignages afin de les regrouper en clusters.
