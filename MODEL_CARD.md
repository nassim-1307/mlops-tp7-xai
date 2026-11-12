# Model Card - fraude (version servie par l'alias production)

## Modele
Nom et version dans le registre MLflow : fraude, version 1 (alias production)
Famille et reglages : RandomForestClassifier, n_estimators=500, max_depth=16, random_state=42
Run d'origine (MLflow) : <run_id du TP2>

## Objectif et usage prevu
Detecter les paiements potentiellement frauduleux et les signaler a une revue humaine.

## Usages exclus
Bloquer definitivement un compte ou refuser un paiement sans revue humaine ; usage sur des donnees reelles non validees.

## Donnees
Fichier data/transactions.csv, 5000 lignes, 568 fraudes (~11,4 %), empreinte md5 : <donnees_md5>
Origine des donnees : synthetiques (generees avec une graine fixe).

## Performances (jeu de test, 1 250 transactions)
F1 : 0,8669   precision : 0,8837   rappel : 0,8507   AUC : 0,9872

## Methodes d'explicabilite
Globale : importance par permutation (10 repetitions) et SHAP TreeExplainer (400 transactions).
Locale : SHAP (waterfall) et LIME (2 000 voisins, graine 0).
Variables les plus influentes : montant, puis freq_24h / anciennete / nuit.

## Comparaison avec un modele interpretable
Logistique avec log10(montant) : F1 0,8593, 113/134 fraudes detectees contre 114/134 pour la foret.

## Limites et risques connus
Donnees synthetiques ; LIME instable d'une graine a l'autre ; SHAP n'indique pas de causalite ; fraudes rares (134 dans le test) donc metriques bruitees.

## Recommandations d'utilisation et de surveillance
Revue humaine obligatoire ; surveiller la derive des variables (montant, nuit) ; reevaluer a chaque reentrainement.

## Tracabilite
Run des explications (experience tp7-explicabilite) : xai-fraude-v1, <run_id>
Auteurs : <noms> Date : <date> Prochaine revue : <date>