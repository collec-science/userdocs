---
title: Les différents types de droits
authors: Éric Quinton
license: CC-BY
tags:
  - droits
  - admin
created: 19/08/2025
---
Collec-Science gère 6 droits différents :

- admin
- param
- collection
- import
- manage (gestion)
- consult

Ces droits sont attribués à des groupes d'utilisateurs ([[Les groupes d'utilisateurs]]) du même nom, et permettent d'accéder aux divers modules du logiciel, selon le tableau suivant :


| Fonction générale dans le logiciel                                                                | admin | param | collection | import | manage (gestion) | consult |
| ------------------------------------------------------------------------------------------------- | :---: | :---: | :--------: | :----: | :--------------: | :-----: |
| Gérer les utilisateurs : créer les comptes, gérer les groupes, etc.                               |   X   |       |            |        |                  |         |
| Accéder aux fonction d'administration (sauvegarde, consultation des logs, etc.)                   |   X   |       |            |        |                  |         |
| Définir les paramètres de fonctionnement de l'application (paramètres stockés en base de données) |   X   |       |            |        |                  |         |
| Accéder à l'ensemble des paramétrages dans le logiciel, sauf ce qui dépend du droit *admin*       |       |   X   |            |        |                  |         |
| Créer des requêtes SQL (module de requête)                                                        |       |   X   |            |        |                  |         |
| Exécuter des requêtes SQL                                                                         |       |   X   |     X      |  X\*   |       X\*        |         |
| Créer des collections                                                                             |       |   X   |            |        |                  |         |
| Créer des types d'échantillons, des types de contenants, des campagnes de prélèvements, etc.      |       |   X   |     X      |        |                  |         |
| Réaliser des opérations sur des lots d'échantillons ou de contenants                              |       |   X   |    X\*     |        |                  |         |
| Importer des échantillons                                                                         |       |   X   |    X\*     |  X\*   |                  |         |
| Créer des contenants ou des échantillons                                                          |       |   X   |    X\*     |  X\*   |       X\*        |         |
| Créer des mouvements                                                                              |       |   X   |     X      |   X    |        X         |         |
| Consulter les échantillons ou les contenants                                                      |       |   X   |     X      |   X    |        X         |    X    |

\* : nécessite des droits sur les collections considérées

## Le droit *admin*

Il permet de créer les utilisateurs, d'attribuer les droits, de paramétrer les données générales du logiciel, de consulter les traces, de réaliser une sauvegarde ponctuelle de la base de données.

Il est indépendant des autres droits. Il est en général détenu par les administrateurs du système.

## Le droit *param*

C'est le super-utilisateur de l'application. Il peut tout faire dans le logiciel, sauf ce qui est dévolu au droit *admin*, et en particulier :

- la modification de l'ensemble des tables de paramètres
- la création des collections.

En général, le détenteur du droit *param* devrait également posséder le droit *admin* (l'inverse n'est pas forcément vrai).

## Le droit *collection*

C'est un droit attribué aux administrateurs des collections. Ils peuvent modifier la plupart des paramètres comme créer des types d'échantillons, des modèles de métadonnées, etc., et réaliser des importations pour les collections auxquelles ils appartiennent.

## Le droit *import*

Il permet d'importer des échantillons pour les collections auxquelles appartient l'utilisateur concerné.

## Le droit *manage* (gestion)

C'est le droit de base pour les utilisateurs actifs dans le logiciel. Il permet de :

- créer/modifier des échantillons pour les collections auxquelles appartient l'utilisateur concerné
- enregistrer des mouvements d'entrée/sortie pour tous les échantillons, y compris ceux qui ne font pas partie de ses collections

Dès lors qu'un utilisateur est rattaché à une collection, il hérite automatiquement de ce droit.

## Le droit *consult*

Tout utilisateur disposant de ce droit peut visualiser les échantillons existants, mais ne peut pas consulter les métadonnées rattachées.


