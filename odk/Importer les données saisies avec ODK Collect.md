---
title: Importer les données saisies avec ODK Collect
authors: Éric Quinton
license: CC-BY
tags:
  - odk
  - import
created: 14/10/2026
---
- Vous avez créé un modèle de formulaire ODK ([[Générer le formulaire ODK]]), et l'avez publié sur une plate-forme ODK Central.
- Les formulaires ont été saisis depuis des terminaux Android avec ODK Collect. 
- Vous souhaitez maintenant importer les échantillons dans Collec-Science.

Voici les opérations à effectuer :

## Générer le fichier zip contenant les données

Depuis ODK Central, dans votre projet et votre formulaire et depuis l'onglet *Soumissions*, cliquez sur le bouton *Télécharger*.

![[odkcentral-generatefile.png]]

- cochez impérativement la case *Supprimer les noms de groupe*
- choisissez la rubrique *Toutes données et fichiers joints*.

Au moment du téléchargement dans votre ordinateur, assurez-vous que le nom du fichier ne soit pas modifié automatiquement par le navigateur, **conservez le nom d'origine**. Par exemple, si une première version existe, il peut rajouter un numéro de version pour ne pas écraser les téléchargements précédents.

Au moment de l'importation, le nom du fichier *zip* est utilisé pour retrouver les fichiers inclus, qui sont tous préfixés avec le même radical, à savoir le nom du fichier zip d'origine.

## Importer les échantillons

Dans Collec-Science, depuis le menu, choisissez *Imports/Exports > Importer les échantillons* (sous *Formulaires ODK*).

Sélectionnez le modèle qui vous a permis de générer le formulaire ODK, puis lancez l'importation.

Les échantillons vont être créés, les documents associés téléchargés. Notez les UID des échantillons traités, cela pourra vous faciliter la tâche si vous avez besoin de les retrouver ultérieurement. L'information est également  enregistré dans les logs, si besoin était.

Vous pouvez relancer l'importation : notamment si vous avez réalisé des modifications des déclarations dans ODK Central. Les échantillons seront simplement mis à jour. Toutefois, dans ce cas, les documents ne seront pas traités (ils existent en principe déjà).