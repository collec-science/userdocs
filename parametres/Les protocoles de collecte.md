---
title: les protocoles
authors: Éric Quinton
license: CC-BY
tags:
  - protocole
  - opération
created: 19/08/2025
---
Les protocoles permettent de préciser dans quelles conditions les échantillons sont prélevés ou générés. Au sein d'un protocole, différentes opérations permettent de créer des échantillons : collecte sur le terrain, tri initial en laboratoire, sous-échantillonnage, etc.

Les échantillons peuvent être rattaché à une opération de collecte (à partir de la version v26.2.0) :

![[protocole.png]]
Les protocoles sont décrits par leur nom, leur numéro de version, et quelques informations complémentaires comme l'année ou le numéro de l'autorisation associé. Un document peut également lui être attaché, qui devrait être sa description officielle.

Une ou plusieurs opérations peuvent être définies au sein d'un protocole, chacune étant décrite par un nom, un code, un numéro d'ordre dans le protocole et un numéro de version. Le code associé à l'opération doit être unique : il est utilisé dan le logiciel pour associer une opération à un échantillon, lors des importations.

**Attention :** avant la version v26.2.0, les opérations étaient rattachées aux types d'échantillons. Les informations étaient identiques, mais la manière de les gérer différait : il fallait créer un type d'échantillon pour chaque opération.

## Créer un protocole

Depuis le menu, *Paramètres > Protocoles > Protocoles*. Vous accédez alors à la liste, puis vous pouvez soit modifier un protocole, soit en créer un nouveau.

![[Pasted image 20260527155620.png]]
La collection de rattachement est obligatoire, mais n'est pas utilisée dans le logiciel, hormis pour différencier les protocoles. Vous pouvez, depuis cet écran, ajouter un fichier pdf au protocole, ou le supprimer en cochant la case *ad-hoc* le cas échéant.

## Créer une opération

Depuis le menu, *Paramètres > Protocoles > Protocoles*. Vous accédez alors à la liste, puis vous pouvez soit modifier une opération, soit en créer une nouvelle.

![[Pasted image 20260527155935.png]]

Depuis la liste, vous pouvez dupliquer une opération : le nouvel item reprend toutes les informations de l'opération copiée, hormis le numéro de version.

![[Pasted image 20260527160328.png]]


**Attention :** le code utilisé pour les importations doit être unique dans la base de données. Si le code choisi est déjà associé à une autre opération, l'enregistrement échouera.
Par ailleurs, le code ne peut pas contenir d'espace.

## Manipulation des échantillons en lien avec les opérations

Depuis la fenêtre de recherche des échantillons (*Objets>Échantillons*), vous pouvez :

- rechercher les échantillons associés à une opération (*cf.* [[Chercher les échantillons]], onglet *Divers*) ;
- associer une opération aux échantillons sélectionnés, depuis le menu en bas de la liste (*cf.* [[Les opérations globales sur les échantillons]]).