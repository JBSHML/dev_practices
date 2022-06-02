# Initialisation de projet: Git & Poetry :new:
## a) Initialiser un repo Git (via Github, Gitlab,...)

La méthode la plus simple est de créer un repo directement sur Github ou Gitlab (ou autre) et de le cloner sur la machine local. On ne traitera pas ici son utilisation.


<br>
<br>

## b) Initialiser un projet avec Poetry (à faire une seule fois, à la création du projet)
\
  Poetry permet d'initialiser un projet avec une structure par défaut et tous les outils nécessaires au management des packages et de dépendances.\
  Le comportement par défaut de la commande d'initialisation de projet via Poetry, est **d'utiliser l'environnement Conda dans lequel la commande est lancée**\

  1. Lancer Powershell ou CMD
  2. Se rendre dans le repo git cloné:
  ```powershell
  cd root/path/to/project/repogit
  ```
  3. Puis, dans ce repo, activer l'environnement Anaconda de votre projet via:
  ```powershell
  conda activate nom_env 
  ```
  4. Enfin, exécuter la commande qui permet d'initialiser un projet poetry
  ```powershell
  poetry new project_name 
  ```
  4. Le projet Poetry est désormais créer, avec cette arborescence:
  ```bash
  project_src
  │   pyproject.toml
  │   README.rst  
  │
  └───project_name
  │       __init__.py
  │
  └───tests
          __init__.py
          test_project_name.py
  ```
  * **pyproject.toml** : fichier des dépendances du projet. Il est possible d'ajouter les dépendances manuellement dans ce fichier (peu recommandé).\
   Dans  le cadre de bonnes pratiques, il suffit ajouter les dépendances, dans l'environnement conda du projet, via la commande:
  ```powershell 
   poetry add librairie
  ```
  * **README.rst** : Readme du projet
  * **project_name** : répertoire contenant la partie code (hors test, à adapter)
  * **test** : contient la partie test du code (à adapter)
  * *Les fichiers init servent à Python en tant que constructeurs pour les imports*

<br>
<br>

## c) Actualiser l'environnement sur machine locale sur la base d'un projet Poetry d'un repo 
\
  Une fois le projet Poetry initialisé dans un repo Git, celui travaillant dessus va pouvoir le ```commit```.

  Dès lors, à l'aide des fichiers pyproject.toml et poetry.lock, on peut actualiser notre environnement dédié au projet localement pour que celui-ci soit identique à celui qui l'a commit (s'il respecte aussi les bonnes pratiques bien sûr)


  1. Lancer Powershell/CMD
  2. Activer l'environnement pour le projet
  ```bash
  conda activate nom_env 
  ```
  3. Se déplacer jusqu'au repo git local qui a été cloné (et est à jour) et ```se placer sur la bonne branche de développement``` à l'aide des commandes git
 
  4. Lancer une commande poetry install dans le projet
  ```bash
  poetry install
  ```
  L'environnement est désormais actualisé\
  Dans l'arborescence du projet, on va désormais trouver un nouveau fichier,  **poetry.lock**:
  ```bash
  project_src
  │   pyproject.toml
  │   README.rst 
  │   poetry.lock
  │
  └───project_name
  │       __init__.py
  │
  └───tests
          __init__.py
          test_project_name.py
  ```
  Le fichier poetry.lock contient des dépendances plus précises que le le fichier toml
  - Si la commande `poetry install` n'a jamais été lancé et qu'il n'y pas de fichier poetry.lock dans le projet, Poetry  va tout simplement résoudre les dépendances présentes dans le fichier pyproject.toml  et télécharger leurs dernières versions. Une fois terminée, le fichier poetry.lock va être créé avec toutes les dépendances exactes, qui serviront dans le cas d'un autre install
  - Si les fichiers poetry.lock et pyproject.toml existent , l'exécution de la commande poetry install, va alors actualiser l'environnement actuel pour correspondre parfaitement avec ces dépendances

  <p style='color:orange'>Ne pas oublier de commit les fichiers poetry également pour permettre aux autre contributeurs du projet de réutiliser l'environnement ou bien le mettre à jour avec des nouvelles dépendances</p>

<br>
<br>

[Accueil](../README.md)