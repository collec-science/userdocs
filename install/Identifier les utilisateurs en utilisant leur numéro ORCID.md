---
title: Identifier les utilisateurs en utilisant leur numéro ORCID
authors: Éric Quinton
license: CC-BY
tags:
created: 30/07/2026
---
ORCID (https://orcid.org) est un *identifiant unique que les personnes peuvent utiliser dans le cadre de leurs activités de recherche, de recherche et d'innovation*. La plate-forme propose un mécanisme d'identification Oauth ou OIDC, qui permet à des applications tierces d'identifier leurs utilisateurs en s'appuyant sur cet identifiant.

À partir de la version v26.2.0 de Collec-Science, il est possible d'identifier les utilisateurs en s'appuyant sur ORCID. Cette fonctionnalité peut être utile si vous souhaitez que des utilisateurs provenant d'autres organismes puissent accéder à votre instance.

## Inscrire l'application auprès d'ORCID

Vous devez disposer d'un compte ORCID. Suivez alors les prescriptions décrites dans ce document : https://info.orcid.org/fr/documentation/api-tutorials/api-tutorial-get-and-authenticated-orcid-id/#h-get-some-client-credentials

L'URL de redirection doit être impérativement : https://votreAdresseCollec-science.organisation.org/oidc

## Configurer Collec-Science

La configuration s'effectue dans le fichier *.env* situé à la racine de l'application (*cf.* [[Définir le mode d'identification des utilisateurs]]). Voici les paramètres à indiquer :

~~~
Ppci\Config\IdentificationConfig.identificationMode = MIXED
Ppci\Config\Oidc.servers = "orcid"
Ppci\Config\Oidc.orcid.name = "Identification via ORCID"
Ppci\Config\Oidc.orcid.provider = "https://orcid.org"
Ppci\Config\Oidc.orcid.clientId = "[client fourni par ORCID]"
Ppci\Config\Oidc.orcid.clientSecret = "[secret fourni par ORCID]"
Ppci\Config\Oidc.orcid.name = "name"
Ppci\Config\Oidc.orcid.firstname = "given_name",
Ppci\Config\Oidc.orcid.lastname = "family_name",
Ppci\Config\Oidc.orcid.email = "email"
Ppci\Config\Oidc.orcid.getGroups = 0
Ppci\Config\Oidc.orcid.isPublic = 1
Ppci\Config\Oidc.orcid.scopes = ""
Ppci\Config\Oidc.orcid.logo = "display/images/orcid.png"
~~~

À noter que le logo est déjà présent dans Collec-Science.

Vous devrez rajouter votre mode d'identification habituel, pour vos utilisateurs internes, soit, en fonction des modes de connexion dont vous disposez :

- si vous utilisez un serveur LDAP :

~~~
Ppci\Config\IdentificationConfig.mixedLocalIdentification = LDAP
~~~

- si vous utilisez un serveur CAS :

~~~
Ppci\Config\Cas.servers = "default"
# for each server, here named default
Ppci\Config\Cas.default.name = "displayed name"
Ppci\Config\Cas.default.address = "mycasserver.com"
Ppci\Config\Cas.default.uri = "/cas"
Ppci\Config\Cas.default.port = 443
Ppci\Config\Cas.default.debug = false
Ppci\Config\Cas.default.logo = "favicon.png"
Ppci\Config\Cas.default.Capath = ""
Ppci\Config\Cas.default.getGroups = 1
Ppci\Config\Cas.default.groups = "supAnnEntiteAffectation"
Ppci\Config\Cas.default.firstname = "givenName"
Ppci\Config\Cas.default.lastname = "sn"
Ppci\Config\Cas.default.email = "mail"
~~~

Vous pouvez également utiliser un autre serveur OIDC : il suffit de modifier cette directive :

~~~
Ppci\Config\Oidc.servers = "monserveur,orcid"
~~~

Puis de définir les paramètres pour votre serveur interne OIDC ainsi :

~~~
Ppci\Config\Oidc.monserveur.name = "Identification via MONSERVEUR"
Ppci\Config\Oidc.monserveur.provider = "https://monserveur.org"
Ppci\Config\Oidc.monserveur.clientId = "[client fourni par MONSERVEUR]"
Ppci\Config\Oidc.monserveur.clientSecret = "[secret fourni par MONSERVEUR]"
Ppci\Config\Oidc.monserveur.name = "name"
Ppci\Config\Oidc.monserveur.firstname = "given_name",
Ppci\Config\Oidc.monserveur.lastname = "family_name",
Ppci\Config\Oidc.monserveur.email = "email"
Ppci\Config\Oidc.monserveur.getGroups = 1
Ppci\Config\Oidc.monserveur.isPublic = 0
Ppci\Config\Oidc.monserveur.scopes = "email"
Ppci\Config\Oidc.monserveur.scopeGroup = "scope contenant le nom du groupe"
Ppci\Config\Oidc.monserveur.logo = "display/images/monserveur.png"
~~~

Vous pouvez vérifier les *scopes* disponibles en consultant cette page : https://monserveur.org/.well-known/openid-configuration ou en demandant à votre direction informatique les informations adéquates.

Pensez à faire enregistrer l'adresse de retour à  https://votreAdresseCollec-science.organisation.org/oidc

Il faudra également que vous installiez le logo de votre organisation dans le dossier *public* de Collec-Science, de préférence dans le sous dossier *display/images*.

## Fonctionnement

Lorsque l'utilisateur se connecte pour la première fois à votre instance Collec-Science avec son identifiant ORCID, son compte va être créé mais va être verrouillé. Si l'envoi de mails est activé dans votre instance, les administrateurs de l'application (droit *admin*) recevront un message leur informant de la connexion.

Il faudra alors activer le compte de l'utilisateur :

- dans le menu *Administration > Liste des comptes locaux*, vous retrouverez son nom et son prénom (les seules informations récupérées) ainsi que son identifiant ORCID, qui sert de login. Modifiez sa fiche pour l'activer :
![[Pasted image 20260730183247.png]]
Si vous connaissez son email, indiquez-le également dans cette fiche : l'information n'est pas récupérée depuis ORCID.

Au moment de la validation, si vous avez renseigné son email, un message sera envoyé à l'utilisateur pour l'informer de l'activation de son compte.

- dans le menu *Administration > ACL - groupes de logins*, affectez son compte à au moins un groupe (au minimum *consult*) pour qu'il puisse accéder au contenu de l'application.

## Limitations

ORCID ne fournit pas l'adresse email de l'utilisateur : vous devrez la renseigner manuellement.

Un utilisateur interne à votre organisation pourrait se connecter non seulement avec le mécanisme habituel (serveur LDAP, CAS, etc.), mais également avec son compte ORCID. Dans ce cas, il disposerait de deux comptes séparés, avec des droits différents de l'un à l'autre.
Dans la pratique, il est conseillé de demander aux utilisateurs internes qui disposent d'un compte lié à votre organisation de ne pas utiliser l'identification ORCID.

## Si vous voulez supprimer un compte

Le meilleur moyen pour supprimer un compte est de passer par le menu *Administration > ACL - logins* : c'est la table sous-jacente (acllogin) qui est utilisée pour gérer les droits.

La suppression de la fiche dans ce module supprimera également les droits attribués et la fiche créée dans les comptes locaux.