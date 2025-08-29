---
title: Supprimer un échantillon
authors: Éric Quinton
license: CC-BY
tags:
  - api
created: 19/08/2025
---
## Principe

Cette API permet, depuis une application tierce, de supprimer un échantillon.

## Identification

Consultez ce document pour créer l'utilisateur de l'API, générer un token et lui donner les droits adéquats : [[Identification pour les API]]

## Appel par défaut

> URL : apiv1sampleDelete

L'API doit être appelée en mode http **POST**.

### Variables à fournir

| Nom de la variable | Description                                                                                                          | obligatoire |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- | :---------: |
| login              | Login du compte utilisé pour appeler l'API                                                                           |      X      |
| token              | Jeton d'identification associé au login                                                                              |      X      |
| locale             | Code de la langue utilisée pour les messages d'erreur ou le formatage des dates. Par défaut : fr, sinon 'en' ou 'us' |             |
| uid                | UID de l'échantillon à supprimer                                                                                     |      X      |

