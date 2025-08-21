---
title: Récupérer un fichier attaché à un objet
authors: Éric Quinton
license: CC-BY
tags:
  - api
  - document
created: 19/08/2025
---
## Méthode d'appel

~~~
	documentGetSW?uuid=xxx&token=yyyy&mode=inline
	apiv1documentGet?uuid=xxx&token=yyyy&mode=inline
~~~

Paramètres :

| Paramètre | Contenu                                                                                                              |
| --------- | -------------------------------------------------------------------------------------------------------------------- |
| uuid      | UUID du document concerné (obligatoire)                                                                              |
| token     | jeton d'identification. Information obligatoire si la collection n'est pas publique                                  |
| login     | login associé au jeton (token). Les deux informations doivent être fournies pour que l'identification soit réalisée  |
| mode      | inline/attached : définit le mode d'envoi du document. Par défaut,*inline*                                           |
| locale    | Code de la langue utilisée pour les messages d'erreur ou le formatage des dates. Par défaut : fr, sinon 'en' ou 'us' |


## Données retournées

Le document au format binaire, avec le type MIME correspondant.
## Codes d'erreur

| Code d'erreur | Signification         |
| ------------- | --------------------- |
| 500           | Internal Server Error |
| 401           | Unauthorized          |
| 520           | Unknown error         |
| 404           | Not Found             |

