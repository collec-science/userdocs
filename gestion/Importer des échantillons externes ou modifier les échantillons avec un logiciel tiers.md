---
title: Importer des échantillons externes ou modifier les échantillons avec un logiciel tiers
authors: Éric Quinton
license: CC-BY
tags:
  - import
created: 9/6/2026
---
Un mécanisme est prévu dans Collec-Science pour pouvoir échanger des échantillons entre deux instances :

- un fichier au format CSV est généré depuis l'instance initiale, depuis la liste des échantillons ;
- ce fichier va pouvoir être importé dans la nouvelle instance.

Le mécanisme mis en œuvre permet de conserver les étiquettes générées dans la première instance, et notamment les Qrcodes. Si l'échantillon sera enregistré dans la nouvelle instance avec un UID "local", il conservera son UID d'origine (dans un champ dédié), associé au code de l'instance initiale.

Concernant les tables de paramètres (stations, campagnes, etc.), au moment de l'importation, le logiciel va essayer de retrouver les informations transmises dans la nouvelle base de données. Il sera alors possible de réaliser un appariement manuel, pour faire coïncider des informations équivalentes.

Enfin, ce module travaille en mode "modification" : il est ainsi possible de réimporter des échantillons déjà importés (ou existants). C'est une fonctionnalité que vous pourrez utiliser si vous souhaitez modifier une liste d'échantillons en dehors du logiciel, par exemple avec un tableur. Vous pourrez alors :

- exporter les échantillons concernés ;
- les modifier dans votre tableur ;
- les réimporter en utilisant ce module.

## Exporter les échantillons

Depuis la liste des échantillons, cochez les échantillons que vous souhaitez exporter, puis cliquez sur le bouton *Export vers une autre base*.

Toutes les informations concernant les échantillons vont être insérées dans un fichier csv, avec quelques particularités :
- seuls les libellés des tables de paramètres sont conservées
- si la colonne *dbuid_origin* est vide, celle-ci sera renseignée avec l'information *db:uid*, où *db* correspond au code de l'instance et *uid* au numéro informatique de l'échantillon. C'est cette colonne qui est utilisée pour pouvoir lire les étiquettes générées depuis une autre instance
- les métadonnées sont exportées sous deux formes :
	- une forme "brute", qui contient les informations au format JSON 
	- une colonne par métadonnée, préfixée par *md_*.
- si l'échantillon a subi des événements, ceux-ci sont insérés dans une colonne "history" au format JSON, avec le code de l'instance, le type de l'événement, sa date, et le commentaire ;
- si l'échantillon a un ou plusieurs parents (échantillons composés), ceux-ci sont également insérés dans la colonne "history". Dans ce cas, le type correspondra au type d'échantillon.

### Structure de la colonne *history*

Le contenu de la colonne *history* sera utilisé pour afficher les parents ou les événements survenus avant l'importation de l'échantillon dans la nouvelle instance. Elle contient les informations au format JSON, avec une occurrence par parent ou par événement. Voici sa structure :

| item     | contenu pour un événement         | contenu pour un parent |
| -------- | --------------------------------- | ---------------------- |
| dborigin | code de l'instance d'origine      | idem                   |
| type     | event                             | parent                 |
| date     | date de l'événement               |                        |
| name     | Type de l'événement               | identifiant métier     |
| comment  | commentaire associé à l'événement | type de l'échantillon  |

## Importer les échantillons

L'importation va être réalisée en deux temps :

- le fichier va d'abord être vérifié (nom des colonnes, vérifications générales) ;
- la liste des paramètres associés aux échantillons va être affichée avec, pour chaque paramètre, la possibilité de choisir celui qui correspond le mieux dans l'instance courante. Par défaut, le logiciel positionne les listes sur le bon paramètre, s'il est identique.

Pour lancer l'importation, depuis le menu, choisissez *Imports/Exports > Import d'échantillons externes* :

![[Pasted image 20260611143911.png]]

Une fois envoyé au serveur, le logiciel va vérifier la structure du fichier et tenter de réaliser les appariements :

![[Pasted image 20260611144156.png]]
Si un libellé ne trouve pas de correspondance, vous devrez ajouter une entrée correspondante dans les tables de paramètres, ou créer un paramètre "inconnu", si besoin était, puis relancer toute la procédure.

Une fois l'importation déclenchée, l'application affichera les UID mini et maxi qui auront été traités, soit les UID créés en cas de réelle importation depuis une autre instance, soit ceux qui auront été modifiés en cas de modification des échantillons de l'instance courante avec un logiciel tiers.