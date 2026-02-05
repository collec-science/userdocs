---
title: Les échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - échantillon
created: 19/08/2025
---
![[échantillon.png]]
Les échantillons sont des #objets ([[Les objets dans Collec-Science]]), et héritent donc de l'ensemble de leurs propriétés.

Un échantillon est rattaché à une #collection (et à une seule). Il peut avoir été prélevé pendant une #campagne ([[Les campagnes]]), provenir d'un pays (soit le pays où il a été échantillonné, soit le pays qui l'a fourni dans le cadre des accords de Nagoya). La station de prélèvement a pu être déclarée dans le logiciel, pour faciliter les recherches.

Les échantillons sont caractérisés par :

- un type ;
- une date d'échantillonnage, une date d'expiration, une date de création dans Collec-Science ;
- des #métadonnées ([[Les métadonnées]]): ce sont des informations complémentaires qui permettent de caractériser l'échantillon (par exemple, le taxon, les profondeurs des carottes sédimentaires, etc.).

Les échantillons peuvent être composés de plusieurs éléments, qui vont être utilisés pour réaliser du sous-échantillonnage (notion d’aliquote en chimie).

Enfin, un échantillon peut être subdivisé en d'autres échantillons (notion d'échantillon dérivé), voire être composé de plusieurs échantillons (après sous-échantillonnage).
## Les types d'échantillon

Chaque échantillon est rattaché à un type, qui le définit. Les types d'échantillons permettent d'indiquer :

- ce que contient le sous-échantillonnage (liquide, écailles de poisson) ;
- l'unité utilisée pour caractériser le nombre d'éléments composant le sous-échantillonnage ;
- le modèle de #métadonnées utilisé ([[Les métadonnées]]).
- 
Il est également possible de rattacher un type de #contenant ( [[Les contenants et le stockage]]) à un type d'échantillons. Dans la plupart des cas, les échantillons ne sont pas dissociables de leur contenant : un sachet d'écailles de poisson est manipulé par le sachet, c'est sur celui-ci qu'on va coller une étiquette, et pas directement sur l'écaille. Il en est de même pour tout ce qui est stocké dans un tube, dans une boite, etc. En associant le type d'échantillon avec le type de contenant utilisé, cela va permettre de récupérer les informations spécifiques au type de stockage, les produits utilisés, les risques associés à sa manipulation, etc.

## La transformation des échantillons

![[échantillons dérivés.png]]
### Les échantillons dérivés

À partir d'un échantillon, il est possible de créer des échantillons dérivés, soit directement, soit au moment du sous-échantillonnage.

Les échantillons dérivés peuvent être d'un type différent de l'échantillon parent, voire être rattachés à une autre collection.
### Les échantillons composés

À partir du sous-échantillonnage de plusieurs échantillons différents, il est possible de créer un nouvel échantillon, dit *échantillon composé*. Ce type d'échantillon est utilisé pour réaliser des analyses globales pour rechercher des occurrences rares d'un paramètre, avant de rechercher plus finement l'échantillon qui le porte.

Les échantillons composés peuvent être créés soit depuis le détail d'un échantillon lors de la réalisation d'un sous-échantillonnage, soit depuis la liste des échantillons : il faut alors que la quantité prélevée soit identique pour chaque échantillon parent. Il est toujours possible de rattacher un échantillon composé déjà existant à un sous-échantillonnage réalisé sur un autre échantillon parent.

## La traçabilité des échantillons

À partir de la version v26.1.0, Collec-Science intègre des informations permettant de retracer l'historique des modifications d'un échantillon :

- la date de création et le login de l'utilisateur qui opère l'opération sont enregistrés ;
- toutes les modifications apportées soit aux données générales de l'échantillon, soit aux métadonnées, sont enregistrées, avec la date et le login concerné.

Techniquement, l'enregistrement des modifications est réalisé selon le protocole suivant :

- le login et la date de modification sont enregistrés ;
- les anciennes valeurs qui ont été modifiées sont également enregistrées, mais pas la nouvelle valeur saisie : c'est la valeur actuelle (ou celle qui aura été modifiée ultérieurement) ;
- si une valeur est saisie pour la première fois, l'information qui est enregistrée est que cette valeur est créée.

Ainsi, à partir des valeurs actuelles de l'échantillon, il est possible de reconstituer toutes les modifications apportées. Voici un exemple :

![[Pasted image 20260205103223.png]]

- La première ligne contient les valeurs actuelles. L'échantillon a été créé le 14/1/2026 à 9 heures 33 (c'est dans la ligne de commentaires, avant le tableau) ;
-  à 10:37 (dernière ligne), le référent a été ajouté ;
- à 10:38 (avant-dernière ligne), la date d'échantillonnage a été modifiée. Sa valeur initiale était au 14/1 ;
- diverses modifications, notamment dans les identifiants secondaires, ont été apportées (troisième et cinquième lignes) ;
- un mouvement d'entrée a été généré le 5/2 (seconde ligne). Les historiques des mouvements sont détaillés dans l'onglet *Mouvements*.

Ainsi, pour retrouver tout l'historique, il faut parcourir le tableau de bas en haut (ou inverser l'ordre de tri de la date).

L'historique n'est pas supprimable par l'utilisateur, sauf en cas de suppression de l'échantillon : toutes les informations le concernant sont alors effacées.

Actuellement, les événements, les documents associés ou les réservations ne font pas l'objet d'une conservation historique.
## Les droits d'accès

Collec-Science met en œuvre un certain nombre de mécanismes pour garantir que seuls les personnes autorisées puissent accéder à un échantillon.

Par défaut, seuls les utilisateurs disposant du droit *consult* ([[Les différents types de droits]]) peuvent consulter les échantillons, mais avec des restrictions : les documents, les métadonnées et l'historique de modification ne sont pas accessibles.

Pour pouvoir modifier un échantillon ou consulter les informations masquées (documents, métadonnées, historique), il faut disposer du droit *manage* (ou *gestion*) et, en même temps, faire partie d'un groupe d'utilisateurs ([[Les groupes d'utilisateurs]]) associé à la collection d'appartenance de l'échantillon.

Toutefois, si l'échantillon a été rattaché également à une campagne, et qu'un ou plusieurs groupes sont rattachés à celle-ci, l'utilisateur ne pourra accéder aux informations masquées ou modifier l'échantillon s'il fait également partie d'un des groupes associé à la campagne.

Concernant les informations masquées, il est toutefois possible de les rendre accessibles à tous les détenteurs du droit *consult* : il faut alors modifier le paramètre *consultSeesAll* dans les paramètres généraux ([[Les paramètres généraux de l'application]]). Dans ce cas, aucune information confidentielle ne pourra être stockée dans le logiciel sans qu'elle soit accessible à tous ceux qui peuvent se connecter.