# predictive-maintenance-aero
Ce dépôt contient l'implémentation d'une solution d'intelligence artificielle dédiée à l'estimation de la durée de vie restante (Remaining Useful Life - RUL) de moteurs d'avions. Ce travail s'inscrit dans une démarche de maintenance conditionnelle visant à réduire les coûts opérationnels et à accroître la sécurité.

1. Présentation du Jeu de Données
   
Le projet exploite le dataset C-MAPSS (Commercial Modular Aero-Propulsion System Simulation) fourni par la NASA. Les données simulent la dégradation de moteurs de type turboréacteur sous différentes conditions de vol et modes de défaillance.

Chaque échantillon contient :
Un identifiant d'unité (moteur).
Le nombre de cycles opérationnels.
Trois réglages opérationnels (Operational Settings).
Vingt-et-un capteurs mesurant diverses données physiques (température, pression, vitesse de rotation).

2. Environnement Technique
   
Le projet a été développé en Python sur Google Colab. Les librairies principales utilisées sont :

Pandas : Pour le nettoyage et la structuration des données temporelles.
NumPy : Pour la manipulation des matrices et les calculs statistiques.
Matplotlib & Seaborn : Pour la visualisation des courbes de dégradation et l'analyse de corrélation.
Scikit-Learn : Pour le prétraitement (Scaling) et l'implémentation des algorithmes d'apprentissage automatique.

3. Pipeline de Réalisation
   
Phase 1 : Acquisition et Analyse Exploratoire (EDA)
Importation des fichiers train_FD001.txt et test_FD001.txt.

Analyse de l'évolution des capteurs : Identification des capteurs présentant une tendance à la hausse (température d'échappement, etc.) ou à la baisse (pression à la sortie du ventilateur, etc.).

Phase 2 : Ingénierie des Données (Feature Engineering)

Création de la cible (Labeling) : Puisque le RUL n'est pas fourni directement dans les données d'entraînement, il a été calculé en soustrayant le cycle actuel du cycle de défaillance final de chaque moteur.

Sélection de variables : Suppression des colonnes dont l'écart-type est nul (capteurs constants), car elles n'apportent aucune information discriminante au modèle.

Normalisation : Utilisation du MinMaxScaler pour transformer les données entre 0 et 1, évitant ainsi que les variables à forte amplitude n'influencent démesurément les calculs de distance.

Phase 3 : Modélisation et Apprentissage

Deux modèles de régression ont été développés pour comparer les performances :

Régression Linéaire : Utilisée comme modèle de référence (Baseline) pour évaluer la linéarité de la dégradation.

Random Forest Regressor : Algorithme d'ensemble basé sur des arbres de décision, capable de capturer les relations non-linéaires complexes entre les capteurs.

Phase 4 : Évaluation des Performances

L'évaluation finale est réalisée sur l'ensemble de test en utilisant la métrique RMSE (Root Mean Square Error). Cette métrique pénalise fortement les erreurs de prédiction importantes, ce qui est crucial pour la sécurité aéronautique.
4. Résultats et AnalyseLes

résultats obtenus mettent en évidence la supériorité du modèle non-linéaire :ModèleRMSEPrécision relativeRégression Linéaire30.96MoyenneRandom Forest Regressor26.24Élevée
