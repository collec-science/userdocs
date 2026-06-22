---
title: Exporter les échantillons dans un format particulier
authors: Éric Quinton
license: CC-BY
tags:
  - export
created: 21/06/2026
---
Collec-Science dispose d'un module qui permet de préparer des exportations dans des formats particuliers, notamment pour les charger dans des logiciels tiers. Ce module a été testé avec succès pour exporter des échantillons vers la collection d'échantillons ichtyologiques Colisa (https://colisa.hub.inrae.fr), vers le logiciel de rédaction de cahiers de laboratoires ElabFTW (https://www.elabftw.net/) ou le GBIF  *Global Biodiversity Information Facility* (https://www.gbif.org/fr/).

Pour pouvoir réaliser un export de ce type, il faut d'abord définir un modèle d'export. Un modèle d'export peut contenir un ou plusieurs modèles de  jeux de données (*datasets*), qui décrivent les informations qui doivent être exportées, et sous quel format.

Pour réaliser un export, l'utilisateur doit sélectionner les échantillons concernés et créer un lot d'export. Ce lot sera alors traité en fonction du modèle d'export, et un fichier sera alors généré (soit un fichier simple, comme un CSV, soit un fichier ZIP contenant plusieurs fichiers - un par jeu de données).

Voici l'organisation générale :

![[lots pour exportation.png]]

Un modèle d'export contient un ou plusieurs modèles de jeux de données, chacun décrivant les informations qui peuvent être exportées. Si nécessaire, les libellés peuvent être transcodés en utilisant des traducteurs.
## Les différentes étapes pour créer un modèle d'export

Consultez le document [[Préparer un modèle d'exportation]].

## Créer un lot d'échantillons

La création des lots d'échantillons n'est possible que si les échantillons appartiennent à la même collection. Vous devrez impérativement sélectionner une collection dans l'interface de recherche pour pouvoir déclencher la création du lot.

Depuis la page de recherche des échantillons : 

- sélectionnez la collection qui contient vos échantillons 

![[Pasted image 20260622172706.png]]

- sélectionnez les échantillons que vous souhaitez exporter
- en bas de la liste, choisissez l'option *Créer un lot d'export*. Vous devez disposer du droit *collection* (*cf.* [[Les différents types de droits]]) pour accéder à cette fonction

![[Pasted image 20260622172853.png]]

Une fois le lot créé, le logiciel affiche le détail du lot.

## Exporter un lot d'échantillons dans le format désiré

La page d'affichage du détail du lot vous permet de consulter la liste des échantillons exportés. Si besoin était, vous pouvez effacer un des échantillons de la liste, mais vous ne pourrez pas en rajouter un : dans ce cas, vous devrez recréer un lot d'exportation.

![[Pasted image 20260622173450.png]]


Cliquez sur le lien *Nouvel export*, puis choisissez le modèle d'export que vous voulez utiliser. La liste contient dès lors un nouvel item : il ne vous reste plus qu'à cliquer sur l'icone *ad hoc* pour générer l'export.

![[Pasted image 20260622173839.png]]

Vous pouvez utiliser plusieurs modèles à partir d'un lot d'échantillons, voire relancer l'exportation si des modifications ont été réalisées sur les échantillons après le premier export (seuls les UID des échantillons sont enregistrés dans les lots).

## Manipuler les lots d'exportation

Depuis le menu, choisissez *Imports/Exports > Lots d'export*. Sélectionnez la collection pour afficher ensuite la liste des lots attachés à celle-ci.

![[Pasted image 20260622174457.png]]

Vous pourrez alors accéder au détail des lots pour réaliser une nouvelle exportation.