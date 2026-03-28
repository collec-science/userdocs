---
title: Le lexique
authors: Éric Quinton
license: CC-BY
tags:
  - lexique
created: 28/03/2026
---
#accuracy : Précision de la localisation d'un échantillon, en mètres

#authorization : Les campagnes de prélèvement peuvent nécessiter des autorisations. Il est possible d'indiquer, réglementation par réglementation, le numéro et la date de l'autorisation

#campaign ou #campagne : Les échantillons peuvent être récoltés pendant des campagnes de prélèvement. Il est possible de définir, pour une campagne, les réglementations applicables et les numéros d'autorisation en cas de décision officielle

#collection : une collection est un ensemble cohérent d'échantillons se rapportant à un sujet particulier. Les droits d'accès aux échantillons sont gérés par collection. Il est également possible de leur rattacher des lieux de prélèvement.

#composite ou échantillon composé : échantillon créé à partir de plusieurs échantillons différents

#container ou #contenant : tout objet qui peut en contenir un autre. À ne pas confondre avec les échantillons dérivés ou les sous-échantillons.

#container_family : grande catégorie de containers, pour faciliter la recherche (salle, site, caisse, bidon...)

#container_latlong : pour un local, un bâtiment, un site, etc., coordonnées WGS84 sous forme décimale

#container_type : type détaillé du #contenant, précisant la capacité, le produit de stockage ou les conditions de stockage le cas échéant, les risques associés en cas de manipulation, etc. Cela peut être un site, un bâtiment, une salle, une armoire, une étagère, une caisse, un bidon, un tube, etc. Lors de la création d'un type de container, il est possible d'indiquer le nombre d'emplacements disponibles (nombre de lignes ou de colonnes), qui contiendront un et un seul objet. C'est une notion qui prend tout son sens pour les boites contenant de multiples tubes, ou les armoires pour lesquelles on ne souhaite pas déclarer les étagères. Si rien n'est précisé, le nombre d'emplacements est au minimum de 1 (une ligne, une colonne, donnée obligatoire pour des raisons techniques). Les conteneurs sont définis indépendamment des collections.

#country ou pays de collecte : pays où l'échantillon a été récolté

#country_origin ou pays d'origine : pays qui a fourni l'échantillon (qui l'a récolté). Il peut être différent du pays de récolte

#dbuid : en saisie d'un échantillon, si celui-ci a été créé dans une autre base de données, il est possible d'indiquer le code de la base de données initiale suivi de l'identifiant attribué. Ce code sera alors utilisé lors des recherches, ce qui permet de conserver les étiquettes apposées initialement.

#event_type ou type d'événement : #événement qui peut survenir sur un échantillon ou sur un conteneur. L'événement peut être extérieur (par exemple conteneur cassé), volontaire (par exemple analyse) ou involontaire (par exemple échantillon perdu)

#filetype ou type de fichier : définit les types de fichiers que l'on peut importer dans les différents menus du logiciel. Pour connaitre les types MIME importants dans le cadre du WEB, vous pouvez consulter https://developer.mozilla.org/fr/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

#identifier_type ou type d'identifiant secondaire : il est possible de rattacher divers identifiants à un objet, par exemple des codes internationaux. Les types d'identifiant permettent de les décrire. S'ils ne sont pas numériques, ces identifiants peuvent en outre être utilisés dans les recherches ou lors des scans pour les entrées-sorties

 #étiquettes : les étiquettes peuvent être associées à des containers ou à des échantillons. Elles contiennent deux parties : un QRcode contenant des valeurs susceptibles d'être lues automatiquement et un contenu libre. Le QRcode général contient au minimum le uid et le db. Le QRcode particulier contient uniquement un numéro. Pour activer le cas particulier, il faut cliquer sur Etiquette ne comprenant qu'un identifiant métier

#metadata ou #métadonnées : des éléments (comme le nom des récolteurs, taxons, ...) que l'on souhaite ajouter à chaque échantillon d'une collection

#operation : une opération peut être décrite comme une action modifiant l'état d'un échantillon. Elle aboutit à la création d'un nouvel échantillon dérivé du précédent

#product ou #produit : produit utilisé pour conserver l'échantillon (par exemple éthanol). Appelé parfois produit de stockage dans la documentation

#protocole : protocole utilisé pour collecter les données. Un protocole est une suite d'opérations qui concourent à produire (voire à conserver) des échantillons utilisables pour la recherche. Il s'agit en principe d'un document qui décrit les différentes étapes que suit un prélèvement.

#référent : responsable d'une collection et/ou de l'échantillon et/ou du contenant. En général, le référent d'un contenant n'est renseigné que pour les pièces utilisées pour le stockage (c'est la personne qui dit où ranger les échantillons) ou les matériels techniques susceptibles de tomber en panne (par exemple le frigo)

#sample_derivated ou échantillon dérivé : échantillon créé à partir d'un autre, de même type ou non, identifié de manière autonome. Autrement dit, échantillon fils d'un autre. Par exemple, une section de carotte est dérivée de la demi-carotte X, qui dérive elle-même de la carotte entière.

#sample_empty ou échantillon vidé de son contenu : #statut d'un échantillon. Échantillon dont on a utilisé la totalité. Par exemple une carotte d'un mètre, 10 prélèvements de 10 cm, il ne reste plus rien de l'échantillon.

#sample_latlong : lieu où est prélevé l'échantillon. En fait, le point géographique associé à l'échantillon. Il peut être édité en cliquant dans la carte ou sur le lien *Repérez votre position !.* Cette action, si elle est réalisée sur le terrain, déclenchera l'enregistrement du lieu de création/collecte de l'échantillon

#sample_type ou type d'échantillon : permet de définir des types génériques - par type de conteneur (tube, sachet zip, ..) avec possibilité d'associer un modèle de métadonnées

#sampling_place ou site de collecte : lieu ou site où a été prélevé l'échantillon. Le site est en fait en général une façon de regrouper les échantillons vis à vis d'une organisation spatiale de la collecte. Cette notion n'a pas forcément besoin d'un géo-référencement précis, mais peut servir à codifier le nom de l'échantillon et peut aider le chercheur à définir comment il recherche/regroupe ses échantillons. Quand on sélectionne un lieu de prélèvement pour que la longitude et la latitude soient mises à jour au niveau de la fiche échantillon, il faut que la longitude et la latitude soient vides auparavant. A noter qu'il suffit de ne pas indiquer de collection pour que lieu de prélèvement soient disponibles pour toutes les collections

#statut : permet d'indiquer si un objet (échantillon ou container) est toujours utilisable. Les statuts peuvent être variés et dépendre du mode opératoire local (contenant cassé, échantillon qui ne contient plus de matière exploitable, etc.)

#storage_condition ou condition de stockage : caractéristiques principales du mode de conservation (froid, atmosphère contrôlée, lyophilisation, etc.). Peut également être utilisé pour décrire le traitement préalable de l'échantillon en vue de sa conservation.

#sous-échantillon : partie d'un échantillon non identifiable individuellement (prélèvement de x matière, une écaille parmi 10 identiques). En chimie, peut être assimilé à l’aliquote

#translationTable : Table permettant de remplacer les libellés présents dans la base de données par ceux attendus par le destinataire de l'export

#trashed ou mis à la corbeille : objet en attente de suppression (mis à la corbeille). Utilisé pour pouvoir indiquer à des services externes qu'un objet a été supprimé

#UUID : dentifiant stocké sur 36 caractères, qui est généré avec des fonctions cryptographiques qui le rendent unique, quel que soit le système qui l'a produit. Exemple : a95d8731-3501-4cc7-a71d-50ebd839b035. Il est utilisé pour faciliter les échanges entre bases de données, en lieu et place du couple Code de base de données:UID