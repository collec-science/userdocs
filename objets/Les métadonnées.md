---
title: Les métadonnées
authors: Éric Quinton
license: CC-BY
tags:
  - métadonnées
created: 19/08/2025
---
Les métadonnées sont des informations qui sont rajoutées aux #échantillons pour les décrire.
Collec-Science associe quelques données aux échantillons (dates d'échantillonnage, par exemple), mais l'application ne peut prendre en compte tous les besoins liés aux usages de chacun. Le mécanisme de gestion des métadonnées permet ainsi de définir de nouveaux champs qui permettront de décrire plus finement les échantillons.
Techniquement, les métadonnées sont stockés dans un champ de la base de données au format JSON : leur manipulation est un peu plus complexe par le langage d'interrogation SQL, et certaines contraintes sont associées à ce format. Il est ainsi compliqué de renommer un champ de métadonnées, et le nom des champs doit impérativement respecter quelques contraintes précisées ci-dessous.
## Les modèles de métadonnées
Pour pouvoir ajouter des métadonnées aux échantillons, il est nécessaire de les décrire dans des modèles (menu *Paramètres > métadonnées*). 
![[metadonnees-detail.png]]
Chaque champ d'un modèle va être décrit avec les informations suivantes :
- son nom : il doit impérativement être écrit en minuscule, sans accent, sans espace, sans utiliser le caractère tiret (-). Il est toutefois possible d'utiliser le caractère tiret bas (\_).
- son type. Il peut être :
	- du texte
	- un nombre, décimal ou non
	- une date (un sélecteur de type calendrier sera proposé)
	- une zone de texte multi-ligne
	- des cases à cocher : dans ce cas, une liste de valeurs possible devra être ajoutée
	- une liste de choix : la liste de valeurs possibles doit être saisie manuellement
	- des boutons-radios : la liste des valeurs possibles doit être saisie
	- un lien vers un site externe (url)
	- une zone permettant la saisie de plusieurs valeurs textuelles.
- une valeur par défaut
- la description du champ, qui sera affichée dans le formulaire de saisie des informations
- si le champ peut être utilisé pour rechercher des échantillons. En validant cette information, le logiciel va créer un *index* dans la base de données pour accélérer les recherches : n'activez cette fonctionnalité que si vous en avez réellement besoin
- si le champ est obligatoire ou non
- l'unité de mesure, si l'information à renseigner concerne des données quantifiables
- il est également possible d'ajouter un message d'aide, qui sera affiché dans le formulaire.
Vous pouvez modifier l'ordre des champs à votre convenance.
![[metadonnees-saisie.png]]
## Gérer les modèles de métadonnées
![[metadonnees-liste.png]]
Les modèles peuvent être :
- dupliqués : cela permet de créer un premier modèle pour un type d'échantillons, puis de rajouter un nouveau champ pour un second type d'échantillons qui serait utilisé pour des échantillons dérivés, ce qui permettra de mieux caractériser ces derniers
- exportés, puis importés : cette opération est intéressante quand un modèle a vocation à être échangé avec d'autres instances de Collec-Science.

## La gestion des métadonnées pour les échantillons dérivés
Prenons un exemple. Un premier type d'échantillons est *poisson*. À partir d'un poisson, on prélève des tissus :
![[metadonnees-heritees.png]]
Les métadonnées permettant de qualifier le poisson (son taxon, ses mensurations) sont complétées par la nature du tissu qui est prélevé.
Si les métadonnées sont modifiées dans le parent, par exemple le taxon, elles seront également mises à jour dans les échantillons dérivés.
## Modifier le nom d'une métadonnée
Cette opération est complexe, et nécessite d'intervenir avec des commandes SQL directement dans la base de données : assurez-vous de disposer d'une sauvegarde avant de lancer l'opération !
Imaginons que nous souhaitions renommer le champ "espece" en "species".
### Première étape : renommer le champ dans la base de données
Avec un éditeur SQL, nous allons d'abord vérifier l'opération de renommage avant de l'exécuter :

~~~
select sample_id, metadata, metadata -> 'espece',
jsonb_insert(metadata::jsonb, '{"species"}'::text[], (metadata->'espece' )::jsonb) - 'espece'
from col.sample
where metadata ->>'espece' is not null;
~~~
La requête permet de rajouter un champ "species" dont le contenu est 'espece' (*jsonb_insert*), puis de supprimer le champ 'espece' (- 'espece').
Pour mettre à jour les données, il suffit de modifier la requête ainsi :
~~~
update col.sample
set metadata = jsonb_insert(metadata::jsonb, '{"species"}'::text[], (metadata->'espece' )::jsonb) - 'espece'
where metadata ->> 'espece' is not null;
~~~
### Seconde étape : modifier le ou les modèles de métadonnées correspondants
Dans le logiciel, modifiez les modèles de métadonnées pour renommer le champ 'espece' en 'species'.
Vous pouvez visualiser rapidement la liste des modèles de métadonnées qui contiennent le libellé concerné :
~~~
select metadata_id, metadata_name, metadata_schema
from col.metadata
where metadata_schema::text like '%espece%';
~~~