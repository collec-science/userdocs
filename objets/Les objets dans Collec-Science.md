---
title: Les objets dans Collec-Science
authors: Éric Quinton
tags:
  - objet
---
![[objets.png]]
Collec-Science manipule des objets. Un objet est :
- soit un #échantillon ([[Les échantillons]])
- soit un #contenant ([[Les contenants et le stockage]])
Les objets sont porteurs de propriétés propres :
- un identifiant métier : c'est le code par lequel l'objet est connu et manipulé au quotidien
- un #UID (*unique identifier*) : il s'agit d'un nombre généré par le logiciel, qui sert à le manipuler dans le logiciel. L'UID figure sur les étiquettes
- un #UUID (*Universal Unique identifier*) : il s'agit d'un nombre formé de 36 caractères, généré avec des algorithmes cryptographiques qui garantissent qu'il est unique au niveau mondial
- des informations de localisation : le point GPS soit de prélèvement (pour les échantillons) soit l'emplacement (pour un bâtiment, par exemple).
À un objet peuvent être rattachés :
- un #statut : les statuts permettent de caractériser l'état de l'objet (en service, détruit, prêté, etc.)
- un ou plusieurs autres identifiants, qui pourront être utilisés (ou non) pour retrouver l'objet dans Collec-Science
- un #référent. Pour les échantillons, si le référent n'est pas défini, le référent de la #collection sera retenu (s'il existe)
- un ou plusieurs documents, de tous types. Les documents peuvent être stockés dans la base de données, s'ils sont peu volumineux, ou dans une arborescence bureautique accessible depuis le serveur
Les objets peuvent également subir des #événements. Ceux-ci peuvent être programmés à l'avance si besoin était.
Enfin, un objet peut être prêté : le logiciel permet de suivre les prêts et de connaître les emprunteurs.
