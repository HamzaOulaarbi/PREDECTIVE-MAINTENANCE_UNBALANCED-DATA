# MAINTENANCE PREDICTIVE 
La maintenance prédictive pour l'industrie 4.0 est une méthode de prévention des pannes des machines par l'analyse des données. Elle consiste à développer des modèles de Machine Learning capable de prévoir les pannes avant qu'ils ne se produisent
# CHOIX DE LA METRIQUE: 
Le choix de la métrique est plus important surtout lorsque les données ne sont pas équilibrées.
Dans notre exemple on va s'intéresse particulièrement à la classe positive/minoritaire (target=1). Il nous faudra donc une  métrique qui sera moins influencée par la classe majoritaire. L'objectif étant de minimiser les faux négatifs (les pannes non détectées) nous allons contrôler principalement la métrique rappel 'Recall' et ensuite le F1-score. Nous tracerons aussi la matrice de confusion pour mieux visualiser les résultats.

# DONNEES DESEQUILIBREES
Ce problème de données déséquilibrées est rencontré souvent dans le secteur bancaire, médical ou encore en maintenance prédictive… le risque d'entrainer un modèle avec ce genre de données est de biaiser le modèle et donc de prédire beaucoup de faux négatif.

Je présente ici quelques techniques qu'on peut utiliser pour résoudre ce problème. Ces différents techniques sont explorées dans le cadre d'un exemple de maintenance prédictive.
Les données sont chargées depuis kaggle : https://www.kaggle.com/shivamb/machine-predictive-maintenance-classification

## Ré-échantillonnage du jeu de données
### 1. Sous-Echantillonnage
Lorsque le nombre d’observations dans le dataset est assez important, on a la possibilité de sous-échantillonner les observations associées à la classe la plus prépondérante. On peut réaliser un sous-échantillonnage de façon aléatoire mais on peut également utiliser d’autres techniques telles que NearMiss,  TomekLink…
#### 1.a Sous-échantillonnage aléatoire
Sous-échantillonnage pour réduire la taille de la classe majoritaire et atténuer le déséquilibre. Le choix des points à retirer se fait de manière aléatoire.
#### 1.b Sous-échantillonnage avec la méthode NearMiss
NearMiss Consiste à rééchantillonner la classe majoritaire en utilisant les méthodes de voisinage proche afin de ne pas perdre l'information (l'utilité des exemples pour déterminer les limites de décision au sein des différentes classes).
Les trois  versions de NearMiss:
- NearMiss-1(version=1) :  sélectionne les échantillons majoritaires pour lesquels la distance moyenne aux N échantillons les plus proches de la classe minoritaire est la plus petite.
- NearMiss-2 (version=2) sélectionne les échantillons majoritaires pour lesquels la distance moyenne aux N échantillons les plus éloignés de la classe minoritaire est la plus petite.
- NearMiss-3 (version=3)  est un algorithme en 2 étapes. D'abord, pour chaque échantillon minoritaire, les M plus proches voisins sont conservés. Ensuite, les échantillons de la classe majoritaire sélectionnés sont ceux pour lesquels la distance moyenne aux N plus proches voisins est la plus grande.
### 2. Sur-Echantillonnage 
Les techniques de sur-échantillonnage sont utilisées lorsqu'on a un Dataset pas très grand. On peut sur-échantillonner les observations de la classe minoritaire en générant des échantillons par répétition de façon aléatoire ou en utilisant des méthodes comme SMOTE ou ADASYN  qui génèrent des nouveaux échantillons par interpolation : 
#### 2.a. SMOTE ( Synthetic Minority Over-Sampling Technique)  
Consiste à sur-échantillonner en se basant sur les proches voisins de la classe minoritaire.
	• On choisit une observation de la classe minoritaire et on sélectionne aléatoirement un de ses proches voisins appartenant à la même classe en utilisant la distance euclidienne.
	• Ensuite, on calcule la différence pour chaque feature et on la multiplie par un nombre aléatoire entre 0 et 1.
	• Finalement, on ajoute le résultat à l’observation choisie pour obtenir un nouveau point
Les faiblesses de la SMOTE :
- Ne prend pas en compte les exemples voisins pouvant provenir de la classe majoritaire.
- Risque de générer du bruit supplémentaire dans le jeu de données, ce qui pourrait éventuellement biaiser le modèle. 
#### 2.b. ADASYN (ADAptive SYNthetic :
Comme la SMOTE génèrent de nouveaux échantillons par interpolation. Cependant, les échantillons utilisés pour interpoler/générer de nouveaux échantillons synthétiques diffèrent.  En fait, ADASYN se concentre sur la génération d'échantillons à côté des échantillons originaux qui sont mal classés à l'aide d'un classificateur de k-voisins les plus proches (KNN), tandis que l'implémentation de base de SMOTE ne fera aucune distinction entre les échantillons à classer à l'aide de la règle des voisins les plus proches.
### 3. Combinaison sur-échantillonnage et  sous-échantillonnage
la combinaison du sur-échantillonnage et du sous-échantillonnage peut aussi apporter des meilleurs performances.
- Combinaison de SMOTE et Tomek links 'SMOTETomek'
## Apprentissage sensible aux coûts (scale_pos_weight / class_weight) :
C’est un type d’apprentissage qui prend en compte les coûts d’une mauvaise classification (de la classe minoritaire).
Au cour de l’apprentissage, on peut attribuer des poids aux observations. le poids des observations la classe minoritaire sera plus important. Le principe est de redéfinir la fonction de coût du modèle en tenant compte de ces poids.
Cela est possible en configurant les paramètres suivants:
- scale_pos_weight  => pour les modèles de boosting  XGBClassifier, Light GBM, Catboost ..
	- recommandation pour le scale_pos_weight = le ratio des observations négatives par rapport aux positives.
- class_weight => pour les autres modèles 

### L'ensemble learning 
Consiste à moyenner les prédictions de différents modèles. Ces modèles sont entrainés sur des sous ensembles de données constitués du même ensemble des observations minoritaire et d’un sous-ensemble des observations majoritaire ( avec à chaque fois le même ratio)
- Exemples: EasyEnsembleClassifier, BalancedBaggingClassifier,BalancedRandomForestClassifier
### Utilisation de la One-Class-Classification :
C'est un apprentissage sur un jeu de données avec une seule classe d’observations. lors du testing, on cherchera à déterminer si une nouvelle observation ressemble à la population d’observations ou si elle peut être considérée comme un outlier. Deux techniques:
- Exemple : Utilisation de la densité de probabilité pour identifier les outliers, les méthode de frontières telle que le One class SVM, IsolationForest ...

### Conclusion :
Après exploration de l'ensemble des méthodes citées ci-dessus nous constatons pour notre exemple de maintenance prédictive que :
- Toutes les techniques apportent une amélioration par rapport à l'entrainement de base
- La Combinaison'SMOTETomek' est la meilleure technique dans notre exemple de maintenance prédictive.
- Le plus important dans ce contexte est d’abord de bien choisir la métrique et ensuite de tester de nombreuses techniques avant de retenir la meilleure

![image](https://user-images.githubusercontent.com/80227876/147871729-613f4c37-8018-4ac4-bc95-bd76995cb625.png)




