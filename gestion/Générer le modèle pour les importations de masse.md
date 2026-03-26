---
title: Générer le modèle pour les importations de masse
authors: Éric Quinton
license: CC-BY
tags:
  - import
  - échantillon
  - contenant
created: 25/03/2026
---
## Présentation

L'importation de masse ([[L'import de masse]]) permet d'insérer des contenants ou des échantillons dans la base de données à partir d'un fichier CSV. Des contraintes fortes sont imposées concernant la structure de ce fichier, les colonnes doivent respecter une nomenclature, les informations relatives aux objets intégrés (type de contenant ou d'échantillon, collection de destination, etc.) doivent être conformes à ce qui existe dans la base de données.

Pour faciliter la création de ce fichier, un module a été ajouté à l'application (à partir de la version v26.1.0). Il permet de générer le canevas de ce fichier,  en tenant compte des informations que vous souhaitez intégrer. En particulier, dans le cas de l'importation d'échantillons, les colonnes correspondant aux métadonnées associées aux types d'échantillons sélectionnés seront automatiquement ajoutées.

Enfin, au delà de l'entête des colonnes, des lignes d'exemple sont ajoutées, pour faciliter le remplissage du fichier.

## Générer le fichier

Ouvrez la page depuis le menu *Imports/exports > Modèle d'import de masse* :

![[Pasted image 20260325104100.png]]

Vous pourrez décider d'importer des contenants, des échantillons où les deux à la fois.

### Pour importer des contenants

