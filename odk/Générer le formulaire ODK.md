---
title: Générer le modèle ODK
authors: Éric Quinton
license: CC-BY
tags:
  - odk
created: 1/10/2026
---
La création d'un formulaire ODK va passer par plusieurs étapes successives :

- la création des informations générales
- la sélection des types d'échantillons qui seront utilisés, des référents des échantillons et des sites fréquentés
- la génération des lignes du formulaire
- la modification éventuelle des lignes, pour adapter la présentation
- et enfin, la génération de la feuille Excel.

## La création des informations générales

Depuis la liste des projets ODK (menu *Imports/Exports > Formulaires ODK*), cliquez sur le bouton *Nouveau...*. 

![[Pasted image 20261001100916.png]]

Voici les informations à indiquer :

- nom de la collection : c'est la collection de destination des échantillons. Elle est également utilisée pour limiter les types d'échantillons qui pourront être saisis sur le terrain 
- nom du formulaire : c'est le nom qui vous permet de retrouver votre formulaire
- identifiant unique : c'est l'identifiant qui sera transmis au serveur ODK Central. Il doit être unique
- projet ODK : pour vous aider à vous y retrouver...
- description : n'hésitez-pas à dire à quoi va servir le formulaire !
- campagne de prélèvement : les échantillons saisis sur le terrain seront rattachés à la campagne sélectionnée
- sous-échantillonnage : en activant cette information, vous pourrez, à partir d'un premier échantillon saisi sur le terrain, déclarer des sous-échantillons (échantillons dérivés). Par exemple, si vous récoltez sur une arbre des feuilles, des fruits, un morceau d'écorce, vous pourrez d'abord déclarer l'arbre comme échantillon principal (et virtuel, à moins que vous le rameniez dans votre besace), puis saisir les prélèvements effectués, qui seront rattachés à votre arbre
- version du formulaire : c'est le numéro de version qui sera inséré dans le formulaire.

Une fois le formulaire créé, vous arriverez à la page de détail :

![[Pasted image 20261001101134.png]]

Vous avez accès à trois onglets : 

- le premier contient les informations générales sur le formulaire, celles que vous venez de saisir
- le second permet d'indiquer les types d'échantillons que vous voulez utiliser
- le troisième permet d'indiquer des informations complémentaires

## déclarer les types d'échantillons

![[Pasted image 20261001101434.png]]

La partie haute de l'onglet affiche la liste des échantillons déjà déclarés. Pour chaque type d'échantillon, indiquez :

- le type. La liste proposée est construite à partir des types déclarés dans la collection 
- l'ordre de tri : c'est l'ordre dans lequel les échantillons seront proposés dans le formulaire
- préfixe utilisé pour générer l'identifiant métier : c'est le préfixe qui sera ajouté à l'information saisie par l'utilisateur, et qui permettra d'identifier l'échantillon
- enfin, indiquez si vous autorisez l'ajout de photos, vidéos ou enregistrements sonores à vos échantillons.
## Ajouter des informations complémentaires

![[Pasted image 20261001102418.png]]

trois types d'informations vont pouvoir être ajoutées à votre formulaire :

- si vous utilisez des identifiants secondaires qui seront saisis sur le terrain, vous pouvez les sélectionner
- si les stations sur lesquelles vous avez prévu les prélèvements sont déclarées, vous pouvez également les indiquer
- enfin, la liste des référents des échantillons permettra d'indiquer quel référent sera associé aux échantillons saisis. Attention : on ne pourra saisir qu'un seul référent par échantillon, à choisir parmi la liste.

## Calculer le formulaire

Une fois que vous aurez renseigné les types d'échantillons et les informations complémentaires, vous pourrez déclencher le calcul du formulaire. Une fois le calcul effectué, deux nouveaux onglets sont disponibles : 

- lignes du formulaire : c'est l'ensemble des lignes du formulaire qui seront insérées dans la feuille Excel, dans l'onglet *survey*
- choix : ce sont les listes de choix qui sont nécessaires à l'affichage du formulaire. Elles seront insérées dans l'onglet *choices* de la feuille Excel

Pour chaque type d'échantillon, le logiciel va préparer les champs permettant de saisir l'ensemble des informations associées, que ce soit :
- la quantité récoltée
- toutes les métadonnées, en tenant compte des différents types possibles. Par exemple, les listes de sélection que vous auriez pu déclarer sont enregistrées dans l'onglet *choix*

Vous retrouverez la plupart des colonnes qui sont utilisables dans le formulaire Excel :

![[Pasted image 20261001103552.png]]

L'ordre d'affichage tient compte de l'ordre de déclaration des types d'échantillons et de l'ordre des métadonnées dans le modèle associé. Les métadonnées déclarées obligatoires dans le modèle sont également marquées comme obligatoires dans le formulaire.

Vous pourrez modifier quasiment toutes les informations, et notamment l'apparence, à l'exception du type et du nom technique.

**Attention** : si vous relancez le calcul du formulaire, toutes les modifications que vous pourriez avoir apporter seront perdues !

L'onglet *choix* n'est pas modifiable. Vous pourrez simplement consulter ce que le logiciel a récupéré comme informations, à partir des saisies réalisées au préalable :

![[Pasted image 20261001104053.png]]

Les choix associés aux métadonnées sont préfixées par md_. 

## Générer la feuille de calcul

Une fois vos saisies terminées, vous pouvez déclencher la génération de la feuille de calcul. Le logiciel va créer un fichier Excel comprenant trois onglets : survey, choices et settings.

