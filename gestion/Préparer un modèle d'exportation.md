---
title: Préparer un modèle d'exportation
authors: Éric Quinton
license: CC-BY
tags:
  - export
created: 22/6/2026
---
Les modèles d'exportations permettent de réaliser des exportations "à façon", c'est à dire adaptées aux systèmes informatiques qui vont accueillir les données. Le mécanisme général mis en place est le suivant :

![[lots pour exportation.png]]

Un modèle d'export contient un ou plusieurs modèles de jeux de données. Chaque jeu de données contient une liste d'informations à transférer. Le cas échéant, si les libellés doivent être transcodés pour être correctement compris par l'application cible, des traducteurs peuvent être utilisés pour transformer les informations avant leur transfert.

Une fois en possession d'un modèle d'export, vous pourrez générer un lot d'échantillons et l'associer à votre modèle pour générer automatiquement le fichier au format voulu (*cf. * [[Exporter les échantillons dans un format particulier]]).
## Créer les traducteurs

Les traducteurs servent à transformer un libellé présent dans la base de données pour qu'il corresponde à ce qui est attendu dans l'application destinataire.

Par exemple, si vous avez décrit une métadonnée de type *taxon*, avec une espèce de poisson *Alosa fallax* (alose feinte), et que c'est le libellé ALF qui est attendu, vous pourrez utiliser un traducteur pour réaliser la transformation.

Les traducteurs sont associés aux attributs transférés : ils sont donc utilisables pour tous les libellés transmis.

Pour créer un traducteur, choisissez, dans le menu, la rubrique *Imports/Exports > Traducteurs*, puis cliquez sur *Nouveau* :

![[Pasted image 20260622113538.png]]


## Créer un modèle de jeu de données

Les modèles de jeux de données permettent de décrire précisément les informations que vous souhaitez transmettre. Ils comprennent d'une part des informations générales qui permettent de décrire notamment le format attendu (csv, etc.) et d'autre part la liste des informations, dont les attributs, à transmettre.

Pour créer un nouveau modèle de jeu de données, depuis le menu, choisissez *Imports/Exports > Modèles de datasets*, puis cliquez sur *Nouveau...* :
![[Pasted image 20260622114207.png]]

Plusieurs informations sont nécessaires pour décrire le jeu de données :
- le nom, pour pouvoir le retrouver ensuite
- le type. Il permet d'indiquer ce qu'on souhaite transférer :
	- sample : le fichier contiendra un export des informations concernant les échantillons
	- collection : permet d'exporter les informations concernant la collection de rattachement des échantillons
	- document : la liste des documents attachés aux échantillon pourra être transmise, avec si nécessaire un lien web permettant de les télécharger directement
	- arbitrary content : permet de créer un fichier qui contient un texte particulier. C'est utilisé pour créer des fichiers xml ou json qui servent de "porte d'entrée" pour traiter les autres fichiers de l'export, dans le cas de structures complexes, comme celle du GBIF
	- elabftw : c'est un format d'export particulier, qui permet de transférer les échantillons vers le logiciel ElabFTW (cf. [[Exporter des échantillons vers ElabFTW]])
- le format d'export : vous pouvez indiquer soit CSV, soit XML, soit JSON
- le nom du fichier qui sera généré
- si le type de votre modèle est "document", vous pouvez choisir soit de générer une entrée pour chaque fichier attaché aux échantillons, soit uniquement le plus récent
- si le format d'export est CSV, vous pouvez indiquer le séparateur que vous souhaitez utiliser (virgule, point-virgule, tabulation)
- enfin, si vous souhaitez exporter au format XML, des informations complémentaires sont nécessaires :
	- l'entête du fichier XML, qui permettra de définir son contenu
	- le nom du nœud XML qui sera utilisé pour "boucler" sur les échantillons
	- la transformation XSL qui sera appliquée pour générer le contenu du fichier XML.

L'export au format XML est complexe à créer : référez-vous aux descriptions fournies par les destinataires de vos jeux de données pour savoir comment organiser votre fichier.

### Décrire les colonnes dans le modèle de jeu de données

Une fois le type de fichier défini, vous pourrez définir la liste des colonnes que vous souhaitez insérer dans votre fichier. La liste varie en fonction du type choisi : selon le type, les informations qui seront transférées ne seront pas identiques.

L'interface pour créer une nouvelle colonne est identique, seul la liste des colonnes va changer selon le type :

![[Pasted image 20260622121343.png]]

La fenêtre est organisée en deux parties : la partie haute permet de définir le contenu d'une colonne, et la partie basse contient la liste des colonnes déjà décrites.

Pour chaque colonne, vous pourrez indiquer :

- le nom de la colonne à exporter
- si vous choisissez une métadonnée (metadata) ou un identifiant secondaires (identifiers), vous devrez indiquer quelle métadonnée ou quel identifiant secondaire vous souhaitez exporter
- le nom que prendra la colonne exportée dans le fichier. Par défaut, le nom courant est proposé, mais vous pouvez le modifier si vous le souhaitez
- si vous avez défini une table de correspondance (*cf. supra*), vous pourrez l'indiquer. Les libellés seront alors traduits si le contenu correspond à une entrée décrite dans cette table
- pour éviter d'exporter des informations incomplètes, vous pouvez indiquer que la colonne doit impérativement être renseignée pour que l'élément traité soit exporté. Dans le cas contraire, une erreur se produira et le traitement s'arrêtera
- vous pouvez également indiquer une valeur par défaut
- si vous souhaitez transférer une date, vous pouvez choisir de la formater. Par défaut, les dates sont stockées au format YYYY-MM-DD HH:mm:ss, mais vous pouvez les transformer comme vous le souhaitez. La syntaxe utilisée est celle du langage PHP : pour formater une date en français, vous pouvez utiliser le code : **d/m/Y H:i:s**.Vous retrouverez le détail des formats disponibles ici : https://www.php.net/manual/fr/datetime.format.php
- le numéro d'ordre dans l'export, ce qui vous permettra de réorganiser les colonnes comme vous le souhaitez. Par défaut, les colonnes sont incrémentées de 10 en 10, ce qui vous permettra facilement de déplacer une colonne entre deux autres, en utilisant les intervalles entre les deux nombres.

Enfin, vous disposez d'une colonne particulière, nommée *fixed_value*, qui permet d'indiquer un contenu fixe dans votre fichier. Dans ce cas, vous devrez indiquer le libellé à fournir dans la rubrique *valeur par défaut*.

Après avoir créé une colonne, n'oubliez pas de cliquer sur le lien *Nouvelle colonne* pour créer une nouvelle colonne : par défaut, c'est la colonne que vous venez de traiter qui reste à l'écran.
### Cas particulier du modèle pour ElabFTW

Le logiciel ElabFTW utilise un modèle de fichier qui mixe des colonnes "classiques" et une colonne au format JSON. Pour obtenir les meilleurs résultats, l'utilisation de cette colonne est nécessaire.

En conséquence, la génération du fichier au format ElabFTW est complètement pilotée par le logiciel, il n'est pas possible de définir des colonnes particulières dans ce contexte.

Pour faciliter la génération dans ce format, le modèle ElabFTW est déjà intégré dans Collec-Science : vous n'aurez pas besoin de vous préoccuper de sa construction.

Pour plus d'informations sur l'utilisation de ce modèle : [[Exporter des échantillons vers ElabFTW]].

## Créer le modèle d'export et associer les modèles de jeux de données

Une fois les modèles de jeux de données créés (datasets), il reste à définir le modèle d'export. Le modèle d'export intègre au moins un dataset, mais pour traiter des configurations particulières, il peut également en contenir plusieurs : dans ce cas-là, le fichier qui sera généré sera au format ZIP (compressé) et comprendra l'ensemble des fichiers correspondants aux jeux de données.

Pour créer un modèle d'export, depuis le menu, choisissez *Imports/exports > Modèles d'export*, puis cliquez sur *Nouveau...* :

![[Pasted image 20260622170003.png]]

La partie gauche de l'écran contient les informations générales, la droite vous permet de sélectionner le ou les modèles de jeux de données à utiliser.

Si vous sélectionnez au moins deux datasets, l'extension du fichier généré sera remplacée par **.zip**, le fichier sera compressé pour contenir les fichiers des datasets.

Si vous n'utilisez qu'un seul dataset, vous pourrez décider de le compresser : un fichier zip sera alors généré.

## Exporter ou importer un modèle d'export

Depuis la liste des modèles d'export, vous avez la possibilité de générer un fichier qui permettra de transférer votre modèle vers une autre instance Collec-Science :

![[Pasted image 20260622170515.png]]

Le fichier généré est au format JSON, et contient la description non seulement du modèle d'export, mais de tout ce qu'il contient : 
- les modèles de jeux de données
- la liste des colonnes, avec les paramètres associés
- les traducteurs.

Lors de l'importation, l'ensemble des objets transférés seront recréés dans la nouvelle instance, au besoin en les renommant si des objets de même nom existent déjà.

Si vous souhaitez en savoir plus sur le mécanisme utilisé, vous pouvez consulter le projet ici : https://github.com/inrae/dbexportmodel