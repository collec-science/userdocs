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

Cochez *Importer des contenants*. Vous pourrez alors indiquer :

- la collection de destination, si le contenant est exclusivement attaché à une collection. Cette information ne sert que pour retrouver les contenants plus facilement ;
- le type de contenant (à partir de la famille) : il vous permettra d'avoir le bon libellé dans la ligne d'exemple qui sera générée, mais vous pourrez bien évidemment renseigner n'importe quel type par la suite ;
- si vous souhaitez ranger les contenants dans d'autres contenants : dans ce cas, les colonnes *container_parent_identifier*, *container_column* et *container_line* seront rajoutées au fichier ;
- si vous voulez décrire les contenants avec la colonne *container_comment* ;
- si vous disposez déjà d'un identifiant de type #UUID pour vos contenants (générés en principe à partir d'une autre application).

N'oubliez pas d'indiquer les identifiants secondaires si nécessaire (cf. [[#Rajouter des identifiants secondaires]], ci-dessous).

Dans le modèle, une ligne d'exemple, prenant en compte le type de contenant, sera généré.
### Pour importer des échantillons

Cochez *Importer des échantillons*. Vous pourrez alors indiquer :

![[Pasted image 20260328154502.png]]

- la collection de destination. Si l'information est obligatoire, rien ne vous empêche de la modifier ensuite quand vous remplirez le fichier ;
- le ou les types d'échantillons visés. C'est une information essentielle pour préparer le fichier ! En effet, en fonction des types d'échantillons, les colonnes de métadonnées correspondantes seront rajoutées. Si vous n'indiquez pas de type d'échantillon, aucune colonne ne sera ajoutée pour permettre l'importation d'un échantillon.
- le référent, qui sera proposé, dans les lignes d'exemple, sous la forme *Nom prénom*.
- les pays de collecte et de provenance, informations utiles si vos échantillons sont soumis au protocole de Nagoya ;
- la campagne de prélèvement, si besoin était ;
- le lieu de prélèvement ;
- d'autres colonnes supplémentaires peuvent être ajoutées :
	- la date d'expiration de l'échantillon, qui devra être renseignée sous la forme *jj/mm/aaaa* ;
	- l'identifiant dans la base de données d'origine. En principe, cet identifiant doit être construit sous la forme *sigle:numéro*, le sigle correspondant au code de la base de données. Pour un échantillon provenant d'une autre instance de Collec-Science, le numéro correspond à l'UID de la base de données d'origine ;
	- si vous cochez *rangement de l'échantillon dans un contenant*,  les colonnes *container_parent_identifier*, *sample_column* et *sample_line* seront rajoutées au fichier. Si vous avez également sélectionné l'importation d'un contenant, la colonne *container_parent_identifier* contiendra, dans les lignes d'exemple, l'identifiant métier du contenant d'exemple ajouté également dans le fichier ;
	- *échantillon dérivé* : la colonne *sample_parent_identifier* va être rajoutée, pour pouvoir indiquer l'identifiant métier du parent. Le parent doit soit exister au préalable, soit figurer plus haut dans le fichier ;
	- *échantillon composé* : si vous créez un échantillon composé, vous devrez indiquer dans la colonne *composite_parents_identifier* qui va être rajoutée au fichier l'ensemble des identifiants métiers des parents, séparés par une virgule ;
	- *localisation GPS* : les colonnes *wgs84_x* et *wgs84_y* seront rajoutées. Les coordonnées devront être indiquées sous forme numérique, avec le point comme séparateur décimal ;
	- si l'échantillon possède déjà un identifiant de type #UUID (généré à partir d'une autre application ou d'une autre instance Collec-Science), vous pourrez l'indiquer ici.


Une ligne d'exemple par type d'échantillon sélectionné sera rajoutée au fichier. Si des métadonnées sont obligatoires, vous retrouverez sur cette ligne d'exemple le terme *obligatoire* dans la colonne correspondante.

N'oubliez pas d'indiquer les identifiants secondaires si nécessaire (cf. [[#Rajouter des identifiants secondaires]], ci-dessous).
### Rajouter des identifiants secondaires

![[Pasted image 20260328161608.png]]

Si vous souhaitez indiquer des identifiants secondaires, tant pour vos contenants que pour vos échantillons, vous pourrez les sélectionner dans la liste proposée dans *identifiants secondaires*. Une colonne sera créée avec comme entête le code de l'identifiant secondaire : dans l'exemple ci-dessus, si vous aviez sélectionné *tag (pittag)*, la colonne *tag* aurait été rajoutée.

Attention : seuls les identifiants secondaires qui possèdent un *code* seront affichés dans cette liste.
