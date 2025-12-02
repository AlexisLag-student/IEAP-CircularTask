# README - `CircularTask.ipynb`

## Analyse de la Tâche Circulaire Ciblée

Ce **Jupyter Notebook** (`CircularTask.ipynb`) est dédié à l'analyse des données issues d'une expérience de pointage appelée **Tâche Circulaire Ciblée** (`CircularTarget`), souvent utilisée pour étudier les performances motrices dans le cadre de la **Loi de Fitts**.

| Information | Détails |
| :--- | :--- |
| **Auteurs** | Antoine Lescarboura & Alexis Lagarde |
| **Date de l'analyse** | 02 Décembre 2025 |
| **Logiciel d'acquisition des données** | LSL-mouse, version 1.2.0rc5 |

***

## Prérequis

Pour exécuter ce Notebook, vous devez disposer d'un environnement Python avec les bibliothèques suivantes installées :

* `numpy` (pour les calculs numériques)
* `matplotlib.pyplot` (pour la visualisation des données)
* `os` (pour les opérations sur les chemins de fichiers)
* `IPython.display` (pour l'affichage dans l'environnement Jupyter)

Le Notebook utilise la commande magique `%matplotlib widget` pour activer des **graphiques interactifs et zoomables**.

***

## Structure des Données

L'analyse suppose que les fichiers de données brutes se trouvent dans un sous-répertoire nommé `./data/`.

### 1. Fichier de Données Brutes

**`001MoDe_R1.csv`**

Ce fichier contient les données d'échantillonnage point par point, y compris :

* **Horodatages** (`timestamp`)
* **Coordonnées de la souris** (`mouseX`, `mouseY`)
* **État du curseur** (`mouseInTarget`: booléen indiquant si le curseur est dans la zone cible).

Il inclut également des **métadonnées cruciales** dans son en-tête pour la configuration de la tâche, telles que :

* `centerX`, `centerY`: Centre de la zone de tâche.
* `externalRadius`, `internalRadius`: Rayons de la cible.
* `taskRadius`: Rayon de la tâche.
* `indexOfDifficulty`: L'**Indice de Difficulté (ID)** théorique calculé (ex: `28.007 bits`).

### 2. Fichier des Marqueurs d'Événements

**`001MoDe_R1.marker.csv`**

Ce fichier contient les marqueurs temporels qui délimitent les événements de l'expérience. Les marqueurs clés sont :

* `DoRecord` et `DoPause`: Utilisés pour identifier le début et la fin de chaque période d'enregistrement (cycle).
* Statistiques récapitulatives de performance pour chaque essai.

***

## Processus d'Analyse

Le Notebook effectue une analyse de la performance motrice, inspirée de la **Loi de Fitts** appliquée à un mouvement circulaire.

1.  Chargement des Données : Les fichiers CSV de données et de marqueurs sont chargés en mémoire.
2.  Segmentation des Cycles : Les marqueurs `DoRecord` et `DoPause` sont utilisés pour découper le flux de données brutes en segments d'enregistrement distincts (cycles, généralement de 20 secondes chacun).
3.  Calcul des Métriques de Performance :
    * La fonction `evaluate_cycle` est le cœur de l'analyse, calculant les métriques pour chaque cycle.
    * Les métriques calculées incluent :
        * **Nombre de tours** (`laps`)
        * **Temps de Mouvement Moyen par tour** (`MT/lap`)
        * **Rayon effectif** (`Re`) et **Tolérance effective** (`Te`)
        * **Pourcentage d'erreur** (`error`)
        * **Indice de Difficulté effectif par tour** (`IDe/lap`)
        * **Débit d'Information (Throughput)** (`IPe` en bits/s)
    * Les résultats (ex: **Rec001** à **Rec005**) sont affichés et comparés aux valeurs théoriques.
4.  Visualisation des données :
    Le Notebook génère des figures pour chaque cycle, qui affichent :
    * Le **tracé 2D** de la trajectoire de la souris dans le plan (x, y).
    * L'**évolution des coordonnées** (x et y) en fonction du temps.
    
    
    
    
    
    
    
    
    