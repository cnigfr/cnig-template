# Modèle pour les dépôts de standards CNIG

Ce dépôt contient les fichiers nécessaires pour démarrer la création d'un dépôt pour un standard, il est conforme à ce qui est demandé pour un schéma [Table Schema](https://specs.frictionlessdata.io/table-schema/). A noter que la création d'un schéma n'est pas obligatoire pour la création d'un standard CNIG. En revanche, il est obligatoire de créer un dépôt github afin que le standard soit référencé sur schema.data.gouv. Dans le cas où le standard n'a pas de schéma, il faut l'indiquer clairement dans ce fichier (voir plus de conseils sur sa rédaction plus bas).

## Utiliser ce template

- Si vous créez votre dépôt sur GitHub, il vous suffit d'appuyer sur le bouton vert "Use this template". Consultez [la documentation](https://docs.github.com/fr/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) pour plus d'infos ;

> [!NOTE]
> Il est conseillé de se familiariser avec la syntaxe markdown utilisée dans ce document avant de se lancer dans sa rédaction (pour cela, [la documentation de Github](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) peut être utile).
> 
## Fichiers disponibles

Ce dépôt contient un ensemble de fichiers utiles pour le dépôt d'un schéma.

- [`CHANGELOG.md`](CHANGELOG.md) contient la liste des changements entre les différentes versions de votre schéma ;
- [`exemple-valide.csv`](exemple-valide.csv) est un fichier CSV d'exemple conforme par rapport au schéma décrit dans `schema.json`  ;
- [`LICENSE.md`](LICENSE.md) est le fichier de licence du dépôt. Nous recommandons d'utiliser la [Licence Ouverte](https://www.etalab.gouv.fr/licence-ouverte-open-licence), cette licence est recommandée par l'administration française pour le partage de données et de documents ;
- [`README.md`](README.md) est le fichier que vous lisez actuellement. À terme, il devra présenter votre schéma ;
- [`requirements.txt`](requirements.txt) liste les dépendances Python nécessaires pour effectuer des tests en intégration continue sur votre dépôt (il n'est pas nécessaire de modifier ce fichier) ;
- [`schema.json`](schema.json) est le schéma au format [Table Schema](https://specs.frictionlessdata.io/table-schema/).


## Étapes à suivre

Nous détaillons ci-dessous les étapes que nous vous conseillons de suivre après avoir créé votre dépôt Git, tout en utilisant les fichiers d'exemples.

- [ ] Décrire votre schéma dans le fichier `schema.json` en respectant la spécification Table Schema. Le fichier d'exemple comprend des valeurs d'exemples pour toutes les métadonnées possibles. Notez que les champs d'exemple ne comprennent qu'une petite partie des types, formats et contraintes disponibles, référez-vous à [la documentation](https://specs.frictionlessdata.io/table-schema/#types-and-formats) pour toutes les valeurs possibles. Si certaines métadonnées ne sont pas nécessaires pour votre projet, vous pouvez les supprimer. Pour vérifier que votre schéma est conforme, vous pouvez utiliser l'outil [tableschema](https://pypi.org/project/tableschema/) en ligne de commande : `tableschema validate schema.json`
- [ ] Modifier le fichier d'exemple CSV avec des données conforme à votre schéma. L'outil [frictionless](https://pypi.org/project/frictionless/) permet de vérifier que vos fichiers sont conformes au schéma en ligne de commande `frictionless validate --schema schema.json exemple-valide.csv`
- [ ] Modifier le fichier [`CHANGELOG.md`](CHANGELOG.md) pour indiquer la publication initiale. Le contenu de ce fichier sera visible depuis l'onglet "Changements" de la page du schema sur schema.data.gouv.
- [ ] Vérifier que la licence ouverte vous convient. Si vous devez utiliser une autre licence, modifiez le fichier [`LICENSE.md`](LICENSE.md) et indiquez la licence dans le fichier [`schema.json`](schema.json), dans la clé `licenses`
- [ ] Modifier le fichier [`README.md`](README.md). Au sein de plusieurs paragraphes, vous indiquerez le contexte, les modalités de production des données, le cadre juridique, la finalité, les cas d’usage, etc. Consultez plusieurs schémas sur [schema.data.gouv.fr](https://schema.data.gouv.fr) pour découvrir quelles informations sont pertinentes à indiquer. Un modèle de fichier README est proposé plus bas, après la documentation (pour l'utiliser, il vous suffit de supprimer tout ce qui le précède).

> [!IMPORTANT]
> Dans le cas où le standard ne serait pas accompagné d'un schéma de données, il est tout de même nécessaire d'y associer un dépôt github pour qu'il soit référencé sur schema.data.gouv. Dans ce cas, il faut indiquer dans le README :
> - que la description porte sur le standard et non sur le schéma,
> - qu'il n'existe pas de schéma de données,
> - le lien vers le standard sur le site du CNIG.
> Il est tout de même conseillé dans ce cas d'alimenter le dépôt Github puisque la documentation, le cadre juridique, les exemples de données etc. restent pertinents. 

### Intégration continue

Ce dépôt est configuré pour utiliser de l'intégration continue, si vous utilisez GitHub. À chaque commit, une suite de tests sera lancée via [GitHub Actions](https://github.com/features/actions) afin de vérifier :

- que votre schéma est valide à la spécification Table Schema ;
- que vos fichiers d'exemples sont conformes au schéma.

Si vous n'utilisez pas GitHub, vous pouvez lancer ces tests sur votre machine ou sur un autre service d'intégration continue comme Gitlab CI, Jenkins, Circle CI, Travis etc. Consultez la configuration utilisée dans [`.github/workflows/test.yml`](.github/workflows/test.yml).

Localement, voici la procédure à suivre pour installer l'environnement de test et lancer les tests :

```bash
# Création d'un environnement virtuel en Python 3
python3 -m venv venv
source venv/bin/activate

# Installation des dépendances
pip install -r requirements.txt

# Test de la validité du schéma
frictionless validate --type schema schema.json

# Test de la conformité des fichiers d'exemples
frictionless validate --schema schema.json exemple-valide.csv
```

## Lien avec la page sur Schema.data.gouv
Le dépôt github est la source de laquelle la page sur schema.data.gouv prend son contenu. Ainsi, les correspondances suivantes sont effectuées : 
- le fichier README.md apparaît dans l'onglet d'accueil "Informations",
- le fichier documentation.md apparaît dans l'onglet "Documentation",
- le fichier sources.md apparaît dans l'onglet "Règlementation". <!-- à voir si cet onglet est vraiment utile, il répète le paragraphe "Cadre juridique" -->
Les boutons au sommet de la description du standard permettent de réaliser plusieurs actions :
- "Saisir ou valider mes données" : renvoi vers la page "publier.etalab.studio" qui accompagne l'utilisateur poru la production de données conformes à votre standard, 
- "Schéma" : renvoi vers une visualisation du schéma au format JSON,
- "Données" : renvoie vers la page de data.gouv référençant toutes les données conformes au schéma qui y sont publiées,
- "RSS" : permet de renseigner un flux RSS lié au schéma par lequel des informations sur ses évolutions peuvent être communiquées,
- "Git" : renvoie vers ce dépôt Github.

Il est également possible de rendre les anciennes version du schéma depuis sa page en plaçant tous les fichiers dans un dossier nommé avec le numéro de version (comme "1.2" par exemple).


## Documentation

Pour vous aider dans la construction de votre dépôt, nous vous recommandons de vous référer à :

- [Le guide pour la création de schémas](https://guides.data.gouv.fr/guides-open-data/guide-qualite/maitriser-les-schemas-de-donnees/creer-un-schema-de-donnees)
- [la documentation de Github pour le langage markdown utilisé dans les fichiers ".md", comme ce README.md](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [La documentation de schema.data.gouv.fr](https://schema.data.gouv.fr)
- [La spécification Table Schema](https://specs.frictionlessdata.io/table-schema/)

---
<!-- Supprimer cette ligne --> 

# Schéma _Nom_ <!-- Indiquer le nom du schéma à la place de _Nom_. Le texte entre symboles "_" apparaît en italique et doit être remplacé dans ce modèle -->
_Description du schéma et des données qu'il décrit en quelques lignes._

## Contexte
_Le contexte dans lequel le schéma a été élaboré. Il peut être utile de renvoyer ici vers la page du GT CNIG où la documentation du standard correspondant peut être trouvé._

## Modalités de production des données
_A compléter_

## Cadre juridique
_Citer les textes liés aux données sur lesquelles porte le schéma. Même lorsque l'utilisation du schéma n'est pas mentionnée dans les textes, il peut être utile de faire référence ici aux lois, décrets, arrêtés portant spécifiquement sur les données, leur conditions de collecte, de partage, etc. Il n'est pas utile de citer les textes plus généraux (portant sur l'open data par exemple)._

## Finalité
_A compléter._

## Cas d’usage
_Présenter ici quelques cas d'usage de données conformes au schéma. Ces cas peuvent exister ou être fictifs._

## Comment contribuer 
_Fournir ici une adresse mail et le lien vers le dépôt Github du schéma afin de permettre les retours._
