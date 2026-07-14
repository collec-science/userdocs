---
title: Consulter les logs et les fichiers des erreurs
authors: Éric Quinton
license: CC-BY
tags:
  - log
  - erreur
created: 14/07/2026
---
Collec-Science dispose de plusieurs mécanismes permettant d'enregistrer les opérations réalisées dans le logiciel : 

 - les opérations courantes, comme l'appel d'un module, la modification d'une fiche, etc., mais également le résultat des importations ou la connexion à l'application sont enregistrées dans une table de la base de données ;
 - les erreurs d'exécution sont également stockées dans des fichiers dédiés, gérés par le *framework* CodeIgniter (le moteur de l'application).
 - certaines anomalies, comme l'échec de la connexion, sont également enregistrées dans le système de gestion des traces (logs) du serveur qui héberge l'application (mécanisme *syslog*). Ce mécanisme, s'il continue à exister, est maintenant remplacé par le stockage dans les fichiers d'erreurs gérés par CodeIgniter, et devient obsolète.

## Accès aux traces

L'accès au traces n'est disponible que :

- pour les administrateurs de l'ordinateur qui héberge l'application et la base de données ;
- pour les utilisateurs disposant du droit *admin* (cf. [[Les différents types de droits]]): ils peuvent alors consulter les traces enregistrées dans la base de données ainsi que les fichiers contenant les erreurs enregistrées par CodeIgniter.
## Durée de conservation des traces

Les traces enregistrées soit dans la base de données, soit dans les fichiers gérés par CodeIgniter, sont supprimées automatiquement au bout d'une année (365 jours). Pour que la suppression soit effective, il faut toutefois que l'application soit utilisée, c'est l'utilisateur qui déclenche (de manière transparente et automatique) cette opération.

## Consulter les traces enregistrées en base de données

Depuis le menu, choisissez *Administration > Logs*.

![[Pasted image 20260714160636.png]]
Le nom des modules est celui qui est géré par l'application. À noter que ceux qui commencent par *App/Models* sont les enregistrements des écritures dans les tables de l'application, et ils contiennent normalement, dans la colonne *Commentaires*, l'identifiant de l'enregistrement modifié.

Vous pouvez réaliser une recherche par login ou par module. La liste des modules qui est affichée contient uniquement les modules qui ont été appelés dans l'intervalle de date.

Si vous souhaitez connaître la liste des connexions réalisées, vous pourrez interroger le module *col-loginExec*.

Dans certains cas de figure, les enregistrements réalisés le jour même n'apparaissent pas : vous les retrouverez en fixant la date *au :*  au lendemain.

Quelques traces intéressantes : 

- col-loginExec : la liste des connexions réalisées ;
- col-massImportDone : les informations liées à un import de masse (UID min et max, nombre de lignes traitées)
- col-externalImportDone : idem, mais pour l'importation d'échantillons externes

Avec ce module, vous pouvez également rechercher toutes les opérations réalisées par un utilisateur, mais uniquement pendant l'année écoulée.

## Consulter les erreurs enregistrées dans les fichiers de traces de l'application

Les traces sont enregistrées automatiquement par le *framework* CodeIgniter dans le sous-dossier de l'application *writable/logs*. 

Les administrateurs de l'application peuvent également les consulter depuis l'application, à partir du menu *Administration > Trace des erreurs* :

![[Pasted image 20260714162134.png]]

Un fichier est créé par jour.

En cliquant sur un des fichiers, vous accéderez aux données enregistrées. Deux types d'informations différentes sont enregistrées :

- les messages d'erreur générés par l'application (en rouge). Par exemple, voici le contenu correspondant à problème au moment de l'importation d'un fichier (ici, le séparateur de colonne n'était pas correct) :

![[Pasted image 20260714162418.png]]

Vous retrouvez, après la date, l'adresse appelée, puis le message d'erreur qui a été affiché.

- les messages d'erreur résultant d'une erreur d'exécution, en général un bug dans le logiciel :

![[Pasted image 20260714162638.png]]

Ces informations sont cruciales pour permettre la correction du bug, elles permettent de repérer le code qui a généré l'erreur (ici, c'est la ligne 164 du fichier Models/Export.php qui pose problème).

Si vous détectez ce type de messages, n'hésitez-pas à déclarer un incident ici : https://github.com/collec-science/collec-science/issues/new/choose

