---
title: Utiliser ODK pour importer des échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - odk
  - échantillon
created: 29/09/2026
---
ODK est un ensemble de logiciels qui permet de saisir des informations sur le terrain à partir d'un terminal Android, puis de récupérer celles-ci soit dans un drive *google*, soit à partir d'un serveur *ODK Central*. Voici la présentation qui en est faite depuis le site https://docs.getodk.org/ :

==_ODK_ is a data collection platform that helps researchers, field teams, and other professionals collect the data they need wherever it is. For a quick start, read [Getting Started With ODK](https://docs.getodk.org/getting-started/).==

Techniquement : 

- un formulaire est décrit dans un document au format Excel (xslx). Ce document comprend au minimum trois onglets, l'un dédié aux questions du formulaire, l'autre aux choix types, et le troisième est la *carte de visite* du formulaire ;
- ce document est déposé dans un serveur ODK Central, qui va le transformer en fichier normé
- le logiciel *ODK Collect* est installé dans un terminal Android. Le formulaire va être téléchargé à partir d'un qrcode généré par le serveur
- une fois le formulaire renseigné, il est automatiquement envoyé au serveur. ODK collect gère l'absence de réseau, pour n'envoyer les informations que lors qu'il est disponible
- il ne reste plus qu'à récupérer les informations saisies, qui sont fournies dans des fichiers csv encapsulés dans un fichier compressé au format zip.

ODK permet de saisir toutes sortes d'informations, de positionner des points gps, d'intégrer des photos, des vidéos, des enregistrements sonores. Il est possible de réaliser des boucles (pour saisir plusieurs fois le même type d'information), de rajouter des conditions, des calculs, etc.

## ODK et Collec-Science

Pour automatiser l'enregistrement des échantillons collectés sur le terrain, il est possible, à partir de la version v27.0.0 de Collec-Science, de :

- générer un fichier excel qui pourra être directement inséré dans le serveur ODK Central
- d'importer automatiquement les échantillons décrits à partir du formulaire généré dans Collec-Science.

Pour générer le formulaire ODK, l'utilisateur va :

- sélectionner la collection cible
- sélectionner les types d'échantillons qu'il souhaite collecter sur le terrain
- ajouter quelques informations complémentaires, comme la campagne de prélèvement, les référents potentiels, si des photos ou vidéos peuvent être ajoutées, etc.

Une fois les formulaires saisis sur le terrain, il ne restera qu'à récupérer les informations dans un fichier zip, puis à l'importer dans Collec-Science.

[[Générer le formulaire ODK]]

[[Importer les données saisies avec ODK Collect]]

