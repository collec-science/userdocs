---
title: les collections
authors: Éric Quinton
license: CC-BY
tags:
  - collection
created: 19/08/2025
---
Les collections regroupent les échantillons en ensembles cohérents. ==À un échantillon correspond une et une seule collection==.

Les collections sont l'unité de base pour gérer les échantillons. Il sera ainsi possible de définir si la collection est publique, les groupes d'utilisateurs autorisés à modifier les échantillons, si des messages de rappel doivent être envoyés pour avertir de l'expiration des échantillons ou d'événements à réaliser, etc.

Seuls les membres du groupe *param* peuvent créer ou modifier une collection (menu *Paramètres > Collections > Collections*).

## Les informations générales
![[Pasted image 20250826112605.png]]

Elles permettent de définir les dispositions générales pour les échantillons qu'elle contient :
- nom : nom de la collection connu dans le logiciel
- nom public : c'est le nom qui sera transmis lors des exportations d'échantillons par lots, notamment quand la collection est définie "publique"
- les mots clés associés sont également utilisés lors de l'exportation des informations. Ils ne servent pas dans le logiciel
- référent de la collection : c'est la personne qui est responsable de celle-ci. Si un échantillon n'a pas de référent attribué, c'est le référent de la collection qui sera utilisé
- flux de modification ou de consultation : pour qu'un échantillon puisse être modifié par une API ([[Les API]]), la collection à laquelle il appartient doit être autorisée à recevoir les flux externes, soit en lecture, soit en lecture-écriture (il faut cocher les deux valeurs)
- collection publique : dans ce cas, il est possible de lire les informations sur les échantillons, notamment via les api, sans recourir à une identification préalable.
- licence de diffusion : si la collection est publique, c'est la licence qui est appliquée pour fournir les informations sur les échantillons
- collection sans la gestion de la localisation : si vous gérez des échantillons sans avoir besoin d'afficher de coordonnées géographiques, vous pouvez activer cette possibilité. Dans ce cas, les cartes et les coordonnées géographiques ne seront pas affichées
- par défaut, le logiciel stocke les documents associés aux échantillons dans la base de données. Dans certains cas (fichiers volumineux), il est plus intéressant de "brancher" la collection à une arborescence bureautique. Pour savoir comment paramétrer cette fonctionnalité, consultez le document [[Associer des documents externes à un échantillon]].

## Les groupes d'utilisateurs

![[Pasted image 20250826113855.png]]

Seuls les membres d'une collection peuvent modifier un échantillon qu'elle contient et visualiser les métadonnées  et les documents associés (ce comportement peut être modifié : *cf.* [[Les paramètres généraux de l'application]]).

Pour qu'un utilisateur puisse créer ou modifier un échantillon, il doit faire partie d'un des groupes attaché à la collection. Dans cet exemple, seuls les membres du groupe *collection* pourront modifier les échantillons de cette collection.

## Les types d'échantillons rattachés

![[Pasted image 20250826114259.png]]

## Les types d'événements rattachés

![[Pasted image 20250826114214.png]]

## La gestion des notifications


![[Pasted image 20250826114413.png]]

