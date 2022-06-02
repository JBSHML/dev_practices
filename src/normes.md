# 4-Normes de développement: Git & Precommit :large_blue_diamond:
## Precommit
\
 Les precommit permettent d'effectuer certaines actions avant de commit du code, notamment, afin de s'assurer de certaines normes et d'une qualité de code de façon plus ou moins automatisées 

## Mettre en place des precommit
### a) Installer le pre-commit via poetry (un seul fichier precommit, actualiser à chaque ajoutr de hooks nécessaires)
\
La première étape consiste à ajouter dans l'environnement conda du projet, via Poetry, la librairie de precommit (exemple: [Black](https://github.com/psf/black), qui est un formatter de code Python)

  1. Lancer Powershell/CMD
  2. Activer l'environnement du projet
  ```powershell
  conda activate my_env
  ```
  3. Se déplacer jusqu'au répertoire du projet (qui contient les fichiers poetry) et exécuter:
  ```powershell
  poetry add black
  ```


<br>

### b) Création ou mise à jour du fichier ```.pre-commit-config.yaml``` 
<br>

  1. Une fois la libraire black ajouter, il faut configurer les precommit hooks git du projet. Pour cela, on se rend dans à la racine du projet (là où se trouvent les fichiers poetry) et on va créer un nouveau fichier ```.pre-commit-config.yaml```, compléter par ces informations:

  ```yaml
  #Commande lancée à chaque tentative de commit, se stop et renvoie l'erreur dès qu'un hook fail
  fail_fast: true 
  repos:
  - repo: local
    hooks:
      - id: system 
        name: Black
        entry: poetry run black . 
        language: system
  ```

  2. Retourner sur Powershell, dans l'environnement Conda du projet, et exécuter l'installation de ces hooks avec:
  ```bash
  pre-commit install
  ```
  <p style='color:orange'>Désormais, à chaque tentative de commit, qu'on veillera à lancer dans l'environnement du projet (toutes les opérations git via le powershell, dans vscode, en étant bien l'environnement conda du projet), on aura la commande `poetry run black .` qui s'executera.</p>

  <p style='color:orange'>Si des modifications de fichiers sont à appliquer, celles-ci seront indiquées dans le la console powershell/cmd (files formatted). Il faudra alors penser rajouter les fichiers modifiés via git add puis de retenter le commit. Si tous les hooks sont ok, le code est alors commit</p>

<br>

### C) Exemple de hooks populaires et conseillés: Black, isort et Pylint 

<br>

 - black: formatter de code Python (paramètrable, voir la [documentation](https://github.com/psf/black))
 - isort: formatter de code afin de trier les imports dans l'ordre des conventions builtin, puis via pip, puis module locaux, ... (paramètrable, voir la [documentation](https://github.com/PyCQA/isort))
 - pylint: Analyser de code python avec notation de qualité (paramètrable, voir la [documentation](https://pylint.pycqa.org/en/latest/))

Les hooks s'ajoutent via les même commandes et dans les mêmes contextes que l'exemple de Black présenté au dessus.\
Voici un exemple de fichier ```.pre-commit-config.yaml``` avec ces hooks:

```yaml
fail_fast: true
repos:
  - repo: local
    hooks:
      - id: system
        name: BLACK
        entry: poetry run black .
        pass_filenames: false
        language: system
  - repo: local
    hooks:
      - id: system
        name: ISORT
        entry: poetry run isort .
        pass_filenames: false
        language: system
  - repo: local
    hooks:
      - id: system
        name: PYLINT
        entry: poetry run pylint --fail-under=9 --fail-on=E --output-format=colorized src #Ici score >9/10 mais paramétrable
        pass_filenames: false
        language: system
````
<br>
<br>

[Accueil](../README.md)
