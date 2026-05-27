---
title: Chercher les échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - échantillons
created: 19/08/2025
---
## Présentation

Le module permettant de rechercher les échantillons est probablement celui que vous utiliserez le plus dans le logiciel : c'est la porte d'entrée pour accéder à vos échantillons.

L'interface est organisé en trois parties : 

- la partie haute permet de définir les critères de recherche ;
- la partie centrale affiche la liste des échantillons (ou la carte de leurs emplacements), et permet de réaliser quelques opérations sur ceux-ci, comme l'impression d'étiquettes ou l'export des données ;
- la partie basse, accessible si vous disposez du droit "collection" (cf. [[Les différents types de droits]]), permet de réaliser des opérations sur plusieurs échantillons à la fois. Ces opérations sont décrites ici : [[Les opérations globales sur les échantillons]].

## L'interface de sélection

Les critères de recherche sont cumulatifs, c'est à dire qu'ils s'additionnent les uns aux autres. Ils sont organisés en onglets, pour faciliter leur manipulation :

- UID/Identifiant : critères de recherche par nom, collection, statut
- Types et métadonnées : recherche sur le type d'échantillon ou par contenu de métadonnée
- Dates : recherches sur des créneaux de dates, pour les différents types de dates manipulées
- Divers : autres critères de recherche, comme la campagne de prélèvement, le motif de déstockage, le type d'événement, etc.
- Localisation : recherche soit par lieu de prélèvement, par pays, ou en sélectionnant une zone sur la carte.

Enfin, un dernier onglet permet d'enregistrer une recherche pour pouvoir la rejouer sans être obligé de repositionner tous les critères.

Dans cet interface, quelques informations vont influer sur le comportement global de l'affichage. Il s'agit de la dernière ligne de celui-ci :

![[Pasted image 20260216100120.png]]

- nombre maxi à lire depuis la base de données / À partir de la page : dès lors que votre recherche risque de récupérer plus de quelques centaines d'échantillons, il est fortement conseillé de limiter le nombre renvoyé au navigateur, sous peine d'avoir des temps d'affichage qui augmentent considérablement. 
  Si vous indiquez une valeur supérieure à 0, les échantillons seront affichés du plus récent au plus ancien (date de création dans la base de données), et vous pourrez naviguer dans les pages. Une fois la requête lancée, le nombre total d'échantillons qui répondent à celle-ci, indépendamment du nombre maxi que vous souhaitez récupéré, sera affiché :
  ![[Pasted image 20260216100712.png]]

- Bouton *Rechercher* : il va déclencher la recherche, à condition qu'un critère au moins ait été renseigné, pour éviter que la requête vous renvoie tous les échantillons.
- Bouton *RAZ* : il réinitialise l'ensemble des critères de recherche à la valeur par défaut. Les critères que vous avez sélectionné sont conservés tout au long de votre session de travail : tant que vous ne vous serez pas déconnecté (ou avez été déconnecté en cas d'inaction prolongée), les critères seront appliqués automatiquement quand vous afficherez cette page de recherche.
- Bouton *Export CSV direct* : si vous souhaitez récupérer une liste très conséquente d'échantillons, vous pouvez alors indiquer 0 dans la zone *Nombre maxi à lire*, et utiliser ce bouton pour récupérer un fichier CSV contenant l'ensemble des informations. C'est le seul moyen pour récupérer rapidement une liste très importante d'échantillons (plusieurs milliers).
- Activer la recherche par colonne : cette case va changer l'affichage de la liste, en remplaçant les entêtes des colonnes par des zones de saisie. Ces zones vont pouvoir être utilisées pour réaliser des recherches uniquement dans les colonnes considérées.
  Pour plus d'informations sur cette fonctionnalité, consultez la page [[La liste des échantillons]].

### L'onglet UID/identifiant

![[Pasted image 20260216101353.png]]

#### La recherche par UID

Pour rechercher par UID, vous avez deux possibilités :

- soit vous connaissez l'UID précisément : il suffit de l'indiquer dans la zone *UID*
- soit vous souhaitez rechercher dans une fourchette : il suffit d'indiquer une valeur basse et une valeur haute dans la zone *UID entre*.

#### La recherche par identifiant

La zone *identifiants ou UUID* vous permet de rechercher à partir de l'identifiant métier ou de l'UUID de l'échantillon :

- en indiquant l'identifiant métier, la recherche va être de type plein texte, c'est à dire que le libellé *bx10* ramènera aussi bien *bx10-12* que *acbx1000*, par exemple ;
- la recherche est indépendante de la casse : vous pouvez saisir aussi bien *BX10* que *bx10* ;
- si la longueur que vous saisissez dans cette zone est de 36 caractères, la recherche sera réalisée en cherchant l'UUID correspondant.

Si une douchette est connectée à votre ordinateur, vous pouvez également scanner un QRCODE (après avoir positionné le curseur dans cette zone) : le programme extraira alors automatiquement l'identifiant métier de l'étiquette.

#### La recherche par collection

Vous disposez de deux possibilités pour rechercher par collection :

- soit vous sélectionnez une seule collection, dans la liste *Collection* ;
- soit vous pouvez rechercher dans plusieurs collections, en en sélectionnant plusieurs (ctrl + clic souris) dans la zone *recherche multiple*.

Attention : seules les recherches effectuées à partir de la zone *Collection* ouvrent la possibilité de réaliser certaines opérations de groupe (*cf.* [[Les opérations globales sur les échantillons]]).

#### La recherche par statut

Par défaut, la recherche s'effectue uniquement en recherchant les échantillons qui sont dans un *état normal*. Si vous ne retrouvez pas un échantillon, c'est peut-être que son statut a évolué (échantillon prêté, par exemple) : désactivez alors la recherche par statut pour le retrouver.

#### La gestion de la corbeille

Collec-Science dispose d'un mécanisme de corbeille : avant de supprimer définitivement un échantillon, vous pouvez simplement le mettre dans une corbeille.

Pour retrouver les échantillons mis à la corbeille, désactivez le paramètre *En attente de suppression* ou indiquez la valeur *oui*.

### L'onglet Type et métadonnées

![[Pasted image 20260216103605.png]]

À partir de cet onglet, vous pouvez rechercher par *type d'échantillon*.

Si vous n'indiquez pas de type, vous pourrez rechercher dans l'ensemble des métadonnées indiquées comme étant utilisables pour la recherche (*cf.*  [[Les métadonnées]]). Si vous indiquez un type, seules les métadonnées associées à ce type seront proposées dans la zone *Rechercher dans les métadonnées*. 

La recherche est une recherche plein texte : si vous indiquez *alosa*, le programme recherchera indifféremment *alosa sp.*, *alosa fallax*, etc. Le programme ne tient également pas compte de la casse.

Vous pouvez indiquer plusieurs valeurs à rechercher pour la même métadonnée (critère *ou*), en les séparant par une virgule. Dans l'exemple ci-dessus, le programme recherchera les échantillons dont la métadonnée *taxon* contient soit le libellé *alosa*, soit le libellé *sturio*.

Enfin, en cliquant sur l'icone *plus*, vous pourrez afficher jusqu'à deux lignes supplémentaires de recherche sur les métadonnées, ce qui vous permettra de compléter vos critères en sélectionnant une seconde métadonnée dans les échantillons. Cette recherche est cumulative : seuls les échantillons qui contiennent les deux (ou trois) métadonnées recherchées seront sélectionnés.

Cet onglet permet également de limiter l'affichage des métadonnées dans la liste. En sélectionnant une métadonnée dans la liste *N'afficher qu'une métadonnée*, seule cette métadonnée sera affichée dans la liste des échantillons (*cf.* [[La liste des échantillons]]).

### L'onglet Dates

![[Pasted image 20260216104544.png]]

L'onglet *Dates* va vous permettre de rechercher les échantillons selon plusieurs dates :

- la date de création dans la base : c'est la date technique qui correspond à l'ajout de l'échantillon dans la base de données ;
- la date d'échantillonnage : c'est la date à laquelle l'échantillon a été récolté ;
- la date d'expiration : si vous avez indiqué une date à laquelle l'échantillon n'est plus utilisable, vous pouvez utiliser cette possibilité ;
- la date technique de dernier changement : c'est la date où l'échantillon a été modifié pour la dernière fois dans la base de données.

Vous pouvez indiquer une fourchette de temps pour la recherche. Par défaut, celle-ci est positionnée sur une année.

Si vous utilisez le module de réservation des échantillons, vous avez également la possibilité de rechercher les échantillons réservés (ou non) sur une période.

### L'onglet Divers
![[Pasted image 20260527161424.png]]

À partir de cet onglet, vous pouvez rechercher :

- les échantillons "appartenant" à un *référent* ;
- les échantillons qui n'ont pas été rangés dans un contenant (*Échantillons sans contenants*) ;
- ceux qui ont été récoltés pendant une *campagne de prélèvement*, ou ceux qui ont bénéficié d'une autorisation administrative (*N° d'autorisation*). La recherche par numéro d'autorisation s'effectue indépendamment des campagnes de prélèvement auxquelles elles sont rattachées ;
- ceux qui sont associés à un protocole/opération de collecte (*cf.* [[Les protocoles de collecte]]) ;
- ceux qui ont été déstockés pour un motif particulier (*Motif de déstockage*) ;
- enfin, pour les échantillons pour lesquels vous avez activé le sous-échantillonnage, vous pouvez rechercher ceux qui disposent encore d'une certaine quantité (*quantité minimale disponible dans l'échantillon*) ou ceux qui sont quasiment vides (*maximale*).

### L'onglet Localisation

![[Pasted image 20260216105730.png]]

Cet onglet va permettre deux types de recherche : une recherche sur des critères "classiques", et une recherche par emplacement géographique

Vous pouvez lancer une recherche par lieu de prélèvement (*cf.* [[Les lieux de prélèvement]]), par pays de collecte ou par pays de provenance : ces deux dernières informations sont utilisées dans le cadre du protocole de Nagoya (https://fr.wikipedia.org/wiki/Protocole_de_Nagoya).

Si vous avez indiqué des coordonnées géographiques dans vos échantillons, vous pouvez également lancer la recherche sur une zone particulière. Pour cela, dans la carte, cliquez sur le bouton au centre (à gauche), puis tracez un rectangle sur la carte. Seuls les échantillons présents dans cette zone seront affichés.

### L'onglet Recherches enregistrées

![[Pasted image 20260216110700.png]]

Si vous utilisez régulièrement les mêmes critères de recherche et qu'ils sont nombreux à positionner, vous avez la possibilité d'enregistrer ces critères une bonne fois pour toute, à partir de cet onglet.

Pour créer une nouvelle recherche enregistrée :

- sélectionnez l'ensemble des critères de recherche que vous voulez appliquer ;
- indiquez le nom que vous souhaitez donner à votre recherche dans la zone *Nom de la recherche*.

Quand vous déclencherez la recherche, avec le bouton *Rechercher*, les critères seront enregistrés.

Les recherches sont personnelles, mais vous pouvez toutefois mettre à disposition une recherche pour vos collègues :

- dans les critères de recherche, indiquez la collection sur laquelle vous travaillez ;
- indiquez le *nom de la recherche* ;
- cliquez sur *oui* dans la zone *Enregistrer pour la collection sélectionnée*.

Vos collègues, dès lors qu'ils disposent des droits de modification sur la collection considérée, pourront accéder à la recherche que vous avez enregistré.

Pour supprimer une recherche enregistrée, sélectionnez-là dans la liste, puis cliquez sur le bouton *Supprimer*. La recherche va être lancée, mais elle sera quand même supprimée de la base de données.

Si vous souhaitez modifier une recherche enregistrée, vous devrez en créer une nouvelle puis supprimer l'ancienne.
## La liste des échantillons

La liste des échantillons sélectionnés est affichable sous deux formes :

- soit une liste textuelle, décrite ici : [[La liste des échantillons]]
- soit sous forme de carte géographique, où vous pouvez consulter l'emplacement de chaque échantillon géo-référencé. 

Pour visualiser l'emplacement des échantillons, sélectionnez l'onglet *Carte*. Si la densité d'échantillons est trop importante, un cercle sera affiché qui permettra de savoir combien d'échantillons sont situés à cet emplacement.

En cliquant sur l'icône d'un échantillon, une bulle s'affiche avec son UID et son identifiant métier. En cliquant sur ces informations, vous ouvrirez le détail de l'échantillon.

![[Pasted image 20260206112950.png]]

Sur la carte, en cliquant sur l'icône <flèche vers le bas>, vous pourrez obtenir une image de la carte, au format paysage. L'image est calculée à partir du centre de la carte.

## Les opérations globales

Consultez cette page pour en savoir plus sur les opérations globales possibles : [[Les opérations globales sur les échantillons]]
