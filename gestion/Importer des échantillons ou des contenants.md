---
title: Importer des échantillons ou des contenants
authors: Éric Quinton
license: CC-BY
tags:
created: 23/03/2026
---
Pour éviter de devoir créer manuellement les échantillons ou les contenants, plusieurs mécanismes d'importation sont proposés :

- un import de masse ([[L'import de masse]]), qui permet de créer des contenants ou des échantillons. Cet import est basé sur un fichier au format CSV, dont le format peut être généré par le logiciel ([[Générer le modèle pour les importations de masse]]). Cet import ne travaille qu'en mode "création" : il n'est pas possible de modifier des échantillons avec cette fonctionnalité ;
- un import d'échantillons externes ([[Importer des échantillons externes ou modifier les échantillons avec un logiciel tiers]]) : il s'agit d'une fonctionnalité qui permet, à partir d'un fichier généré depuis une autre instance de Collec-Science, d'intégrer dans sa propre instance ces échantillons. Cette fonctionnalité peut également être utilisée pour modifier des échantillons en dehors du logiciel ;
- un import de contenants avec les objets qu'ils contiennent : cette fonctionnalité permet d'envoyer un contenant et les échantillons qui y sont stockés à une autre instance Collec-Science. Le fichier généré est au format JSON, qui permet de stocker des informations hiérarchisées.
