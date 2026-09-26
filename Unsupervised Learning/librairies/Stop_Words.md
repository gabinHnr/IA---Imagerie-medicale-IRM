# Justification de la librairie Stop_Words

## Principe
La librairie `stop_words` fournit des listes de "mots vides" (ou mots-outils). Il s'agit des mots extrêmement fréquents dans le langage courant (comme *le, et, de, the, is*) qui servent à construire des phrases mais ne portent aucune signification sémantique forte ou pertinente pour une analyse thématique.

## Utilité dans le projet
Dans ce projet, cette librairie est utilisée exclusivement lors de l'étape de visualisation des données. Elle nous permet de filtrer ces mots parasites avant de générer nos graphiques. Sans ce filtre, les graphiques de fréquences seraient saturés par ces mots majoritaires, ce qui masquerait totalement le vocabulaire médical et les symptômes qui nous intéressent réellement.

## Cohérence avec le modèle
Ce filtrage visuel ne fausse en rien notre analyse. Au contraire, il est le reflet exact de notre pipeline d'apprentissage : lors de la phase d'entraînement, notre `TfidfVectorizer` exclut nativement ces mêmes *stop words*. Le graphique illustre donc fidèlement la matière première sur laquelle nos algorithmes (comme le KMeans ou le Spectral Clustering) se basent réellement pour regrouper les patients.

*(Note : Librairie explicitement autorisée par Jayce pour ce projet).*