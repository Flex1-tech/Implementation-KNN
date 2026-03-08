
# K-Nearest Neighbors (KNN) – Implémentation en Python

[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

---

## Description

Ce projet propose une **implémentation de l’algorithme K-Nearest Neighbors (KNN)** en Python en utilisant principalement la bibliothèque **NumPy**.

L’objectif est de construire une version personnalisée de l’algorithme permettant de résoudre à la fois des **problèmes de classification** et de **régression**, tout en supportant plusieurs **métriques de distance**.

L’implémentation a ensuite été **comparée avec celle de la bibliothèque `scikit-learn`** afin de vérifier la cohérence des résultats.

---

## Fonctionnalités

L’implémentation inclut :

* Support des **problèmes de classification**
* Support des **problèmes de régression**
* Plusieurs **métriques de distance**
* Gestion de la **distance de Mahalanobis**
* Vérification de la **stabilité de la matrice de covariance**
* **Régularisation** en cas de matrice non inversible

---

## Métriques de distance supportées

Les distances suivantes sont disponibles :

* **Euclidean**
* **Manhattan**
* **Cosine**
* **Minkowski**
* **Hamming**
* **Jaccard**
* **Mahalanobis**

La distance de **Minkowski** utilise un paramètre (p) configurable (par défaut (p = 2), correspondant à la distance euclidienne).

---

## Structure de la classe

La classe principale est `KNN` et comprend les méthodes suivantes :

### `__init__(k, metric, pb, p=2)`

Initialise les paramètres du modèle :

* `k` : nombre de voisins
* `metric` : métrique de distance utilisée
* `pb` : type de problème (`"class"` ou `"reg"`)
* `p` : paramètre de la distance Minkowski

---

### `fit(x_train, y_train)`

Cette méthode :

* stocke les **données d’entraînement**
* calcule la **matrice de covariance** si la distance Mahalanobis est utilisée
* vérifie la **stabilité de la matrice** via ses valeurs propres
* applique une **régularisation** si nécessaire pour permettre l’inversion de la matrice.

---

### `distance(x1, x2)`

Calcule la distance entre deux points selon la **métrique sélectionnée**.

---

### `predict(X_pred)`

Prédit les sorties pour de nouvelles observations :

1. Calcul des distances entre l’observation et les données d’entraînement
2. Sélection des **k plus proches voisins**
3. Prédiction :

* **vote majoritaire** pour la classification
* **moyenne des valeurs** pour la régression

---

## Exemple d’utilisation

```python
import numpy as np

knn = KNN(k=5, metric="euclidean", pb="class")

knn.fit(X_train, y_train)

predictions = knn.predict(X_test)
```

---

## Validation

L’implémentation a été testée sur un **dataset réel** et comparée avec l’algorithme **KNN de scikit-learn**.

Les résultats obtenus montrent des **performances globalement similaires**, ce qui confirme la validité de l’implémentation.

---

## Bibliothèques utilisées

* **NumPy**
* **collections.Counter**

---

## Améliorations possibles

Plusieurs améliorations peuvent être envisagées :

* vectorisation complète du calcul des distances
* optimisation des performances pour les grands datasets
* ajout d’une **pondération des voisins**
* ajout d’une **normalisation automatique des données**
