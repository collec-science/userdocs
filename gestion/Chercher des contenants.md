---
title: Chercher des contenants
authors: Éric Quinton
license: CC-BY
tags:
  - contenant
created: 17/07/2026
---
## Présentation

L'interface de recherche des contenants est organisé en trois parties :

- la partie haute permet de définir des critères de recherche
- la partie centrale comprend la liste des contenants, et permet également d'imprimer les étiquettes
- la partie basse, sous réserve que vous disposiez du droit *collection* (cf. [[Les différents types de droits]]), vous permet de réaliser des opérations globales sur les contenants.

## L'interface de sélection

Les critères de recherche sont cumulatifs. L'interface est organisé en trois parties : deux onglets permettent de définir les critères de recherche, et la partie basse de la boite de recherche permet d'indiquer le nombre de contenants à afficher.

Lorsque vous arrivez pour la première fois sur cette page, l'application va afficher les 100 contenants les plus récents.

### L'onglet principal

![[Pasted image 20260721164551.png]]

L'onglet UID/identifiant/type permet de réaliser la recherche sur ces critères :

- l'UID du contenant ;
- l'identifiant métier du contenant, ou son #UUID. Si vous voulez utiliser une douchette, c'est dans cette zone que vous devrez vous positionner ;
- une fourchette d'UID ;
- la famille ou le type du contenant. Pour rechercher par le type de contenant, vous devrez au préalable sélectionner la famille ;
- le statut du contenant ;
- et enfin, s'il a été mis à la corbeille (*En attente de suppression*).

### Les autres informations

![[Pasted image 20260721165102.png]]

Le second onglet vous permet de rechercher :

- les contenants qui auraient été affectés à une collection. Cette affectation n'est pas obligatoire, il est possible que vous ne retrouviez pas vos contenants s'ils n'ont pas été associés ;
- les contenants gérés par un référent ;
- les contenants qui auraient subi un type d'événement particulier ;
- ceux qui auraient été sortis du stock pour un motif particulier ;
- ou de réaliser une recherche par *date technique de dernier changement*, c'est à dire la dernière fois où ils ont été modifiés dans la base de données. Vous pourrez indiquer l'intervalle de date à rechercher.

## La liste des contenants

![[Pasted image 20260721165657.png]]

La liste des contenants propose plusieurs fonctionnalités :

- vous pouvez indiquer les colonnes à afficher ;
- en laissant la souris positionnée sur l'UID d'un contenant, vous afficherez la grille (les lignes et les colonnes) du contenant, avec l'ensemble des objets qui y sont contenus. Si une cellule contient trop d'objets, le nombre d'objets contenus sera affiché ;
- en cliquant sur le signe **+** juste avant l'identifiant métier, l'application affichera la liste des contenants situés dans le contenant courant. Vous pourrez ainsi naviguer dans les différents contenants emboîtés.
  Attention toutefois : si la liste contient déjà un des contenants qui est positionné dans le contenant courant, l'information sera dupliquée dans la liste (mais pas dans la base de données).

Vous pouvez également sélectionner un ou plusieurs contenants, puis :

- imprimer les étiquettes ;
- exporter les contenants sélectionnés au format CSV ;
- réaliser un export avec les objets inclus, pour l'exporter vers une autre instance Collec-Science (*cf.* [[Exporter les contenants avec leur contenu vers une autre instance Collec-Science]]).

## Les opérations globales de modification des contenants

Si vous disposez du droit *collection*, vous pourrez réaliser des opérations globales sur les contenants sélectionnés.

![[Pasted image 20260721171023.png]]

### Prêter les contenants et leurs contenus

Cette opération est particulièrement adaptée si vous souhaitez transmettre une boite de tubes (ou d'autres éléments) vers un autre laboratoire qui utilise Collec-Science. Pour le contenant et tout ce qu'il contient (d'autres contenants, des échantillons), elle va créer un prêt, avec le nom de l'emprunteur, la date de prêt et la date de retour escomptée.

Un mouvement de sortie de l'objet (déstockage) va également être généré.

Le statut de l'ensemble des objets concernés va passer à *Objet prêté*, et ne sera plus visible dans la liste, sauf si vous modifiez le statut à rechercher.

Une opération de prêt est réalisée par objet : vous pourrez réintégrer les objets indépendamment des uns des autres, à leur retour.

### Assigner un référent

Cette opération vous permet de changer le référent d'un lot de contenants en une seule opération.

### Modifier le statut

Si vous souhaitez réintégrer des contenants qui ont été prêtés, vous pouvez modifier le statut directement avec cette option. 

Si le statut des contenants était à *objet prêté*, la date de retour sera automatiquement renseignée dans l'enregistrement du prêt.

Si le contenant contient une liste d'objets, ceux-ci seront également réintégrés (modification du statut automatique, enregistrement de la date de retour).

### Assigner une collection aux contenants

Dans certains cas, vous pourriez souhaiter affecter des contenants à une collection. 

Cette opération n'a pour but que de faciliter la recherche des contenants, elle n'influe en rien sur les autres opérations possibles sur les contenants. En particulier, il n'y a pas de gestion de droits liée à la collection de rattachement des contenants.

### Sortir les contenants

Cette opération va créer un mouvement de sortie (de déstockage) sur la liste des contenants concernés.

### Entrer ou déplacer les contenants au même emplacement

Avec cette opération, vous pourrez positionner tous les contenants dans le même contenant.

### Mettre les contenants à la corbeille ou les en sortir

Collec-Science dispose d'une fonctionnalité permettant de mettre des objets à la corbeille pour qu'ils n'apparaissent plus dans les listes, sans toutefois les supprimer définitivement.

Pour faire apparaître les contenants qui ont été mis à la corbeille, vous devrez agir sur l'item *En attente de suppression* dans l'onglet *UID/identifiant/type* de la boite de recherche.

### Supprimer les contenants

La suppression des contenants échouera si des objets sont présents dans celui-ci. Vous devrez au préalable réaliser des opérations de sortie pour l'ensemble des objets présents dans celui-ci.

Pour faciliter cette opération de sortie, vous pourrez aller dans le détail du contenant, et utiliser les fonctionnalités de groupe à partir de la liste des échantillons ou des contenants présents.