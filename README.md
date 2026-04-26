# Projet Paris-Duchesse : Optimisation Logistique sous Contraintes

## Contexte
Ce dépôt contient notre solution pour le projet "Paris-Duchesse", réalisé dans le cadre du cours Mathematics of Data Science (M1 IDD) à l'Université Paris Dauphine - PSL.

L'Université Paris-Duchesse est un bâtiment rectangulaire composé de plusieurs ailes (A, B, C, D) qui doivent subir des rénovations successives en 5 phases. L'objectif principal de ce projet est de planifier les déménagements du personnel (réparti en 5 services : Présidence, Étudiants, Optimisation, Informatique Théorique, et Mathématiques) depuis une configuration initiale (Phase 0) vers une configuration cible (Phase 5), tout en **minimisant le nombre total de mouvements**.

## Méthodologie et Modèles Mathématiques
Pour résoudre ce problème d'affectation complexe, nous avons exploré trois approches d'optimisation :

### 1. Programmation Linéaire (LP) et LP Mixte (MILP)
* Modélisation du problème comme un flot multi-produits sur un graphe temporel.
* Intégration de contraintes de capacité des bureaux et de fermeture temporaire des ailes en rénovation.
* Implémentation d'une version MILP (Variables Binaires) pour forcer une contrainte stricte : interdire la cohabitation et le voisinage entre le service de la Présidence et l'Association Étudiante.
* Résultat : Optimum global théorique atteint à 30 mouvements.

### 2. Problème Pénalisé (Norme L1)
* Ajout d'une pénalité (avec un poids λ = 100) pour encourager le système à atteindre la configuration finale le plus tôt possible dans les phases.
* Résultat : Un compromis logistique menant à 38 mouvements réels, mais assurant une convergence plus rapide vers la cible.

### 3. Relaxation Semi-Définie Positive (SDP)
* Formulation matricielle avancée (U = uuᵀ) convertissant les variables binaires en spins {-1, 1} pour traiter de manière relâchée les exclusions mutuelles strictes.
* Utilisation de la méthode de Goemans-Williamson (arrondi aléatoire) couplée à une heuristique de réparation gloutonne guidée par les scores SDP pour corriger les contraintes couplées.
* Résultat : L'algorithme a généré 100% de solutions réalisables (sur 10 000 essais) avec une meilleure solution entière trouvée à 36 mouvements.

## Technologies Utilisées
* Langage : Python 3
* Environnement : Jupyter Notebook
* Bibliothèques : `numpy`, `cvxpy` (Solveurs utilisés : SCS, SCIP, CBC, GLPK_MI)

## Utilisation
Le code source est intégralement contenu dans le notebook Jupyter du projet.

Pour lancer le projet :
1. Clonez ce dépôt.
2. Assurez-vous d'avoir installé les dépendances requises (`pip install cvxpy numpy`).
3. Lancez Jupyter Notebook et exécutez les cellules séquentiellement pour voir les logs du solveur et l'évolution détaillée des occupations bureau par bureau, pour chaque phase de rénovation.

## Auteurs
* Magomed Tsitsiev
* Nouannapha PHICHITH
