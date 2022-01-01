### MAINTENANCE PREDICTIVE 
La maintenance prédictive pour l'industrie 4.0 est une méthode de prévention des pannes des machines par l'analyse des données qui consiste à développer des modèles de Machine Learning capable de  prévoir les pannes avant qu'ils ne se produisent

### DONNEES DESEQUILIBREES
Ce problème de données déséquilibrés et rencontré souvent dans le secteur bancaire, médical ou encore en maintenance prédictive… le risque d'entrainer un modèle avec ce genre de données est de biaiser le modèle est donc de prédire beaucoup de faux négatif.

Je présente ici quelques techniques qu'on peut utiliser pour résoudre ce problème. Ces différents techniques sont explorées dans le cadre d'un exemple de maintenance prédictive.
Les données sont chargées depuis kaggle : Machine Predictive Maintenance Classification | Kaggle


clf name	clf accuracy	clf recall	clf precision	clf f1_score
11	XGBClassifier	0.9825	0.989594	0.976051	0.982776
3	KNeighborsClassifier	0.9515	0.989098	0.920664	0.953655
6	RandomForestClassifier	0.973	0.986125	0.961353	0.973581
0	StackingClassifier	0.96	0.972745	0.949226	0.960842
8	GradientBoostingClassifier	0.944	0.969772	0.923113	0.945868
7	AdaBoostClassifier	0.96125	0.968781	0.955056	0.96187
5	DecisionTreeClassifier	0.95925	0.967294	0.95266	0.959921
9	MLPClassifier	0.93575	0.956392	0.919485	0.937576
4	SVC	0.92975	0.955897	0.909477	0.932109
1	LogisticRegression	0.82725	0.828543	0.828954	0.828748
2	LinearDiscriminantAnalysis	0.825	0.822597	0.829171	0.825871
10	SGDClassifier	0.832	0.801784	0.856085	0.828045
