---
title: Les opérations globales sur les échantillons
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
### Rattacher à une campagne de prélèvement

Sélectionnez la campagne de prélèvement pour y rattacher les échantillons : 

![[Pasted image 20260205154006.png]]

### Modifier le statut

La liste des statuts est fixe, et ne peut être modifiée (seuls les libellés peuvent être adaptés). Les statuts sont identiques pour les échantillons ou les #contenants . Les #statuts en vigueur sont :

- État normal : tout échantillon stocké localement ;
- objet pré-réservé pour usage ultérieur : cela concerne peu les échantillons, mais est surtout utilisé pour les contenants ;
- objet détruit : cela concerne des échantillons dont on veut conserver la trace, mais qui n'existent plus ;
- HS - vide - non conforme : c'est une variante du statut précédent ;
- objet perdu : objet dont on a perdu la trace ;
- objet prêté : normalement, ce statut est géré automatiquement par le logiciel quand on prête un échantillon.


![[Pasted image 20260205154103.png]]

Attention : après modification du statut, les échantillons n'apparaîtront plus par défaut dans la liste des échantillons, sauf si on modifie les critères de recherche en désactivant "État normal" ou en sélectionnant un statut particulier.

![[Pasted image 20260205154811.png]]
### Entrer ou déplacer dans un même contenant

Si l'interface proposé est identique à celui utilisé pour la création d'un mouvement, il doit être manipulé avec précaution, notamment si vous voulez indiquer un numéro de ligne et de colonne. Dans ce cas de figure, les échantillons seront tous rangés au même endroit.

![[Pasted image 20260205155019.png]]
### Modifier la collection d'affectation

L'utilisateur qui réalise l'opération doit disposer des droits à la fois sur la collection d'origine et sur la nouvelle collection.

![[Pasted image 20260205155229.png]]

### Assigner un parent aux échantillons

Cela permet *a posteriori* d'affecter un parent à un ou plusieurs échantillons "enfants". 

![[Pasted image 20260205155428.png]]

Dans la zone *Recherchez le parent*, indiquez l'UID ou l'identifiant métier, puis cliquez sur la loupe pour le rechercher. Le parent (ou les parents potentiels, le logiciel réalise une recherche "plein texte") est alors affiché dans la liste *Parent à affecter*.

Avec ce module, faites attention à ne pas créer une boucle (un parent qui contiendrait un enfant qui lui-même contiendrait le parent) : vous risqueriez de faire planter le serveur en saturant toutes les ressources !

### Créer un échantillon composé

Un échantillon composé est un échantillon qui contient un sous-échantillonnage de plusieurs autres échantillons, par exemple pour réaliser une analyse globale.

![[Pasted image 20260205155936.png]]
Vous devrez indiquer :

- la quantité de sous-échantillonnage que vous retirez de chaque parent. Dans ce contexte précis, la quantité retirée de chaque parent est identique : si vous souhaitez des quantités différentes, vous devrez soit réaliser des modifications depuis le détail de l'échantillon qui sera créé, soit créer les sous-échantillonnages un par un ;
- l'identifiant métier de l'échantillon créé ;
- sa collection d'affectation ;
- le type d'échantillon créé.

Vous avez également la possibilité de rattacher des échantillons parents à un échantillon composé déjà existant. Dans ce cas de figure, indiquez son UID ou son identifiant métier puis cliquez sur la loupe pour le retrouver dans la base de données.

Par défaut, la quantité de l'échantillon créé est la somme des quantités prélevées de chaque échantillon parent. Toutefois, dans certains cas de figure, l'échantillon que vous allez créer peut être plus volumineux (ajout d'un solvant, par exemple). Si vous créez l'échantillon composé *ex nihilo*, vous avez alors la possibilité d'indiquer la quantité réelle qu'il contiendra.

### Mettre ou sortir de la corbeille

La corbeille fonctionne comme pour les logiciels de messagerie : si vous mettez un message dans celle-ci, celui-ci n'est plus visible, mais n'est pas encore supprimé. De la même manière, vous pouvez mettre de côté un échantillon avant de le supprimer.

Si un échantillon a été mis à la corbeille, il ne sera plus visible, sauf si vous changez les paramètres de recherche :

![[Pasted image 20260205160828.png]]

### Supprimer les échantillons

Cette opération supprime de manière définitive les échantillons sélectionnés. Si vous hésitez, placez-les plutôt dans la corbeille...

La suppression d'un échantillon ne fonctionnera pas si des échantillons dérivés ont été créés à partir de celui-ci.

### Supprimer les échantillons et tous les échantillons dérivés

Cette fonction permet de faire un grand ménage : il va supprimer tous les échantillons et tous les échantillons enfants (dérivés) qui lui sont rattachés, et ceci en cascade.

Manipulez cette fonctionnalité avec précaution !

### Ajouter les mêmes documents aux échantillons

Vous retrouverez ici le même interface qui permet de rattacher un document à un échantillon. Attention : le document sera dupliqué dans la base de données pour chaque échantillon de rattachement.

![[Pasted image 20260205161336.png]]

Vous pouvez indiquer la date de création et une description.