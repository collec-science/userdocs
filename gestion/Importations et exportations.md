---
title: Importations et exportations
authors: Éric Quinton
license: CC-BY
tags:
  - import
  - export
created: 19/08/2025
---
Collec-Science dispose de nombreuses fonctionnalités permettant soit d'importer des échantillons ou des contenants, soit de les exporter dans différents formats.

Parmi les fonctionnalités les plus utilisées, vous avez la possibilité d'importer de nouveaux contenants ou de nouveaux échantillons à partir d'un fichier au format CSV. Le logiciel dispose d'un module qui vous permettra de préparer ce fichier en positionnant les bonnes colonnes : [[Générer le modèle pour les importations de masse]]. Les règles appliquées pendant l'importation sont décrites ici : [[Importer des échantillons ou des contenants]].

**Attention :** ce module ne fonctionne qu'en mode *création*, vous ne pourrez pas modifier vos contenants ou vos échantillons à partir de ce fichier une fois que vous l'aurez traité !

Mais si vous avez besoin de modifier globalement toute une liste d'échantillons, vous pourrez alors les exporter, les modifier avec un tableur comme LibreOffice Calc, puis les réimporter : [[Importer des échantillons externes ou modifier les échantillons avec un logiciel tiers]].

Avec ce module, vous pourrez également importer dans votre instance Collec-Science des échantillons qui auraient été saisis dans une autre instance. Divers mécanismes intégrés permettent de conserver les étiquettes qui auraient été apposées sur vos échantillons préalablement.

Un autre cas de figure intéressant : vous avez créé des échantillons, rangés dans une boite, et vous souhaitez les transmettre à un autre laboratoire pour analyse (ou autre). Si ce laboratoire est également équipé de Collec-Science, vous pourrez lui transmettre un fichier généré à partir de la liste des contenants qui, pour un contenant donné, contiendra tout ce qu'il contient, que ce soit des échantillons ou d'autres contenants et les échantillons qu'ils contiennent (c'est récursif). Pour exporter vos contenants : [[Exporter les contenants avec leur contenu vers une autre instance Collec-Science]], et pour les importer dans la nouvelle instance : [[Importer des contenants avec leur contenu à partir d'un fichier JSON]].

Enfin, vous pourriez souhaiter réaliser des exportations à façon, en indiquant quelles colonnes vous souhaitez transférer, voire créer des exportations complexes, par exemple compatibles avec le format demandé par le GBIF  *Global Biodiversity Information Facility* (https://www.gbif.org/fr/).
Collec-Science vous permet de créer des modèles d'exportation : [[Préparer un modèle d'exportation]]. Avec ce module, vous pourrez même remplacer certains libellés par d'autres, solution utile pour remplacer certaines codifications par celles attendues.
Un modèle, fourni à partir de la version v26.2.0 de Collec-Science, vous permet ainsi d'exporter des échantillons vers le logiciel ElabFTW, un logiciel de gestion de cahiers de laboratoires électroniques : [[Exporter des échantillons vers ElabFTW]].
Ces modèles fonctionnent à partir de lots d'échantillons, que vous pourrez créer à partir de la liste des échantillons : cela vous permettra de transférer vos échantillons dans des formats différents à partir du même lot. La création des lots d'échantillons est décrit ici, [[Les opérations globales sur les échantillons]], rubrique *Créer un lot d'export*.

