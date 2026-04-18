---
title: Les types d'échantillons
authors: Éric Quinton
license: CC-BY
tags:
  - échantillon
created: 12/03/2026
---
Par défaut, les échantillons sont dotés de certaines informations génériques, comme la date de collecte, la collection d'appartenance, etc. Les types d'échantillons permettent de préciser ce qu'ils sont réellement, de rajouter des informations spécifiques (décrites dans les #métadonnées ), d'indiquer les produits rajoutés pour les conserver (solution tampon, alcool, dissolvants, etc.) ou de préciser les risques qui sont liés à leur manipulation (radio-activité, risques liés aux produits rajoutés pour les conserver, etc.). Il est également possible de les associer à un type de contenant pour pouvoir mieux préciser leur conditionnement.

Les échantillons sont forcément rattachés à un type d'échantillon.

## Les informations à indiquer dans un type d'échantillon

![[Pasted image 20260312102145.png]]

- Nom : c'est le nom qui sera utilisé dans le logiciel. Choisissez quelque chose de suffisamment explicite et non ambigu.
- code utilisé pour les échanges d'informations : si vous échangez des informations avec d'autres organismes, vous pouvez indiquer dans cette rubrique le nom qui est utilisé pour le qualifier. Cela peut être une nomenclature nationale ou internationale, par exemple. L'information est remontée, dans les interrogations (exports ou api) dans la colonne *sample_type_code*.
- type de contenant : vous pouvez associer un type d'échantillon à un type de contenant, ce qui permet de préciser le conditionnement utilisé
- protocole / opération : lors de certaines opérations de collecte, les échantillons passent par plusieurs phases de tri ou de traitement, chaque phase définissant un nouvel échantillon d'un type particulier. Par exemple, la capture d'insectes dans un champ est réalisé dans des pots enterrés dans le sol, puis plusieurs opérations de tri permettent d'abord de séparer les différents types d'insectes (araignées, vers, etc.) puis de déterminer les taxons. Chaque opération débouche sur des échantillons dérivés de types différents.
  En associant un type d'échantillon à une opération, cela vous permet de savoir à quel moment du traitement l'échantillon a été généré.
- description : si vous le souhaitez, vous pouvez préciser de manière textuelle le type d'échantillon
- modèle de métadonnées : vous pouvez indiquer ici le modèle de métadonnées qui va être utilisé pour compléter la description des échantillons. Dans l'exemple ci-dessus, le nom du taxon sera demandé lors de la création d'un échantillon de type *écailles de poisson*.

Il est également possible d'indiquer si les échantillons rattachés au type d'échantillon sont susceptibles de faire l'objet d'un sous-échantillonnage. Dans ce cas, vous devrez indiquer :
- la nature du sous-échantillonnage (unité, pourcentage, quantité ou volume, autre)
- l'unité de base, ici, c'est le nombre d'écailles qui sont stockées dans l'échantillon


### Générer automatiquement l'identifiant de l'échantillon

Enfin, lors de la création d'un échantillon depuis l'interface web, le logiciel est doté d'une fonction qui permet de générer l'identifiant de l'échantillon à partir des informations saisies. Cette fonction utilise la bibliothèque Jquery du langage Javascript (un langage utilisé pour gérer la programmation dans le navigateur). 

Voici les consignes à respecter pour écrire la fonction de création de l'identifiant :

- l'opérateur de concaténation est le signe +
- la syntaxe de JQuery est basée sur `$("#id")`, où \#id correspond à l'objet recherché
- la syntaxe varie en fonction du type de champ dont vous voulez récupérer la valeur :
    - pour les champs simples : `$("#uid").val()`
    - pour récupérer le contenu d'une boite de sélection : `$("#collection_id option:selected").text()`
    - pour récupérer le contenu d'une variable simple issue des métadonnées : `$("#md_nom_de_la_metadonnee").val()` (le nom de la métadonnée doit être préfixé par md_)
    - pour récupérer le contenu d'une métadonnée sélectionnée par bouton-radio : `$("#md_nom_de_la_metadonnee:checked").val()`
- Exemple : pour générer cet identifiant : nom_collection-valeur_metadonnee-uid :
    - `$("#collection_id option:selected").text().trim()+$("#md_taxon").val()+"-"+$("#uid").val()`
    (taxon est le champ de métadonnées recherché, qui doit être préfixé par md_)
- Liste des champs utilisables :
    - uid : identifiant interne
    - object_status_id : statut de l'échantillon
    - collection_id : nom de la collection
    - sample_type_id : type d'échantillon
    - sample_creation_date : date de création de l'échantillon
    - sampling_date : date d'échantillonnage
    - expiration_date : date d'expiration de l'échantillon
    - wgs84_x : longitude
    - wgs84_y : latitude
    - et les variables disponibles dans les champs de métadonnées

## Associer un type d'échantillon à une collection

En raison de sa versatilité, Collec-Science peut être utilisé pour gérer des collections très différentes, voire du matériel. Pour faciliter le travail des opérateurs, il peut être intéressant de réserver certains types d'échantillons à des collections dédiées.

L'association d'un type d'échantillon à une collection est réalisé depuis la page de modification d'un échantillon ([[Les collections]]). Une fois qu'un type d'échantillon a été rattaché à une collection, il ne sera plus visible dans les collections auquel il n'est pas associé.

## Combien de types d'échantillons faut-il créer ?

Les types d'échantillons sont une brique essentielle du logiciel, mais il est difficile de donner des règles immuables pour savoir quand en créer un nouveau, sachant que chaque situation peut induire des approches différentes.

Voici toutefois quelques conseils :

- ne rentrez pas trop dans le détail. Si vous pêchez des poissons de multiples espèces, il est probablement préférable d'avoir un seul type d'échantillon, vous pourrez préciser l'espèce à partir des métadonnées.
  De même, si vous récoltez des parties de plante, vous pourrez également n'avoir qu'un seul type et préciser la partie récoltée (feuille, tige, racine, etc.) à partir des métadonnées
- *a contrario*, ne soyez pas trop génériques ! Ne créez pas un seul type qui rendraient les échantillons uniquement identifiables à partir des métadonnées
- respectez les types d'échantillons qui sont utilisés dans votre domaine. Par exemple, si vous travaillez avec des carottes sédimentaires, vous avez probablement des types déterminés (sections, demi-sections, plaquettes, etc.). Conservez ces types, il faciliteront les échanges avec vos partenaires
- créez un nouveau type chaque fois que le produit de stockage utilisé ou le risque encouru change : ces informations pourront figurer sur les étiquettes
- si vous associez vos types d'échantillons à des types de contenants, vous devrez créer des types d'échantillons pour chaque type de contenant correspondant

Et pas de panique ! Si vous souhaitez faire évoluer votre collection de types d'échantillons, le logiciel vous permettra de changer le type d'une série d'échantillons avec les fonctions de groupe ([[Les opérations globales sur les échantillons]]).