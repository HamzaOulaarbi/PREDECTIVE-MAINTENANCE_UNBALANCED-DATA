# MAINTENANCE PREDICTIVE 
La maintenance prédictive pour l'industrie 4.0 est une méthode de prévention des pannes des machines par l'analyse des données qui consiste à développer des modèles de Machine Learning capable de  prévoir les pannes avant qu'ils ne se produisent
# CHOIX DE LA METRIQUE: 
Dans notre exemple on s'intéresse particulièrement à la classe positif de panne. l'objectif étant de minimiser les faux négatifs (les pannes non detectées) nous allons donc contrôler principalement la métrique rappel 'Recall'. Le choix de la métrique est plus important lorsque les données ne sont pas équilibrées.
# DONNEES DESEQUILIBREES
Ce problème de données déséquilibrées est rencontré souvent dans le secteur bancaire, médical ou encore en maintenance prédictive… le risque d'entrainer un modèle avec ce genre de données est de biaiser le modèle est donc de prédire beaucoup de faux négatif.

Je présente ici quelques techniques qu'on peut utiliser pour résoudre ce problème. Ces différents techniques sont explorées dans le cadre d'un exemple de maintenance prédictive.
Les données sont chargées depuis kaggle : Machine Predictive Maintenance Classification | Kaggle


## Ré-échantillonnage du jeu de données

### 1. Sous-Echantillonnage
Lorsque le nombre d’observations dans le dataset est assez important, on a la possibilité de sous-échantillonner les observations associées à la classe la plus prépondérante. On peut réaliser un sous-échantillonnage de façon aléatoire mais on peut également utiliser d’autres techniques telles que NearMiss,  TomekLink…

#### Sous-échantillonnage aléatoire
Sous-échantillonnage pour réduire la taille de la classe majoritaire et atténuer le déséquilibre. Le choix des points à retirer se fait de manière aléatoire.

#### Sous-échantillonnage avec la méthode NearMiss
NearMiss Consiste à rééchantillonner la classe majoritaire en utilisant les méthodes de voisinage proche afin de ne pas perdre l'information (l'utilité des exemples pour déterminer les limites de décision au sein des différentes classes).
Les trois  versions de NearMiss 
		1. NearMiss-1(version=1) :  sélectionne les échantillons positifs pour lesquels la distance moyenne aux N échantillons les plus proches de la classe négative est la plus petite.
		2. NearMiss-2 (version=2) sélectionne les échantillons positifs pour lesquels la distance moyenne aux N échantillons les plus éloignés de la classe négative est la plus petite.
		3. NearMiss-3 (version=3)  est un algorithme en 2 étapes. D'abord, pour chaque échantillon négatif, les M plus proches voisins sont conservés. Ensuite, les échantillons positifs sélectionnés sont ceux pour lesquels la distance moyenne aux N plus proches voisins est la plus grande.

