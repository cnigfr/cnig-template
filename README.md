# Modèle pour les dépôts de standards CNIG

Ce dépôt contient les fichiers nécessaires pour démarrer la création d'un dépôt pour un standard, il est également conforme à ce qui est demandé pour un schéma au format [Table Schema](https://specs.frictionlessdata.io/table-schema/). A noter que la création d'un schéma n'est pas obligatoire pour la création d'un standard CNIG. En revanche, il est obligatoire de créer un dépôt github afin que le standard soit référencé sur schema.data.gouv.

## Utiliser ce template

Si vous créez votre dépôt sur GitHub, il vous suffit d'appuyer sur le bouton vert "Use this template". Consultez [la documentation](https://docs.github.com/fr/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) pour plus d'infos. Pour un standard CNIG, voici quelques recommandations spécifiques : 
- "Include all branches" : laisser décoché,
- "Repository name" : le nom choisi doit commencer par "Standard" suivi d'un espace et du nom du standard,
- "Public/Pivate" : choisir "Public" pour que le dépôt soit visible par tous (vous seul pouvez le modifier pour le moment, mais il vous sera possible d'ajouter des collaborateurs comme décrit plus bas).

## Fichiers disponibles

Ce dépôt contient un ensemble de dossiers et fichiers utiles pour le dépôt d'un schéma.

- [`README.md`](README.md) est le fichier que vous lisez actuellement. À terme, il devra présenter votre schéma ;
- [`schema`](schema) est le dossier où l'on peut trouver le schéma au format [Table Schema](https://specs.frictionlessdata.io/table-schema/), ainsi qu'une documentation pour la rédaction du schéma ;
- [`ressources`](ressources) contient les fichiers utiles pour l'utilisation du standard élaborés par le groupe de travail ou provenant de sources tierces ;
- [`groupe_de_travail_CNIG`](groupe_de_travail_CNIG) est le dossier de travail du GT, dans lequel peuvent être référencés les compte-rendus de réunion et tous les documents de travail (ce dossier peut être supprimé si le GT choisit un autre outil que github pour collaborer) ;
- [`CHANGELOG.md`](CHANGELOG.md) contient la liste des changements entre les différentes versions de votre schéma ;
- [`exemple-valide.csv`](exemple-valide.csv) est un fichier CSV d'exemple conforme par rapport au schéma décrit dans `schema.json` ;
- [`LICENSE.md`](LICENSE.md) est le fichier de licence du dépôt. Nous recommandons d'utiliser la [Licence Ouverte](https://www.etalab.gouv.fr/licence-ouverte-open-licence), cette licence est recommandée par l'administration française pour le partage de données et de documents ;
- [`requirements.txt`](requirements.txt) liste les dépendances Python nécessaires pour effectuer des tests en intégration continue sur votre dépôt (il n'est pas nécessaire de modifier ce fichier) ;
- `.gitignore` : fichier généré automatiquement par github pour le suivi des versions des documents. Vous pouvez ignorer ce fichier.


> [!NOTE]
> Il est conseillé de se familiariser avec la syntaxe markdown utilisée dans les documents ".md" avant de se lancer dans leur rédaction (pour cela, [la documentation de Github](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) peut être utile).

## Étapes à suivre

Nous détaillons ci-dessous les étapes que nous vous conseillons de suivre après avoir créé votre dépôt Git, tout en utilisant les fichiers d'exemples.

- [ ] Ajouter des collaborateurs en vous rendant dans l'onglet "Settings", puis Access/Collaborators, puis "Add people" (à limiter aux animateurs et aux membres du GT familier avec Github, pour les autres membres, privilégier les contributions via les "issues") ;
- [ ] Modifier le fichier d'exemple CSV avec des données conforme à votre schéma. L'outil [frictionless](https://pypi.org/project/frictionless/) permet de vérifier que vos fichiers sont conformes au schéma en ligne de commande `frictionless validate --schema schema.json exemple-valide.csv` ;
- [ ] Modifier le fichier [`CHANGELOG.md`](CHANGELOG.md) pour indiquer la publication initiale. Le contenu de ce fichier sera visible depuis l'onglet "Changements" de la page du schema sur schema.data.gouv ;
- [ ] Vérifier que la licence ouverte vous convient. Si vous devez utiliser une autre licence, modifiez le fichier [`LICENSE.md`](LICENSE.md) et indiquez la licence dans le fichier [`schema.json`](schema.json), dans la clé `licenses` ;
- [ ] Modifier le fichier [`README.md`](README.md). Consultez plusieurs schémas sur [schema.data.gouv.fr](https://schema.data.gouv.fr) pour découvrir quelles informations sont pertinentes à indiquer. Un modèle de fichier README est proposé plus bas, après la documentation (pour l'utiliser, il vous suffit de supprimer tout ce qui le précède) ;
#### Si votre standard ne possède pas de schéma 
- [ ] Expliquer dans le README pourquoi un schéma de données n'est pas pertinent dans votre cas ;
#### Si votre standard possède un schéma 
- [ ] Décrire votre schéma dans le fichier `schema.json` en respectant la spécification Table Schema. Le fichier d'exemple comprend des valeurs d'exemples pour toutes les métadonnées possibles. Notez que les champs d'exemple ne comprennent qu'une petite partie des types, formats et contraintes disponibles, référez-vous à [la documentation](https://specs.frictionlessdata.io/table-schema/#types-and-formats) pour toutes les valeurs possibles. Si certaines métadonnées ne sont pas nécessaires pour votre projet, vous pouvez les supprimer. Pour vérifier que votre schéma est conforme, vous pouvez utiliser l'outil [tableschema](https://pypi.org/project/tableschema/) en ligne de commande : `tableschema validate schema.json` ;

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
- le fichier CHANGELOG.md apparaît dans l'ongler "Changements",
- les onglets "Documentation" et "Réglementation" sont générés automatiquement.
Les boutons au sommet de la description du standard permettent de réaliser plusieurs actions :
- "Saisir ou valider mes données" : renvoi vers la page "publier.etalab.studio" qui accompagne l'utilisateur pour la production de données conformes à votre standard, 
- "Schéma" : renvoi vers une visualisation du schéma au format JSON,
- "Données" : renvoie vers la page de data.gouv référençant toutes les données conformes au schéma qui y sont publiées,
- "RSS" : permet de s'abonner au flux RSS lié au schéma par lequel des informations sur ses évolutions peuvent être communiquées,
- "Git" : renvoie vers ce dépôt Github.

Il est également possible de rendre les anciennes version du schéma depuis sa page en plaçant tous les fichiers dans un dossier nommé avec le numéro de version (comme "1.2" par exemple).


## Documentation

Pour vous aider dans la construction de votre dépôt, nous vous recommandons de vous référer à :

- [Le guide pour la création de schémas](https://guides.data.gouv.fr/guides-open-data/guide-qualite/maitriser-les-schemas-de-donnees/creer-un-schema-de-donnees)
- [Le guide pour l'intégration de schémas à schema.data.gouv](https://guides.data.gouv.fr/guides-open-data/guide-qualite/maitriser-les-schemas-de-donnees/integrer-un-schema-de-donnees-a-schema.data.gouv.fr)
- [la documentation de Github pour le langage markdown utilisé dans les fichiers ".md", comme ce README.md](https://docs.github.com/fr/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [La documentation de schema.data.gouv.fr](https://schema.data.gouv.fr/validation.html)
- [La spécification Table Schema](https://specs.frictionlessdata.io/table-schema/)
- [Les règles Semver de numérotation des versions](https://semver.org/lang/fr/)

---
<!-- Supprimer cette ligne --> 

# Standard _Nom_ <!-- Indiquer le nom du schéma à la place de _Nom_. Le texte entre symboles "_" apparaît en italique et doit être remplacé dans ce modèle -->
_Description du schéma et des données qu'il décrit en quelques lignes. Ici comme dans la suite, il est recommandé de réutiliser le contenu du mandat du GT ou d'autres documents déjà rédigés. Voici plusieurs exemples pour vous inspirer dans la rédaction :_
* _[standard des opération d'aménagement](https://github.com/cnigfr/schema-operations-amenagement/)_
* _[standard risques](https://github.com/cnigfr/Geostandards-Risques)._
_Attention : Dans la suite, tout ce qui est en italique doit être supprimé._

_Préciser ici si le standard est accompagné d'un schéma ou non par soucis de clarté sur le site schema.data.gouv :_

_Si le standard ne possède pas de schéma :_ 
> [!TIP]
> Ce standard n'a pas un schéma directement exploitable par schema.data.gouv.fr. Vous pouvez le consulter sur le site du CNIG.

_Si le standard possède un schéma :_
> [!TIP]
> Ce standard, disponible sur le site du CNIG, est traduit par un schéma conforme à schema.data.gouv.fr

<!-- Insérer une image ici pour représenter la thématique liée à votre standard en suivant le modèle "![texte alternatif](lien vers l'image) --> 
![logo du CNIG à remplacer par l'image du standard](https://cnig.gouv.fr/IMG/png/cnig2022_geolocalise-petit.png)

## Contexte
_Le contexte dans lequel le schéma a été élaboré. Il peut être utile de renvoyer ici vers la page du GT CNIG où la documentation du standard correspondant peut être trouvé._

## Cadre juridique
_Citer les textes liés aux données sur lesquelles porte le schéma. Même lorsque l'utilisation du schéma n'est pas mentionnée dans les textes, il peut être utile de faire référence ici aux lois, décrets, arrêtés portant spécifiquement sur les données, leur conditions de collecte, de partage, etc. Il n'est pas utile de citer les textes plus généraux (portant sur l'open data par exemple)._

## Finalité
_Les enjeux et objectifs liés à la création du standard doivent être précisés ici._

## Cas d’usage
_Présenter ici quelques cas d'usage de données conformes au schéma. Ces cas peuvent exister ou être fictifs._

## Organisation du dépot
* Le dossier [ressources](ressources) contient les documents utiles pour les utilisateurs du standard ;
* Le dossier [groupe_de_travail_CNIG](groupe_de_travail_CNIG) contient les compte-rendus de réunions et les documents de suivi du groupe de travail ; 
* Le dossier [standard](standard) contient le standard ainsi que les documents qui lui sont liés ;
* Le dossier [schéma](schéma) contient le schéma ainsi que les documents qui lui sont liés.

## Modalités de production des données
_Dans le cas où la création du standard interviendrait alors que les données sont déjà produites, documenter ici comment leur production a lieu. Dans le cas contraire, cette partie peut être supprimée._
### Données ouvertes
_Dans le cas où les données sont publiées en open data, sinon, cette partie peut être supprimée._
Les données relatives à _la thématique_ sont ouvertes et sont à la disposition de tous. Elles seront publiées sur https://www.data.gouv.fr

## Informations et participation au groupe de travail
### Méthodologie 
_Cette partie peut être laissée telle quelle. Elle vise à expliquer les modalités d'adoption d'un standard par le CNIG._
La méthodologie des groupes de travail du CNIG repose sur une diversité d'approches complémentaires :
* Construire **une gouvernance ouverte** à l'ensemble des parties prenantes, afin de susciter l’adhésion et de créer le cadre favorable à la pérennité du dispositif ;
* Promouvoir et exploiter **les retours d'expériences** afin d'étudier les diversités d'usages et embarquer les acteurs en les positionnant au centre du processus d’alimentation des référentiels géographiques ;
* Privilégier **l’interopérabilité** entre système d'informations à l’échelle nationale pour favoriser le partage et l’échange de données : éviter les double stockages, double saisies, etc. ;
* S'appuyer sur les **processus éprouvés** de [standardisation du CNIG](http://cnig.gouv.fr/les-standards-cnig-a18959.html#Etapes-de-creation-d-un-Standard-CNIG) et de modélisation suivant [schema.data.gouv.fr](https://guides.etalab.gouv.fr/producteurs-schemas/).
L’objectif est d'aboutir à terme à un consensus qui se traduise en un standard et un modèle de donnée commun pour la thématique considérée.

### Actualisation
_Préciser ici la phase d'avancement dans laquelle se trouve le standard selon la terminologie de [la Fabrique des standards](https://guides.data.gouv.fr/guides-de-data.gouv.fr/fabrique-des-standards/la-fabrique-des-standards) (rédaction, validation, déploiement, etc.). Il peut être utile de donner des élements de calendrier comme la date de passage en commission des standards ou devant le conseil plénier._

### Comment contribuer 
_Indiquer ici comment contribuer au standard. Par exemple :_
Vous pouvez contribuer au standard en créant une issue sur cette page (il s'agit d'une fonctionalité permettant de poser une question, de faire une remarque, une suggestion etc. directement sur github, ce qui en informe automatiquement les responsables du dépôt).

### Nous contacter
Pour contacter le GT CNIG _thématique_, écrire à l’adresse cnig[at]cnig.fr.

### Licence
Les travaux du GT CNIG _thématique_ sont réalisés sous [Licence Ouverte Etalab 2.0](https://www.etalab.gouv.fr/licence-ouverte-open-licence/).
