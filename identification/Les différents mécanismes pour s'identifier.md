---
title: Les différents mécanismes pour s'identifier
authors: Éric Quinton
license: CC-BY
tags:
  - identification
created: 19/08/2025
---
Collec-Science a été conçu pour autoriser l'identification des utilisateurs selon plusieurs mécanismes différents, en fonction des usages locaux liés à l'établissement. Il est également possible de mixer diverses possibilités, pour s'adapter à des situations particulières.

## Les mécanismes disponibles

### Identification gérée directement par l'application

Le stockage des mots de passe est réalisé dans la base de données. Ceux-ci sont chiffrés et ne peuvent pas être découverts.

Les mots de passe doivent, au minimum :
- avoir une longueur de 12 caractères
- comporter au moins 3 jeux de caractères parmi les minuscules, les majuscules, les chiffres et les caractères spéciaux.

Si vous perdez votre mot de passe, un lien vous sera adressé par messagerie pour vous permettre de le réinitialiser.

### Identification auprès d'un annuaire d'entreprise

Plusieurs méthodes sont utilisables pour vous permettre de vous identifier auprès du service d'identification de votre entreprise :
- LDAP : le logiciel va interroger directement l'annuaire de votre entreprise. Cette méthode est aujourd'hui déconseillée
- CAS et OIDC : l'identification est sous-traitée à un site web, qui va se charger de vous identifier
- Fédération d'identité : l'identification va être sous-traitée à une fédération qui regroupe plusieurs organismes. Une fois que vous aurez indiqué votre établissement, la fédération d'identité vous redirigera vers l'identification de votre établissement.

### Particularités

L'utilisation des API, c'est à dire la possibilité d'interagir avec le logiciel depuis une autre application, nécessite une identification particulière ([[Identification pour les API]]). Cette identification est  toutefois incompatible avec l'identification par la fédération d'identité : il faut alors prévoir deux adresses web pour votre application pour gérer à la fois l'identification par la fédération et l'identification directe pour les API.

Une fois que vous vous êtes identifiés une première fois dans la journée, un *cookie* est déposé dans votre navigateur, et vous évitera de devoir vous ré-identifier pendant 10 heures.
### Les identifications mixtes

Dans certains cas, vous avez besoin de gérer des utilisateurs qui proviennent à la fois de votre entreprise, mais également d'autres sociétés, sans pouvoir utiliser un mécanisme de fédération d'identité. Le logiciel pourra être paramétré pour supporter à la fois l'identification de votre entreprise (LDAP, CAS ou OIDC) et l'identification gérée par l'application.

## Modifier son mot de passe

Votre mot de passe ne pourra être modifié dans l'application que si c'est celle-ci qui le gère. La modification s'effectue depuis le menu à droite (sous votre *login*), en choisissant *Mot de passe*.

## Renforcer l'identification

Pour limiter les risques d'usurpation, vous pouvez activer une double identification utilisant le protocole TOTP ([[La double authentification]]). Cette double identification est obligatoire pour accéder aux fonctions d'administration.