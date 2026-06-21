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

![[lots pour exportation.png]]

## Les différentes étapes pour créer un modèle d'export

### Créer les traducteurs


### Créer un modèle de jeu de données


### Décrire les colonnes dans le modèle de jeu de données


### Cas particulier du modèle pour ElabFTW


### Créer le modèle d'export et associer les modèles de jeux de données


## Créer un lot d'échantillons


## Exporter un lot d'échantillon dans le format désiré

