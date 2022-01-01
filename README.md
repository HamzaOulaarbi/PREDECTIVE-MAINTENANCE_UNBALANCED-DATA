# MAINTENANCE PREDICTIVE 
La maintenance prédictive pour l'industrie 4.0 est une méthode de prévention des pannes des machines par l'analyse des données qui consiste à développer des modèles de Machine Learning capable de  prévoir les pannes avant qu'ils ne se produisent
# Choix de la métrique: 
Dans notre exemple on s'intéresse particulièrement à la classe positif de panne. l'objectif étant de minimiser les faux négatifs (les pannes non detectées) nous allons donc contrôler principalement la métrique rappel 'Recall' 
# DONNEES DESEQUILIBREES
Ce problème de données déséquilibrés et rencontré souvent dans le secteur bancaire, médical ou encore en maintenance prédictive… le risque d'entrainer un modèle avec ce genre de données est de biaiser le modèle est donc de prédire beaucoup de faux négatif.

Je présente ici quelques techniques qu'on peut utiliser pour résoudre ce problème. Ces différents techniques sont explorées dans le cadre d'un exemple de maintenance prédictive.
Les données sont chargées depuis kaggle : Machine Predictive Maintenance Classification | Kaggle

