---
title: Les groupes d'utilisateurs
authors: Éric Quinton
license: CC-BY
tags:
  - groupes
  - admin
created: 19/08/2025
---
Les droits gérés dans le logiciel sont attribués à des groupes d'utilisateurs. Les groupes sont gérés de manière hiérarchique : un utilisateur positionné dans un sous-groupe fera également partie du groupe parent.

Voici un exemple issu de l'instance de test :

![[Pasted image 20250826105113.png]]
Les utilisateurs déclarés dans le groupe *param* (207 actuellement) appartiennent également aux groupes *collection*, *manage* et *consult*. Le groupe *testapi*, qui contient des logins utilisés pour tester les API de l'application, hérite des droits attribués au groupe *manage* : les comptes peuvent réaliser des modifications dans la base de données.

Par convention, les droits gérés par le logiciel ([[Les différents types de droits]]) sont attribués aux groupes de même nom : le groupe *admin* dispose du droit *admin*, etc.
==Il est fortement déconseillé de modifier ces groupes de base== (admin, consult, manage, collection, param, import), même si c'est techniquement possible (*via* le menu *Administration > ACL - droits*). Si vous avez besoin de créer des groupes dédiés à certains utilisateurs, vous pouvez facilement rajouter des groupes fils par rapport aux groupes initiaux : ces nouveaux groupes hériteront des droits attribués aux groupes parents.

Vous avez également la possibilité de déplacer un groupe dans l'arborescence : ==ne le faites pas pour les groupes de base==, vous pourriez déclencher des dysfonctionnements dans le logiciel, voire le faire totalement "planter" si vous créez une boucle (un groupe fils devient le parent de son parent).

Les groupes sont utilisés non seulement pour l'accès aux différents modules de l'application, mais également pour attribuer les droits aux collections ([[Les collections]]) ou limiter l'accès aux informations ou la modification des échantillons pour les campagnes de prélèvement ([[Les campagnes]]).

## L'attribution automatique de groupes

Si vous utilisez une identification gérée par votre entreprise (annuaire LDAP, CAS, OIDC ou HEADER - fédération d'entreprise - cf. [[Les différents mécanismes pour s'identifier]]), il est possible de configurer le logiciel pour qu'il récupère automatiquement le groupe d'affectation de l'utilisateur.

Dans la copie d'écran précédente, le groupe **1454** correspond à une unité de recherche (l'unité INRAE EABX). Lorsque les membres de cette unité vont se connecter au logiciel , ce groupe sera récupéré depuis l'annuaire de l'entreprise, et ils disposeront automatiquement du droit *param* (attribué par le groupe *param*).