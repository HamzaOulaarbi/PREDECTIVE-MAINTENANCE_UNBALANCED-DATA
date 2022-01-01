### MAINTENANCE PREDICTIVE 
La maintenance prédictive pour l'industrie 4.0 est une méthode de prévention des pannes des machines par l'analyse des données qui consiste à développer des modèles de Machine Learning capable de  prévoir les pannes avant qu'ils ne se produisent

### DONNEES DESEQUILIBREES
Ce problème de données déséquilibrés et rencontré souvent dans le secteur bancaire, médical ou encore en maintenance prédictive… le risque d'entrainer un modèle avec ce genre de données est de biaiser le modèle est donc de prédire beaucoup de faux négatif.

Je présente ici quelques techniques qu'on peut utiliser pour résoudre ce problème. Ces différents techniques sont explorées dans le cadre d'un exemple de maintenance prédictive.
Les données sont chargées depuis kaggle : Machine Predictive Maintenance Classification | Kaggle


Choix de la métrique: 
Dans notre exemple on s'intéresse particulièrement à la classe panne positif =1, l'objectif étant de minimiser les faux négatifs nous allons contrôler la métrique rappel 'Recall' 
![image](https://user-images.githubusercontent.com/80227876/147846613-1acbbb7c-05a6-4d5f-ac32-42dfbbb813b1.png)
