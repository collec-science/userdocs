---
title: Gérer les droits
authors: Éric Quinton
license: CC-BY
tags:
  - droits
created: 19/08/2025
---
La gestion des droits repose sur des groupes d'utilisateurs ([[Les groupes d'utilisateurs]]), qui sont définis par les administrateurs. 

Collec-Science met en œuvre plusieurs mécanismes pour gérer les droits d'accès :

- des droits généraux, qui définissent les modules que l'utilisateur peut appeler :
	- #admin pour l'accès aux fonctions d'administration
	- #param pour définir les paramètres généraux
	- #collection pour pouvoir créer des collections, créer des types d'échantillons, etc.
	- #import pour importer des données dans une collection
	- #manage (gestion) pour pouvoir modifier des échantillons, créer des mouvements, etc.
	- #consult pour afficher les informations, sans pouvoir opérer de modifications.
- des droits attribués à des #collections : seuls les membres des groupes rattachés à une collection pourront modifier les échantillons correspondants ou visualiser les métadonnées.
- des droits attribués à des #campagnes ([[Les campagnes]]). Si un échantillon est rattaché à une campagne et que des groupes d'utilisateurs sont définis pour celle-ci, seuls les membres de cette campagne pourront modifier l'échantillon, sous réserve que ceux-ci soient également rattachés à la collection considérée :
![[droits par campagne.png]]