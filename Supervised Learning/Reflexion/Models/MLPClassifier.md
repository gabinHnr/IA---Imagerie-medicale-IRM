Le modèle de MLPClassifier est un algorithme basé sur un réseau de neurones. Contrairement à la LogisticRegression, il peut créer des frontières de décision non linéaires.

Globalement, le modèle fait passer les milliers de pixels de chaque image à travers plusieurs couches de neurones. Chaque couche apprend progressivement des caractéristiques de plus en plus complexes afin de déterminer à quelle maladie l'image appartient parmi nos 4 classes.

Sa principale force est donc de pouvoir apprendre des relations complexes entre les pixels, ce qui lui permet de mieux séparer des maladies dont les images se ressemblent.

Cependant, cette complexité est aussi une faiblesse : le modèle possède beaucoup de paramètres, ce qui peut rendre son entraînement plus long et provoquer du surapprentissage s'il n'y a pas assez de données.