---
title: L'import de masse
authors: Éric Quinton
license: CC-BY
tags:
  - import
  - échantillon
  - contenant
created: 23/03/2026
---
## Présentation

L'import de masse permet de créer des contenants ou des échantillons à partir d'un fichier au format CSV.

Le programme va travailler en deux phases. Dans un premier temps, il va vérifier la structure du fichier :
- toutes les colonnes présentes doivent être attendues : si une colonne ne correspond pas à la liste des colonnes prévues, l'opération échouera ;
- un certain nombre de contrôles de cohérence vont être réalisés, comme la vérification que le type d'échantillon existe bien dans la base de données, etc.

En cas de problème, le programme indiquera la ligne qui a généré une erreur, ainsi que le type d'erreur rencontrée.

Si les contrôles sont corrects, l'importation va être lancée. Le programme va traiter les lignes les unes après les autres. Il va également être capable de réaliser des opérations particulières :

- vous pourrez indiquer le nom d'un contenant où ranger l'objet que vous souhaitez créer. Le programme pourra ranger l'objet en cours de traitement dans un contenant qui aurait été déclaré précédemment dans le fichier ;
- vous pourrez également définir le parent d'un échantillon, sous réserve que celui-ci existe au préalable dans la base de données ou s'il a été défini précédemment dans le fichier. Cela fonctionne également pour les échantillons composés.

Même si le logiciel est capable de le gérer, évitez de saisir dans la même ligne un contenant et un échantillon (dans ce cas, l'échantillon sera "déplacé" dans le contenant créé). Il vaut mieux prévoir une ligne pour le contenant, puis une ligne pour l'échantillon.

Une fois l'importation achevée, le programme va afficher les UID mini et maxi des objets créés : notez ces informations, elles pourront vous être utiles pour retrouver vos contenants ou vos échantillons, particulièrement si vous vous rendez compte d'une erreur et que vous avez besoin de les supprimer pour les réimporter.

### Quel logiciel utiliser pour créer le fichier ?

Le logiciel préconisé est LibreOffice (https://fr.libreoffice.org/) : Microsoft Excel a tendance à modifier des caractères (des guillemets, par exemple) qui pourraient vous poser des problèmes par la suite ou à utiliser des encodages des caractères susceptibles de perturber l'importation.

Au moment d'enregistrer votre fichier (*Fichier > Enregistrer sous...*), sélectionnez le type (en bas à droite) **Texte CSV (.csv)**, et cochez **Éditer les paramètres du filtre**. Renseignez alors les paramètres suivants :

- jeu de caractères : Unicode (UTF-8)
- Séparateur de champ : virgule (la tabulation ou le point-virgule sont également acceptés)

![[Pasted image 20260324101905.png]]

### Existe-t-il un modèle de fichier ?

À partir de la version v26.1.0, le logiciel intègre un module qui vous permet de générer un modèle de fichier qui sera configuré en fonction de ce que vous voulez importer. Il tiendra compte de la collection, des types d'échantillons à créer et des métadonnées associées, des identifiants secondaires, etc.

Pour plus d'informations : [[Générer le modèle pour les importations de masse]].

## Les colonnes susceptibles d'être utilisées

### Pour créer un contenant

| Colonne                                             | Description                                                                                                                                                             |                             obligatoire                              |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------: |
| container_identifier                                | identifiant métier                                                                                                                                                      |                                  X                                   |
| container_type_id / container_type_name             | identifiant ou nom du type de contenant                                                                                                                                 |                                  X                                   |
| container_status_id / container_status_name         | Identifiant ou nom du statut                                                                                                                                            | Si le statut n'est pas indiqué, il sera positionné à 1 (état normal) |
| container_uuid                                      | Si le contenant a été généré à partir d'une autre application, et qu'il dispose de son propre UUID (identifiant universel), vous pouvez indiquer ici son UUID d'origine |                                                                      |
| container_collection_id / container_collection_name | Collection de rattachement du contenant. Cette information ne sert que pour rechercher plus facilement un contenant                                                     |                                                                      |
| container_comment                                   | Commentaire libre                                                                                                                                                       |                                                                      |
| container_parent_uid / container_parent_identifier  | UID ou identifiant métier du contenant où doit être rangé le contenant à créer                                                                                          |                                                                      |
| container_line / container_column                   | Numéro de ligne et de colonne où ranger le contenant, si le contenant cible dispose d'emplacements (boites à tubes, par exemple)                                        |                                                                      |
| referent_id / referent_name                         | Numéro informatique ou nom et prénom du référent                                                                                                                        |                                                                      |
| wgs84_x et wgs84_y                                  | point géographique (longitude, latitude) d'emplacement du contenant, sous forme numérique. Séparateur : point                                                           |                                                                      |

### Pour créer un échantillon


| Colonne                                              | Description                                                                                                                                                                                                                                             |                             Obligatoire                             |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |:-------------------------------------------------------------------:|
| sample_identifier                                    | Identifiant métier de l'échantillon                                                                                                                                                                                                                     |                                  X                                  |
| collection_id / collection_name                      | Numéro informatique ou nom de la collection d'appartenance de l'échantillon                                                                                                                                                                             |                                  X                                  |
| sample_type_id / sample_type_name                    | Numéro informatique ou nom du type d'échantillon                                                                                                                                                                                                        |                                  X                                  |
| sample_status_id  / sample_status_name               | Identifiant ou nom du statut                                                                                                                                                                                                                            | S'il n'est pas indiqué, le statut sera positionné à 1 (état normal) |
| campaign_id / campaign_name / campaign_uuid          | numéro informatique, nom ou UUID de la campagne de prélèvement de l'échantillon                                                                                                                                                                         |                                                                     |
| sampling_place_id / sampling_place_name              | numéro informatique ou nom du lieu de prélèvement                                                                                                                                                                                                       |                                                                     |
| country_code / country_name                          | code officiel (sur deux positions) ou nom du pays de collecte. Cette information peut être utilisée dans le cadre du protocole de Nagoya                                                                                                                |                                                                     |
| country_origin_code / country_origin_name            | code officiel (sur deux positions) ou nom du pays d'où provient l'échantillon. Il peut être différent du pays de collecte. C'est une information utilisable dans le cadre du protocole de Nagoya                                                        |                                                                     |
| referent_id / referent_name                          | Numéro informatique ou nom et prénom du référent                                                                                                                                                                                                        |                                                                     |
| wgs84_x et wgs84_y                                   | point géographique (longitude, latitude) de prélèvement de l'échantillon, sous forme numérique. Séparateur : point                                                                                                                                      |                                                                     |
| sampling_date                                        | Date de création ou d'échantillonnage de l'échantillon, sous la forme jj/mm/aaaa                                                                                                                                                                        |                                                                     |
| expiration_date                                      | Date d'expiration de l'échantillon, sous la forme jj/mm/aaaa                                                                                                                                                                                            |                                                                     |
| sample_multiple_value                                | le nombre total de sous-échantillons (ou le volume total, ou le pourcentage...) contenu dans l'échantillon si le type d'échantillons utilisé le permet (valeur numérique, séparateur décimal : point)                                                   |                                                                     |
| sample_multiple_real                                 | le nombre réel de sous-échantillons (ou le volume total, le pourcentage...) qu'il reste dans l'échantillon au moment de l'importation. Un sous-échantillonnage sera généré (différence entre sample_multiple_value et sample_multiple_real)             |                                                                     |
| sample_comment                                       | Description libre de l'échantillon                                                                                                                                                                                                                      |                                                                     |
| sample_parent_uid / sample_parent_identifier         | UID du parent de l'échantillon (doit exister avant l'importation) ou son identifiant métier. Dans ce cas, le parent peut figurer dans le même fichier, sous réserve qu'il soit placé avant                                                              |                                                                     |
| composite_parents_uid / composite_parents_identifier | dans le cas d'échantillons composés, les UID des parents (qui doivent exister avant l'importation) ou leurs identifiants métiers. Dans ce cas les parents doivent figurer avant dans le même fichier.<br>Chaque parent doit être séparé par une virgule |                                                                     |
| composite_multiple_value                             | quantité prélevée dans chaque parent pour créer l'échantillon composé. La quantité doit être identique pour chaque parent                                                                                                                               |                                                                     |
| dbuid_origin                                         | Identifiant technique dans la base de données d'origine (de préférence sous la forme : nom_base:id)                                                                                                                                                     |                                                                     |
| sample_uuid                                          | Si l'échantillon a été généré à partir d'une autre application, et qu'il dispose de son propre UUID (identifiant universel), vous pouvez indiquer ici son UUID d'origine                                                                                |                                                                     |
| container_parent_uid / container_parent_identifier   | UID ou identifiant métier du contenant où doit être rangé l'échantillon à créer                                                                                                                                                                         |                                                                     |
| sample_line / sample_column                          | Numéro de ligne et de colonne où ranger l'échantillon, si le contenant cible dispose d'emplacements (boites à tubes, par exemple)                                                                                                                       |                                                                     |

À ces informations, vous pourrez rajouter les métadonnées avec une colonne pour chaque type de métadonnée. Le nom des colonnes correspondantes doit être sous la forme **md_***nom_metadonnee***. Le programme reconstituera le format initial (format JSON). 

Si vous souhaitez fournir les métadonnées directement sous la forme JSON (par exemple : *{"taxon":"Alosa alosa"}*), utilisez la colonne *sample_metadata_json*. Néanmoins cette approche est déconseillée, en raison des difficultés de codage qu'elle peut comporter.

### Traitement des identifiants complémentaires

Si vous souhaitez rajouter des identifiants complémentaires, tant pour les contenants que pour les échantillons, ajoutez une colonne par type d'identifiant complémentaire. Le nom de la colonne doit impérativement être le *code* de l'identifiant (et pas son nom).

## Le traitement du fichier
### La phase de contrôle

Lorsque vous voulez importer un fichier, (*Imports/Exports > Import de masse*), le logiciel vous demande de sélectionner le fichier et de préciser certains paramètres : 

![[Pasted image 20260324102645.png]]

- séparateur : vous pouvez indiquer la virgule, le point-virgule ou la tabulation. Vérifiez que le séparateur soit cohérent avec ce que vous avez indiqué lorsque vous avez généré le fichier.
- Encodage du fichier : vous pouvez indiquer soit UTF-8 (format par défaut, conseillé) ou ISO-8859-x, format natif utilisé par les logiciels Microsoft. Dans ce second cas, les données seront réencodées avant traitement.
- Rechercher les échantillons parents uniquement dans la collection des enfants : si vous positionnez ce paramètre à *oui*, les parents doivent impérativement appartenir à la même collection que les enfants. C'est un paramètre qui peut être utile si des échantillons portent le même nom dans des collections différentes.

Le programme va lancer un certain nombre de vérifications :

- l'encodage du fichier indiqué va être comparé à celui qui semble avoir été utilisé pour générer le fichier ;
- le nom des colonnes va être vérifié. Si une colonne n'appartient pas à celles qui sont attendues, une erreur est générée ;
- les noms des types d'échantillons, types de contenants, etc. doivent exister dans la base de données ;
- la collection de destination doit faire partie des collections pour lesquelles l'utilisateur dispose des droits adéquats ;
- l'identifiant métier de l'échantillon ne doit pas exister dans la collection si celle-ci est paramétrée pour interdire les doublons d'identifiants métiers ;
- le format des dates doit être cohérent. Le logiciel attend des formats de type "français", c'est à dire sous la forme jj/mm/aaaa ;
- les métadonnées indiquées doivent exister pour le type d'échantillon considéré ;
- les champs attendus comme devant être numériques ;
- si un mouvement d'entrée dans un contenant est prévu, le programme va s'assurer que l'emplacement indiqué (ligne/colonne) ne soit pas plein ;
- enfin, les lignes sans identifiant métier, soit pour un contenant, soit pour un échantillon, sont signalées.

En cas d'anomalie détectée, le programme va afficher la liste des erreurs, en précisant le numéro de la ligne concerné :

![[Pasted image 20260324104920.png]]

Vous devrez corriger votre fichier et reprendre la procédure dès le début.
### La phase d'importation

Si les contrôles sont corrects, vous pourrez déclencher l'importation. Le programme va toutefois réaliser quelques contrôles complémentaires :

- les parents doivent exister dans la base de données avant l'importation, ou figurer plus haut dans le fichier d'import ;
- les contenants doivent également exister préalablement ou figurer plus haut dans le fichier d'importation.

Si une erreur survient, l'importation échouera dans sa globalité : aucun échantillon ou contenant ne sera créé, c'est du "tout ou rien". Le programme affichera alors une erreur du type :

![[Pasted image 20260324105515.png]]

L'importation devra être recommencée à zéro.

L'importation sera réalisée ainsi :

- si la colonne *sample_identifier* est renseignée, l'échantillon sera créé ;
- si la colonne *container_identifier* est renseignée, le contenant sera créé ;
- si la colonne *container_parent_identifier* (ou *container_parent_uid*, dans le cas où le contenant existe au préalable et son UID est connu), un mouvement d'entrée sera généré ;
- si les colonnes *sample_identifier* et *container_identifier* sont remplies sur la même ligne, l'échantillon sera rangé automatiquement dans le contenant figurant dans la même ligne. Toutefois, cette approche est déconseillée : il vaut mieux disposer d'une ligne différente pour les contenants et les échantillons, sachant que les mouvements d'entrée seront alors créés si la colonne *container_parent_identifier* est renseigné.

Si tout se passe bien, le programme affiche alors les UID minimum et maximum qui ont été générés :

![[Pasted image 20260324105732.png]]

Notez bien ces informations : si vous avez besoin de retrouver les objets que vous venez de créer, ce sera bien plus facile avec celles-ci.

Si vous ne les avez pas notées, vous pourrez toutefois les retrouver (ou les faire retrouver). Elles sont enregistrées dans les logs applicatives, consultables par un administrateur depuis le menu *Administration > Logs*. Voici un exemple des traces qui ont été enregistrées et qui correspondent à l'exemple précédent :

![[Pasted image 20260324110153.png]]
Deux mouvements ont également été générés pendant cette importation.

