---
title: Sauvegarder la base de données avant une grosse opération
authors: Éric Quinton
license: CC-BY
tags:
  - admin
  - sauvegarde
  - database
created: 16/07/2026
---
Collec-Science s'appuie sur une base de données Postgresql pour stocker les informations. Quand une nouvelle instance du logiciel est installée, un script de sauvegarde est programmé, pour assurer au moins une sauvegarde par jour.

D'autres systèmes sont parfois mis en place, avec des outils comme [pgbackrest](https://pgbackrest.org), qui permettent des sauvegardes à des fréquences plus courtes (toutes les heures). Néanmoins, ces systèmes sont conçus pour redémarrer le serveur après un crash total, pas forcément pour restaurer une seule base de données.

Le logiciel permet de réaliser des opérations portant sur toute une série d'échantillons (*cf.* [[Les opérations globales sur les échantillons]]). Si vous envisagez de modifier de façon importante la structure de votre base de données (modification des collections, des types d'échantillons, etc.), il peut être intéressant d'en avoir une sauvegarde au préalable, avant de lancer l'opération : en cas de problème ou de mauvaise manœuvre, il sera plus simple de revenir à l'état précédent.

Pour cela, depuis le menu, choisissez *Administration > Backup* :

![[Pasted image 20260716115258.png]]
L'opération peut prendre un certain temps, surtout si votre base de données est volumineuse et contient beaucoup de documents associés aux échantillons (photos, etc.). Si tout se passe bien, l'application va générer un fichier au format gzip (un format largement utilisé avec les systèmes Linux), qui contient un fichier avec l'extension **.sql** : ce fichier contient l'ensemble des commandes nécessaires pour recharger la base de données.

**Attention** : il est possible que la génération de la sauvegarde échoue, notamment si la base de données est trop volumineuse. Cette situation est liée aux limitations du serveur web (celui qui distribue les pages et vous permet d'accéder à l'application).
Si vous rencontrez un tel souci, vous devrez alors demander à l'administrateur du serveur de réaliser la sauvegarde lui-même.

Si vous avez besoin de revenir à la situation antérieure, contactez l'administrateur du serveur en lui fournissant la copie de la sauvegarde, pour qu'il puisse réaliser les opérations adéquates.