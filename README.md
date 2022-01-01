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
#### 1.a Sous-échantillonnage aléatoire
Sous-échantillonnage pour réduire la taille de la classe majoritaire et atténuer le déséquilibre. Le choix des points à retirer se fait de manière aléatoire.
####1.b Sous-échantillonnage avec la méthode NearMiss
NearMiss Consiste à rééchantillonner la classe majoritaire en utilisant les méthodes de voisinage proche afin de ne pas perdre l'information (l'utilité des exemples pour déterminer les limites de décision au sein des différentes classes).
Les trois  versions de NearMiss 
- NearMiss-1(version=1) :  sélectionne les échantillons positifs pour lesquels la distance moyenne aux N échantillons les plus proches de la classe négative est la plus petite.
- NearMiss-2 (version=2) sélectionne les échantillons positifs pour lesquels la distance moyenne aux N échantillons les plus éloignés de la classe négative est la plus petite.
- NearMiss-3 (version=3)  est un algorithme en 2 étapes. D'abord, pour chaque échantillon négatif, les M plus proches voisins sont conservés. Ensuite, les échantillons positifs sélectionnés sont ceux pour lesquels la distance moyenne aux N plus proches voisins est la plus grande.
### 2. Sur-Echantillonnage 
Les techniques de sur-échantillonnage sont utilisées lorsqu'on a un Dataset pas très grand. On peut sur-échantillonner les observations de la classe minoritaire en générant des échantillons par répétition de façon aléatoire ou en utilisant des méthodes comme SMOTE ou ADASYN  qui génèrent des nouveaux échantillons par interpolation : 
#### 2.a. SMOTE ( Synthetic Minority Over-Sampling Technique)  
Consiste à sur-échantillonner en se basant sur les proches voisins de la classe minoritaire.
	• On choisit une observation de la classe minoritaire et on sélectionne aléatoirement un de ses proches voisins appartenant à la même classe en utilisant la distance euclidienne.
	• Ensuite, on calcule la différence pour chaque feature et on la multiplie par un nombre aléatoire entre 0 et 1.
	• Finalement, on ajoute le résultat à l’observation choisie pour obtenir un nouveau point
les faiblesses de la SMOTE :
- Ne prend pas en compte les exemples voisins pouvant provenir de la classe majoritaire.
- Risque de générer du bruit supplémentaire dans le jeu de données, ce qui pourrait éventuellement biaiser le modèle. 
#### 2.b. ADASYN (ADAptive SYNthetic :
Comme la SMOTE génèrent de nouveaux échantillons par interpolation. Cependant, les échantillons utilisés pour interpoler/générer de nouveaux échantillons synthétiques diffèrent.  En fait, ADASYN se concentre sur la génération d'échantillons à côté des échantillons originaux qui sont mal classés à l'aide d'un classificateur de k-voisins les plus proches (KNN), tandis que l'implémentation de base de SMOTE ne fera aucune distinction entre les échantillons à classer à l'aide de la règle des voisins les plus proches.
### 3. Combinaison de SMOTE et NearMiss
la combinaison du sur-échantillonnage et du sous-échantillonnage peut aussi apporter des meilleurs performances.
## Apprentissage sensible aux coûts (scale_pos_weight / class_weight) :
C’est un type d’apprentissage qui prend en compte les coûts d’une mauvaise classification (de la classe minoritaire).
Au cour de l’apprentissage, on peut attribuer des poids aux observations. le poids de des observations  la classe minoritaire sera plus important. Le principe est de redéfinir la fonction de coût du modèle en tenant compte de ces poids.
Cela est possible en configurant les paramètres suivants
    - scale_pos_weight  => pour les modèle de boosting  XGBClassifier, Light GBM, Catboost ..
        => recommandation pour le scale_pos_weight = le ratio des observations négatives par rapport aux positives.
    - class_weight => pour les autres modèles 


