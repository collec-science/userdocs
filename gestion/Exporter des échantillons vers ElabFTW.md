---
title: Exporter des échantillons vers ElabFTW
authors: Éric Quinton
license: CC-BY
tags:
  - elabftw
  - export
created: 17/06/2026
---
ElabFTW (https://www.elabftw.net/) est un logiciel de gestion électronique des cahiers de laboratoires, largement utilisé par le CNRS et INRAE.

Depuis Collec-Science, il est possible de créer un fichier CSV qui permettra d'importer dans ce logiciel les échantillons qui pourront alors être référencés dans les expérimentations. L'exportation utilise le module d'export *à façon*, qui permet de créer des fichiers d'exportation dans des formats différents (*cf.* [[Exporter les échantillons dans un format particulier]]).

L'exportation va se dérouler en plusieurs phases : 

- depuis la liste des échantillons, les échantillons sélectionnés vont être regroupés dans un lot ;
- depuis le détail du lot, un modèle d'export va être associé ;
- une fois le modèle d'export associé, la génération du fichier créera automatiquement le fichier CSV qui pourra être intégré dans le logiciel ElabFTW.

Pour pouvoir réaliser un lot d'export et donc réaliser cette opération, vous devez impérativement disposer du droit *collection* (*cf.*[[Les différents types de droits]] ).
## Créer le lot d'export

Depuis la liste des échantillons :

- sélectionnez impérativement la collection qui contient les échantillons à exporter (il n'est pas possible d'exporter en une seule fois des échantillons appartenant à deux collections différentes) ;
- cochez tous les échantillons dont vous souhaitez transférer les coordonnées à ElabFTW ;
- depuis le menu situé sous la liste, choisissez l'item *Créer un lot d'export*.

Le lot va être créé, et l'application va se positionner sur la *liste des lots d'export*. Vous pourrez la retrouver en choisissant, dans le menu : *Imports/Exports > Lots d'export*.

![[Pasted image 20260617153711.png]]
Les lots sont conservés tant que vous ne les supprimez pas, vous pourrez les réutiliser si nécessaire, voir supprimer des échantillons à l'intérieur de la liste le cas échéant.

Cliquez sur le détail du lot qui vous intéresse :

![[Pasted image 20260617153951.png]]
L'onglet *Liste des échantillons exportés* vous permettra de vérifier les échantillons sélectionnés, voire de supprimer ceux qui auraient été ajoutés indûment.

Cliquez sur *Nouvel export*. Choisissez le modèle **elabftw**, qui a été pré-chargé dans votre base de données, puis validez.
![[Pasted image 20260617154239.png]]

L'application affiche alors le détail du lot, où vous retrouverez maintenant le modèle d'export :

![[Pasted image 20260617154346.png]]
Cliquez alors sur l'icone *Générer l'export* pour créer le fichier CSV au format ElabFTW.

## Importer le fichier dans ElabFTW

Les informations notées ici sont celles qui ont été extraites de la documentation en anglais du logiciel : https://doc.elabftw.net/docs/usage/import-export

- dans le logiciel ElabFTW, assurez-vous de disposer d'au-moins une catégorie de ressource. Si ce n'est pas le cas, demandez à un administrateur de l'application de faire le nécessaire ;
- dans le menu utilisateur (en haut à droite, choisissez la fonction *import*) ;
- sélectionnez votre fichier à importer, choisissez la catégorie de ressource, puis lancez l'importation.

Vous pourrez alors utiliser les ressources créées pour les associer à vos expérimentations.
## Que contient le fichier généré ?

ElabFTW a une gestion particulière des informations transmises : sans précision particulière, tout est mis dans un seul champ texte. Pour éviter cet écueil, Collec-Science transfert la plupart des informations dans un format particulier (champ JSON) qui permet à ElabFTW de traiter de façon plus lisible les données.

Les informations transférées sont les suivantes :

- le type d'échantillon devient le type de la ressource ;
- l'identifiant métier devient le titre de la ressource ;
- la date de création de l'échantillon devient *Démarrée le xxxx*
- les autres informations sont rangées dans la rubrique *Champs supplémentaires* :
	- *collection* comprend le nom de la collection d'origine ;
	- *quantité* contient la quantité associée à l'échantillon, ainsi que l'unité de mesure
	- les métadonnées sont également transférées, elles apparaissent dans une sous-rubrique *metadata*.

Voici un exemple, transmis aimablement par François Ehrenmann lors des premiers tests :

![[resultat_import_elab.png]]


