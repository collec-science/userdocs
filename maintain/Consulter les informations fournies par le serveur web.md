---
title: Consulter les informations fournies par le serveur web
authors: Éric Quinton
license: CC-BY
tags:
  - admin
created: 16/07/2026
---
Le serveur web est l'application qui exécute le programme Collec-Science et envoie les pages web vers le navigateur. Plusieurs informations techniques sont disponibles et permettent d'aider au diagnostic de problèmes divers, que ce soit de configuration ou de fonctionnement de l'application.

Ces informations ne sont accessibles qu'aux utilisateurs qui disposent du droit *admin* (*cf.* [[Les différents types de droits]]).

## Les variables fournies par le serveur web

Ces variables sont transmises par le serveur web à l'application. Elles permettent notamment de connaître l'adresse du client (l'adresse IP de l'utilisateur) et diverses informations techniques. Elles sont utiles pour vérifier la configuration du serveur. Elles contiennent également des informations sur le paramétrage des variables d'environnement de l'application (fichier .env). Pour plus d'informations concernant ce fichier .env,  vous pouvez consulter cette documentation : https://equinton.github.io/ppcidocs/fr/parameters.html.

Pour visualiser ces variables, depuis le menu, choisissez *Administration > Variables SERVER*.

Parmi ces variables, certaines peuvent faciliter le diagnostic :

- database.default.xxxx : paramètres de connexion à la base de données
- BASE_DIR : dossier d'installation de Collec-Science
- envPath : dossier où se situe le fichier .env. Cette variable est particulièrement importante dans le cas où le serveur fonctionne en mode *multi-instances*, c'est à dire où plusieurs instances se partagent la même application. Pour plus d'informations sur le mode *multi-instances*, consultez https://github.com/collec-science/multi-instances
- HTTP_HOST : adresse du serveur
- HTTP_COOKIE : liste des cookies transmis au serveur

## Les variables de session

Le protocole HTTP, qui est utilisé par le serveur web, fonctionne dans un mode dit "sans état", c'est à dire que chaque page est indépendante de la précédente. Pour pouvoir conserver les informations d'une page à l'autre, le serveur utilise des variables dites *de session*, qui sont spécifiques à l'utilisateur. 

Quand l'utilisateur se déconnecte de l'application, ces variables sont effacées. De même, sans interaction avec le logiciel pendant 4 heures, elles sont également effacées.

Leur visualisation permet de vérifier un certain nombre de paramètres liés à l'utilisateur, comme la liste des collections qui lui sont associées, par exemple. 

Pour visualiser ces variables, depuis le menu, choisissez *Administration > Variables SESSION*.

Parmi ces variables, certaines peuvent aider dans le diagnostic :

- collections : liste des collections attachées à l'utilisateur (*cf.* [[Les collections]])
- groupes : liste des groupes auquel appartient l'utilisateur (*cf.* [[Les groupes d'utilisateurs]])
- locale : la langue courante sélectionnée
- userRights : les droits accordés (*cf.* [[Gérer les droits]])

## La configuration de PHP

Collec-Science a été écrit avec le langage PHP. Pour fonctionner, différents ont besoin d'être activés.

Le détail de la configuration de PHP est consultable depuis le menu en choisissant *Administration > PHP info*.

Ces informations peuvent permettre de vérifier la configuration fine du serveur PHP : elles sont avant tout destinées aux administrateurs du serveur hébergeant l'application.