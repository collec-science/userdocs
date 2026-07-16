---
title: Rechercher des mouvements cycliques
authors: Éric Quinton
license: CC-BY
tags:
  - mouvements
created: 16/07/2026
---
Pour gérer le stockage, le logiciel fonctionne avec des mouvements d'entrée : un objet est placé dans un contenant, qui lui-même peut être placé dans un autre contenant, etc. Pour retrouver où se situe un objet (échantillon ou contenant), Collec-Science utilise une requête récursive, qui va parcourir l'ensemble des mouvements pour retrouver les parents de chaque objet.

Avant la version v26.1, il était possible de créer une boucle : un contenant était inséré dans un autre contenant, qui lui-même finissait par être inséré dans le premier. Dans cette situation, l'accès à la liste des échantillons pouvait finir par faire planter le serveur de bases de données, qui tournait en boucle au moment de l'exécution de la requête récursive.

Si le problème survient, il est possible de rechercher les cas où le on rencontre ce cas de figure. Pour cela, depuis le menu, choisissez *Administration > Recherche des mouvements cycliques*.

![[Pasted image 20260716113450.png]]

S'il rencontre des contenants dans ce cas, le logiciel affichera l'UID de chacun des contenants concernés. 

Pour régler le problème : 
- notez les UID des contenants concernés
- depuis le menu, choisissez *Mouvements > Sortir du stock*
- créez le mouvement de sortie pour les objets concernés
- après vérification, vous pourrez alors recréer les mouvements d'entrée corrects

Attention : ne passez jamais par la liste des échantillons ou par la liste des contenants pour créer les mouvements de sortie, sinon vous referez planter le logiciel.

Les dernières versions du logiciel réalisent un contrôle avant la création du mouvement, ce qui devrait maintenant éviter ce type de problème.