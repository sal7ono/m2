# Intro

On va bosser sur la Big data, Python, Hadoop, Spark

Objectif principal : améliorer les performances. 

# Big Data

## Réviser Big data

Les données sont représentées comme un réseau : connexions entre points.

On peut avoir une liste de clients, il n'y a pas de relations entre eux. Mais on peut les foutre sur un graphique et tirer de l'information, par exemple à partir de l'espace entre les points. 

On a donc un réseau à comprendre et dont on doit tirer de l'information. Exemple de Google PageRank : chaque node est un website, et il y a des liens entre les sites > réseau. Un site avec beaucoup de liens vers lui sera plus important  qu'un avec moins. 

## 1.2 - Modélisation des réseaux

$$
C_T = ( V, E)
$$

Où V est un jeu de noeuds et E un jeu de relations

On modélise les noeuds et les relations comme sur le PDF

Ça peut être dirigé ou non  : dirigé on a un sens dans le réseau, c'est le cas du PageRank.  On peut aussi avoir du poids sur les réseaux (graphe pondéré)

Réseau est un terme technique, graph un terme pratique pour représenter la même chose

On réprésente V = {a, b, c, d, e} et E = {ab, bd, bc, cd}

d la distribution des degrès des noeuds. d : {1,2, 2,1,2} . 

d(b) = somme du poids total des relations

$d^+(b) =$  nombre de relations sortantes de b (=2)

$d^-(b) =$ nombre de relations entrantes vers b (=1)



Composants connectés  : Si on peut aller de a vers b, alors a et b appartiennent au même composant connecté. 

Composants fortement connectés (SCC) :  depuis n'importe quel point on peut aller vers un autre. Toutes les directions existent. 

Entre deux SCC, un noeud/SCC vers lequel un SCC de référence se dirige est un out-compoment. À l'inverse, si il se dirige vers le SCC de référence c'est un in-component

À partir des graphes on génère des matrices (voir pdf), on peut compter le nombre de connexions entre les points et tout et tout. Dans un truc non dirigé, M[a,b] = M[b,a]. Si on a une relation M(a,b) = 1, sinon 0. Dans un graph pondéré, M[a,b] = le poids de la relation.

coût : n²

Liste des relations : n*degré moyen (a peu égal à log(n))

Si on a pas le réseau (donc la totalité des données), on va générer un réseau artificel, similaire au réseau réel. Trois méthodes communes qu'on va aborder rapidement.

On connait le nombre de noeuds (1000), pas toutes les relations. On peut étalir le réseau à partir de la probabilité d'avoir une relation entre un noeud et un autre. p.e, chaque nœud a environ 20 connexion. 
$$
degre_a \approx p*n = \frac{20}{1000}*1000 = 20
$$


P : probabilité
$$
P(ab\ is \ an \ edge) \approx Bern(p)  \\
P(degre\ of\ a) \approx Binom(p*n) \approx poisson\ law
$$
Le fait que la plupart des noeuds aient un degrés proche de p*n n'est pas correct dans la réalité. Ces réseaux ne sont donc pas corrects dans la réalité, mais utiles. 

### Réseaux sans échelle

n : nombre de noeuds

$\lambda$ : power parameter ($2 \leqslant \lambda \leqslant 3$)
$$
Nb\ edge = \sum_adegre(a) \\
= \sum i*\frac{n(\lambda-1)}{\lambda^{i+1}}
$$

### Réseaux petit monde 

Les noeuds ne s'atteingnant pas directement, mais sont à une très faible distance les uns des autres (genre moins de 6 étapes pour aller de a vers b)

## Analyse des modèles : Google page Rank

Problématique du spam de mot clef contournée grace au système de PageRank qui donne de l'importance à la page, indépendamment du nombre du mots-clefs.

L'importance du site et donc la probabilité qu'on veuille aller sur celui là se calcule à partir d'une matrice. De cette matrice, on divise toutes les valeurs 1 de sorte à ce que chaque colonne fasse un total de 1.

|      | a    | b    | c    | d    | e    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| a    | 0    | 1    | 1    | 0    | 0    |
| b    | 0    | 0    | 0    | 1    | 0    |
| c    | 1    | 1    | 0    | 0    | 0    |
| d    | 0    | 0    | 0    | 0    | 1    |
| e    | 0    | 0    | 0    | 1    | 0    |

devient

|      | a    | b             | c    | d             | e    |
| ---- | ---- | ------------- | ---- | ------------- | ---- |
| a    | 0    | $\frac{1}{2}$ | 1    | 0             | 0    |
| b    | 0    | 0             | 0    | $\frac{1}{2}$ | 0    |
| c    | 1    | $\frac{1}{2}$ | 0    | 0             | 0    |
| d    | 0    | 0             | 0    | 0             | 1    |
| e    | 0    | 0             | 0    | $\frac{1}{2}$ | 0    |

on obtient une matrice conditionnelle. Chaque ligne est 1/5, on fait la somme en fractions de la ligne et on a la matrice. La somme des éléments de la matrice donne 1. 

Une affaire de V ensuite. $V_0$ est la probabilité d'accéder à un point depuis n'importe  quel point de départ. 



## TP: Python pour Data Science

Installer Anaconda

Copier la database soccer et la metttre dans le dossier "python"

Finir TP 0 et 1