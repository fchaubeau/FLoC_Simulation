# FLoC_Simulation

## Objectifs 
Reprendre la simulation de FLoC mise en place sur la base du jeu de données MovieLens mais en faisant une observation plus orientée vie privée et pas performance des recommandations. 

## Principe de la simulation google
On a les données de MovieLens qui donnent les notes que des utilisateurs ont donné à des films et les catégories associées à ces films. Pour chaque avis d’un utilisateur sur un film, on crée un vecteur v dont la coordonnée vi est le poids de la catégorie i pour ce film. On multiplie ensuite toutes les valeurs par la note que l’utilisateur a donné au film. On fait ensuite la moyenne de tous les vecteurs pour un utilisateur donné et on obtient un vecteur par utilisateur. On applique ensuite l’algorithme simHash aux différents vecteurs afin d’avoir le cohortId de chaque utilisateur.

## Adaptation de la simulation google à notre besoin
On va reprendre la même simulation à un détail près : on va générer des cohortId sur plusieurs périodes de temps. On pourrait chercher à le faire sur 7 jours, mais on manque d’informations quant à la répartition dans le temps des données, et on risquerait de se retrouver avec des utilisateurs ayant parfois une seule note sur 7 jours, voire pas de notes du tout. On se contentera donc de séparer le jeu de données en 2, avec d’un côté toutes les données dont la date est antérieure à la date médiane des notes et de l’autre côté, toutes les données dont la date est postérieure. Ainsi on pourra avoir 2 cohortId, parfois distincts, parfois identiques par utilisateur.

## Mesures sur notre simulation
Nous allons tout d’abord mesurer le nombre de cas où le couple [cohortIdPeriode1, cohortIdPeriod2] est unique par rapport au nombre total d’utilisateurs ainsi que le nombre de cas où il ne concerne que peu d’utilisateurs (<5).
Pour les personnes qui ont un couple de cohortIds unique, nous allons chercher à en apprendre plus sur les différentes cohortes par lesquelles l’utilisateur est passé et voir si cela permet d’en apprendre plus sur l’utilisateur (cette observation devra se faire de manière plutôt qualitative en s’appuyant sur des exemples précis d’utilisateurs). 
