---
title: La liste des échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - échantillons
created: 19/08/2025
---
La liste des échantillons est disponible à deux endroits : soit depuis la page de recherche des échantillons ([[Chercher les échantillons]]), soit depuis le détail d'un échantillon, dans l'onglet *Échantillons dérivés*.

La liste est composée de trois parties :

![[Pasted image 20260224111947.png]]

- au dessus du tableau, vous avez la possibilité de générer des étiquettes pour les échantillons sélectionnés ou créer des fichiers au format CSV ;
- le tableau comprend la liste des échantillons ;
- sous le tableau, si vous disposez du droit *collection*, vous aurez la possibilité de réaliser des opérations globales de modification des échantillons.

## L'affichage des échantillons

### Sélectionner les colonnes à afficher

Vous pouvez sélectionner les colonnes que vous souhaitez afficher : 

![[Pasted image 20260224112433.png]]

Il suffit de sélectionner celles qui vous intéressent.

Le moteur d'affichage dispose également de deux boutons qui vous permettront de récupérer le contenu de la liste au format CSV, ou de le copier pour le coller dans une autre application.

Par défaut, les métadonnées sont toutes affichées. Vous avez la possibilité de n'en afficher qu'une seule. Pour cela, dans les critères de recherche :

- positionnez-vous dans l'onglet *Type et métadonnées* ;
- sélectionnez la métadonnée que vous voulez afficher dans la zone *N'afficher qu'une métadonnée* ;
- relancez la recherche.

### Rechercher des libellés dans la liste des échantillons

Au dessus du tableau, à droite, vous disposez d'une zone *Rechercher* qui vous permet de réaliser une recherche plein texte dans l'ensemble du tableau. Toutefois, vous pourriez souhaiter faire une recherche dans une seule colonne : il faut alors changer le mode d'affichage du tableau. Pour cela :

- dans la partie basse du cartouche de recherche des échantillons, cliquez sur la case *Activer la recherche par colonne* ;
  ![[Pasted image 20260224113151.png]]
- relancez la recherche : les entêtes de chaque colonne deviennent maintenant des zones de recherche, qui fonctionneront uniquement pour la colonne considérée.

![[Pasted image 20260224113319.png]]

## Imprimer des étiquettes ou exporter la liste

Trois fonctionnalités sont disponibles pour tous les utilisateurs : 

- l'impression d'étiquettes ;
- la génération d'un fichier utilisable avec un logiciel tiers pour imprimer les étiquettes ;
- la génération d'un fichier d'export, au format CSV, qui est utilisable pour modifier les échantillons en dehors du logiciel ou pour les transmettre à une autre instance de Collec-Science.

Pour que ces opérations puissent être lancées, vous devrez auparavant sélectionner les échantillons concernés. Vous pouvez tous les sélectionner (ou les désélectionner) en utilisant indifféremment la case *Tout cocher* ou celle qui est dans l'entête du tableau, en première colonne.

### L'impression des étiquettes

Sélectionnez le modèle d'étiquettes que vous souhaitez utiliser, puis cliquez sur le bouton *Étiquettes*. Un nouvel onglet s'ouvrira dans votre navigateur, avec les étiquettes prêtes à être imprimées.

Les étiquettes sont conçues pour être imprimées avec des imprimantes à rouleaux : chaque étiquette est séparée par un saut de page, qui correspond à une nouvelle étiquette avec ces imprimantes.

Si vous ne choisissez pas de modèle d'étiquettes, mais que ce modèle a été associé avec le premier type d'échantillons de la liste (*cf.* [[Les types d'échantillons]]), c'est ce modèle qui sera utilisé pour l'ensemble des échantillons sélectionnés.

Pour plus d'informations sur la création des modèles d'étiquettes, consultez la page [[Créer ou modifier un modèle d’étiquettes]].

### Générer un fichier pour imprimer les étiquettes en dehors du logiciel

Si vous souhaitez utiliser un logiciel tiers pour imprimer vos étiquettes, notamment pour pouvoir imprimer des planches d'étiquettes, vous pouvez déclencher l'export d'un fichier dédié au format CSV en cliquant sur le bouton *Fichier CSV pour impression externe*. Le fichier généré aura comme nom *printlabel.csv*.

### Créer un fichier d'export

Le fichier d'export que vous pouvez créer en cliquant sur le bouton *Export vers une autre base* peut être utilisé pour deux usages différents :

- vous pourrez ouvrir ce fichier (au format CSV) avec LibreOffice (évitez Excel, qui pose plus de problèmes de compatibilité), modifier le contenu des informations, puis les réimporter à partir du menu *Imports/Exports > Import d'échantillons externes*. C'est le moyen le plus efficace pour modifier une série d'échantillons, rajouter des informations, etc.
- vous pouvez transmettre le fichier généré à un autre organisme utilisant Collec-Science : il leur suffira d'utiliser la fonction disponible à partir du menu *Imports/Exports > Import d'échantillons externes* pour les importer directement dans leur instance.

Pour plus d'informations sur la fonction d'import externe, consultez la page [[Importer des échantillons externes ou modifier les échantillons avec un logiciel tiers]].


## Les opérations globales de modification des échantillons

Si vous disposez du droit *collection*, vous pourrez réaliser des opérations globales sur les échantillons sélectionnés, sans avoir à les traiter un par un.

Pour plus d'informations sur ces opérations, consultez la page [[Les opérations globales sur les échantillons]]