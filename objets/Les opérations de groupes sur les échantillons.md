---
title: Les opérations de groupes sur les échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - échantillons
created: 19/08/2025
---
## Présentation

À partir de la liste des échantillons, il est possible de déclencher diverses opérations sur les échantillons sélectionnés.

Pour pouvoir avoir accès à ces fonctionnalités, l'utilisateur doit disposer du droit **collection**, qui permet de manipuler rapidement l'ensemble des échantillons d'une collection.

Certaines opérations imposent qu'une collection soit sélectionnée dans les paramètres de recherche des échantillons. Dans le cas contraire, les opérations considérées ne sont pas accessibles.

Les opérations vont modifier individuellement les échantillons, et jamais de façon groupée. Elles sont l'équivalent d'une modification individuelle de chaque échantillon, il ne sera pas possible d'annuler collectivement une opération. **Ce sont des actions très structurantes** : vérifiez bien ce que vous faites avant de les valider !

Avant de lancer une opération, pensez à cocher les échantillons concernés. Vous pouvez sélectionner (ou désélectionner) tous les échantillons en cliquant sur la case *Tout cocher* ou dans la première colonne de l'entête du tableau.

![[Pasted image 20260205104846.png]]

## les différentes opérations possibles

### Assigner un référent aux échantillons

L'opération va permettre d'indiquer un nouveau responsable, il suffit de le sélectionner dans la liste :

![[Pasted image 20260205105352.png]]
### Créer un événement

Vous pouvez créer un événement pour chaque échantillon concerné, en indiquant les informations nécessaires :

![[Pasted image 20260205105521.png]]
Indiquez soit la date d'échéance, si c'est un événement programmé, soit la date de réalisation. Chaque échantillon sélectionné sera doté d'un événement chacun, qui pourra être manipulé indépendamment des autres.

Vous pourrez manipuler collectivement les événements créés depuis la liste des événements (menu Objets > Événements).

### Prêter les échantillons

L'opération de prêt va modifier de façon importante les échantillons concernés :

- le statut va passer à "Objet prêté" ;
- un mouvement de sortie va être généré automatiquement.

Vous devrez renseigner l'emprunteur, la date du prêt et la date de retour escomptée, ce qui vous permettra de retrouver les échantillons prêtés soit depuis la liste des emprunteurs, soit depuis l'interface de recherche, en sélectionnant le statut *Objet prêté*.

![[Pasted image 20260205110134.png]]

### Sortir les échantillons

Cette opération va générer un mouvement de sortie. Aucune information ne peut être indiquée ici.

### Créer un lot d'export

Cette opération impose qu'une collection soit sélectionnée pour qu'elle puisse être exécutée. Consultez la page [[Les exports par lots]] pour plus d'informations.

### Affecter un pays de collecte

Vous pouvez indiquer le pays de collecte, utilisé dans le cadre du protocole de Nagoya, en le sélectionnant dans la liste officielle des pays :

![[Pasted image 20260205111115.png]]
