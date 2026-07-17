---
title: Régénérer les modèles de métadonnées ou renommer un champ
authors: Éric Quinton
license: CC-BY
tags:
  - maintenance
  - métadonnées
created: 17/07/2026
---
Les modèles de métadonnées sont stockés dans un format spécial, le format JSON. Leur gestion a évolué depuis la création du logiciel, et l'outil utilisé historiquement pour les déclarer a été remplacé en 2025.

Le format des modèles a légèrement évolué lors du remplacement de l'outil de saisie : certains d'entre eux sont devenus incompatibles avec la version actuelle de Collec-Science.
De plus, des bugs ont été découverts dans ce nouveau module, rendant instables les modèles créés avant la version v26.2.0. 

De plus, lors de la création d'un champ de métadonnées, si ce champ est marqué comme utilisable pour les recherches, un index particulier est créé qui va permettre d'interroger beaucoup plus rapidement la base de données.

Enfin, en raison de la gestion particulière des métadonnées et leur stockage au format JSON, renommer un champ de métadonnées est une opération complexe, qui impose de réaliser l'opération non seulement dans le modèle, mais également dans l'ensemble des échantillons qui l'utilisent.

Collec-Science dispose d'outils qui permettent de régénérer les modèles pour les remettre dans le format attendu, de recréer les index et enfin de renommer un champ.

## Régénérer les modèles

Depuis le menu, choisissez *Paramètres > métadonnées*. En bas de la liste, dans le cadre *Régénérer les modèles*, choisissez l'opération *Régénérer les modèles*.

![[Pasted image 20260717153223.png]]

Les modèles vont être parcourus et être réécrits correctement au format JSON.

## Régénérer les index des échantillons

À partir du même cadre que précédemment, choisissez *Régénérer les index de la table des échantillons*. L'ensemble des index qui portent sur les échantillons vont être recréés. 

Cette opération n'est en principe pas nécessaire, sauf si des doutes quant à l'intégrité de la base de données apparaissent.

## Renommer un champ de métadonnées

Si vous souhaitez modifier le nom d'un champ dans un modèle, le plus simple est de le faire directement par l'interface "classique" :

- allez dans le détail du modèle
- passez en mode modification du champ considéré
- renommez le champ

Au moment de l'enregistrement, les métadonnées de tous les échantillons qui utilisent ce modèle seront modifiées pour refléter le nouveau nom attribué.

Toutefois, si vous souhaitez modifier globalement le nom d'un champ et ce, quel que soit le modèle, l'opération peut vite être fastidieuse si vous avez déclaré de nombreux modèles.
Pour réaliser cette opération en une seule fois, depuis le menu, choisissez *Paramètres > métadonnées*. En bas de la liste, dans le cadre *Renommer un champ de métadonnées globalement*, indiquez l'ancien nom et le nouveau nom, et lancez l'opération. 

![[Pasted image 20260717154757.png]]
L'application va modifier à la fois les échantillons concernés et l'ensemble des modèles qui contiennent ce champ.
