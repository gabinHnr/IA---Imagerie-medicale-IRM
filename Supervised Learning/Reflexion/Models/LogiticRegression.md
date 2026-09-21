## LOGISTIC REGRESSION

Elle attribue un poids à chaque pixel des images puis elle fais une somme pondérée de ces poids puis elle transforme ces poids en proba en utilisant une fonction appelé sigmoïd pour transformer le score en valeur entre 0 et 1 et ensuite attrabue à la classe l'image en fonction de quelle classe à la proba la plus élevée pour cette classe.

Pour apprendre ces poids le modèle fais des prédictions puis calculs une erreur à partir des ces prédictions appélée la log loss puis il modifie ces poids pour essayer des faire de meilleurs prédiction.