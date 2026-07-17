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
## Modifier le nom d'un champ de métadonnées

La modification du nom d'un champ de métadonnées implique deux opérations : 
- la modification du nom dans le modèle
- la modification de la métadonnée dans les échantillons concernés.

Si vous modifiez le nom d'un champ dans la description du modèle, le renommage sera reporté automatiquement dans les échantillons qui utilisent ce modèle.

Vous pouvez également renommer globalement un champ, quel que soit le modèle qui l'utilise (à partir de la version v26.0.0). Depuis la liste des modèles de métadonnées, en bas d'écran, choisissez le formulaire *Renommer un champ de métadonnées globalement*, indiquez l'ancien nom et le nouveau, puis lancez l'opération : les modèles seront mis à jour ainsi que l'ensemble des échantillons qui contiennent cette métadonnée.

Pour plus d'informations, consultez cette page : [[Régénérer les modèles de métadonnées ou renommer un champ]].

## Supprimer un champ de métadonnées

Si vous souhaitez supprimer un champ de métadonnées de vos échantillons, vous devrez lancer (ou faire exécuter, si vous ne gérez pas le serveur qui héberge votre instance) cette commande SQL :

~~~sql
update sample
set metadata::jsonb - 'ma_metadonnee' 
from sample 
where metadata::text like '%"ma_metadonnee":%';
~~~


## Opérations de maintenance sur les modèles de métadonnées

Dans certains cas, des opérations de maintenance sont nécessaires pour éviter des dysfonctionnement de l'application. Consultez cette page pour plus d'informations : [[Régénérer les modèles de métadonnées ou renommer un champ]].