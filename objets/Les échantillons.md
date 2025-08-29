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
- un type
- une date d'échantillonnage, une date d'expiration, une date de création dans Collec-Science
- des #métadonnées ([[Les métadonnées]]): ce sont des informations complémentaires qui permettent de caractériser l'échantillon (par exemple, le taxon, les profondeurs des carottes sédimentaires, etc.)
Les échantillons peuvent être composés de plusieurs éléments, qui vont être utilisés pour réaliser du sous-échantillonnage (notion d’aliquote en chimie).
Enfin, un échantillon peut être subdivisé en d'autres échantillons (notion d'échantillon dérivé), voire être composé de plusieurs échantillons (après sous-échantillonnage).
## Les types d'échantillon
Chaque échantillon est rattaché à un type, qui le définit. Les types d'échantillons permettent d'indiquer :
- ce que contient le sous-échantillonnage (liquide, écailles de poisson)
- l'unité utilisée pour caractériser le nombre d'éléments composant le sous-échantillonnage
- le modèle de #métadonnées utilisé ([[Les métadonnées]])
Il est également possible de rattacher un type de #contenant ( [[Les contenants et le stockage]]) à un type d'échantillons. Dans la plupart des cas, les échantillons ne sont pas dissociables de leur contenant : un sachet d'écailles de poisson est manipulé par le sachet, c'est sur celui-ci qu'on va coller une étiquette, et pas directement sur l'écaille. Il en est de même pour tout ce qui est stocké dans un tube, dans une boite, etc. En associant le type d'échantillon avec le type de contenant utilisé, cela va permettre de récupérer les informations spécifiques au type de stockage, les produits utilisés, les risques associés à sa manipulation, etc.

## La transformation des échantillons
![[échantillons dérivés.png]]
### Les échantillons dérivés
À partir d'un échantillon, il est possible de créer des échantillons dérivés, soit directement, soit au moment du sous-échantillonnage.
Les échantillons dérivés peuvent être d'un type différent de l'échantillon parent, voire être rattachés à une autre collection.
### Les échantillons composés
À partir du sous-échantillonnage de plusieurs échantillons différents, il est possible de créer un nouvel échantillon, dit *échantillon composé*. Ce type d'échantillon est utilisé pour réaliser des analyses globales pour rechercher des occurrences rares d'un paramètre, avant de rechercher plus finement l'échantillon qui le porte.
Les échantillons composés peuvent être créés soit depuis le détail d'un échantillon lors de la réalisation d'un sous-échantillonnage, soit depuis la liste des échantillons : il faut alors que la quantité prélevée soit identique pour chaque échantillon parent. Il est toujours possible de rattacher un échantillon composé déjà existant à un sous-échantillonnage réalisé sur un autre échantillon parent.