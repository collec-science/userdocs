---
title: Exporter les contenants avec leur contenu vers une autre instance Collec-Science
authors: Éric Quinton
license: CC-BY
tags:
created: 21/07/2026
---
Si vous souhaitez transférer une boite contenant plusieurs échantillons vers un laboratoire qui utilise Collec-Science, vous pourrez leur transmettre un fichier qui contient déjà toutes les informations adéquates pour qu'ils puissent stocker ce que vous leur transmettez directement.

## Exporter la liste

Pour réaliser cette opération :

- depuis le module de recherche des contenants, sélectionnez ceux que vous souhaitez transférer ;
- cliquez sur le bouton *Export vers une autre base* : le logiciel va rechercher tous les objets contenus, y compris les contenants imbriqués (une caisse qui contient des boites, qui contiennent elles-mêmes des échantillons, par exemple). Le logiciel va générer un fichier au format JSON, qui contient l'ensemble de la hiérarchie des objets concernés.
- une fois votre fichier généré, enregistrez une opération de prêt en utilisant les fonctionnalités de modification globales des contenants, situées en bas de la liste des contenants (*cf.* [[Chercher des contenants]]).

**Attention :** cette opération n'est pas à réaliser sur l'ensemble des contenants de votre instance ! Comme le logiciel va parcourir les contenants imbriqués, puis les échantillons qu'ils contiennent, s'il y a trop d'éléments concernés, vous risquez de faire planter votre serveur ou, dans le meilleur des cas, obtenir un fichier inexploitable.

## Importer la liste

Consultez la page [[Importer des contenants avec leur contenu à partir d'un fichier JSON]].