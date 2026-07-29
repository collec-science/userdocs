---
title: Définir le mode d'identification des utilisateurs
authors: Éric Quinton
license: CC-BY
tags:
  - identification
created: 29/07/2026
---
Collec-Science s'appuie sur le composant Ppci (https://github.com/equinton/ppci) pour gérer l'identification.

Le logiciel propose plusieurs modes d'identification : 

- comptes gérés dans la base de données
- comptes gérés dans un annuaire d'entreprise à la norme Ldap
- identification sous-traitée auprès d'un ou plusieurs serveurs CAS (Common Access Service)
- identification sous-traitée auprès d'un ou plusieurs serveurs OIDC (OpenID Connect)
- identification fournie par le serveur web lui-même : c'est ce mécanisme qui est utilisé pour se connecter auprès d'une fédération d'identités, comme EduGAIN (https://edugain.org/) ou, pour la France, Renater (https://services.renater.fr/federation/documentation/generale/federation-edugain).

Parallèlement à ces modes de connexion (hormis le dernier, qui a un fonctionnement particulier), deux autres mécanismes sont utilisés :

- une fois identifié, un jeton est déposé dans le navigateur de l'utilisateur, ce qui lui permet de se ré-identifier sans avoir besoin de ressaisir son mot de passe pendant 10 heures (une journée de travail) ;
- pour les accès par API, un autre mécanisme est utilisé, qui est décrit ici : [[Identification pour les API]].

Enfin, le logiciel dispose d'un système de double-identification basé sur le protocole TOTP. L'utilisateur doit impérativement l'utiliser s'il souhaite accéder aux fonctions d'administrations (droit *admin*).

Le paramétrage des modes d'identification est opéré dans le fichier *.env* situé à la racine de l'application.

*Nota Bene* : La version v26.2.0 de Collec-Science apporte quelques nouveautés et change la manière de déclarer les mécanismes d'identification. Néanmoins, le composant Ppci reste compatible avec les identifications précédentes : vous ne serez pas obligé de modifier le fichier .env de votre instance.

## Définir le mode d'identification

Le mode d'identification dépend des serveurs d'identification auxquels vous pouvez vous rattacher. Voici un schéma qui devrait vous permettre d'y voir plus clair :

![[choix identification.png]]

### Au moment de l'installation du logiciel

Pour vous permettre de configurer le premier compte d'administration, vous aurez besoin de vous connecter à l'application avec le compte *admin*, géré par la base de données.

Voici la configuration à mettre en place dans le fichier *.env* :

~~~
Ppci\Config\IdentificationConfig.disableTotpToAdmin=1
Ppci\Config\IdentificationConfig.identificationMode = MIXED
Ppci\Config\IdentificationConfig.mixedLocalIdentification = BDD
~~~

### Vous ne disposez pas de mécanismes tiers d'identification (serveurs CAS, OIDC, ou fédération d'identités)

Vous pourrez gérer les comptes soit uniquement dans la base de données, soit auprès d'un annuaire LDAP, si vous avez un accès disponible.

Voici les paramètres à mettre en place :

~~~
Ppci\Config\IdentificationConfig.disableTotpToAdmin=0
Ppci\Config\IdentificationConfig.identificationMode = MIXED
Ppci\Config\IdentificationConfig.mixedLocalIdentification = BDD | LDAP | LDAP-BDD
~~~

La variable *mixedLocalIdentification* peut contenir les valeurs suivantes :

- BDD : l'identification est uniquement gérée par le logiciel
- LDAP : l'identification est uniquement gérée auprès de l'annuaire LDAP
- LDAP-BDD : lors de la connexion, l'identification est testée d'abord auprès de l'annuaire LDAP. En cas d'échec, elle sera alors testée auprès des comptes internes.

Voici l'ensemble des paramètres à renseigner pour l'identification LDAP :

~~~
Ppci\Config\IdentificationConfig.LDAP.address = ldaps://ldap.organisme.fr
# Ppci\Config\IdentificationConfig.LDAP.port = 686
Ppci\Config\IdentificationConfig.LDAP.basedn = "ou=people,dc=organisme,dc=fr"
# Ppci\Config\IdentificationConfig.LDAP.user_attrib = "uid"
# Ppci\Config\IdentificationConfig.LDAP.v3 = true
# Ppci\Config\IdentificationConfig.LDAP.tls = true
# Ppci\Config\IdentificationConfig.LDAP.upn_suffix =
# Ppci\Config\IdentificationConfig.LDAP.groupSupport = false
# Ppci\Config\IdentificationConfig.LDAP.commonNameAttribute = "displayname"
# Ppci\Config\IdentificationConfig.LDAP.mailAttribute = "mail"
# Ppci\Config\IdentificationConfig.LDAP.groupnameAttribute = "cn"
# Ppci\Config\IdentificationConfig.LDAP.loginnameAttribute = "memberuid"
# Ppci\Config\IdentificationConfig.LDAP.basedngroup = 'ou=example,o=societe,c=fr'
Ppci\Config\IdentificationConfig.LDAP.timeout = 1
# Ppci\Config\IdentificationConfig.LDAP.ldapnoanonymous = false
# Ppci\Config\IdentificationConfig.LDAP.ldaplogin =
# Ppci\Config\IdentificationConfig.LDAP.ldappassword =
~~~

En principe, seuls les attributs *address* et *basedn* sont à renseigner, mais si nécessaire, vous pouvez intervenir sur les autres paramètres en fonction des caractéristiques propres de votre annuaire.
### Vous utilisez un service d'identification propre à votre organisation

Ce service est unique et sera le seul à être utilisé. Vous faites confiance aux comptes qui sont présents dans cet annuaire central.

~~~
Ppci\Config\IdentificationConfig.disableTotpToAdmin=0
Ppci\Config\IdentificationConfig.identificationMode = CAS | OIDC
~~~

Selon le type de serveur, vous devrez définir les paramètres suivants : 

#### Serveur CAS

~~~
Ppci\Config\IdentificationConfig.CAS.address = "cas.organisme.fr"
# Ppci\Config\IdentificationConfig.CAS.uri = "/cas"
# Ppci\Config\IdentificationConfig.CAS.Port = 443
# Ppci\Config\IdentificationConfig.CAS.debug = false
# Ppci\Config\IdentificationConfig.CAS.getGroups = 1
# Ppci\Config\IdentificationConfig.CAS.groups = "supannEntiteAffectation"
# Ppci\Config\IdentificationConfig.CAS.email = 'mail'
# Ppci\Config\IdentificationConfig.CAS.name = 'cn'
# Ppci\Config\IdentificationConfig.CAS.firstname = 'givenName'
# Ppci\Config\IdentificationConfig.CAS.lastname = 'sn'
~~~

En principe, les attributs sont standardisés, mais vous pouvez les adapter le cas échéant. Avec la variable *getGroups* positionnée à 1, le serveur vous renverra le groupe d'appartenance de votre utilisateur, qui sera utilisé automatiquement dans Collec-Science.

#### Serveur OIDC

La configuration est un peu plus complexe. Dans un premier temps, vous devrez obligatoirement enregistrer votre instance Collec-Science auprès du serveur OIDC. Pendant cette phase, assurez-vous de déclarer l'adresse de retour (callback) : https://votreserveur.fr/oidc

Les serveurs OIDC ne proposent pas tous de vous fournir les mêmes informations. Elles sont déclarées dans des *scopes*. Vous pouvez consulter ceux qui sont disponibles en consultant la page https://provider.org/.well-known/openid-configuration

Voici les paramètres à renseigner : 

~~~
Ppci\Config\IdentificationConfig.OIDC.name = "displayed name"
Ppci\Config\IdentificationConfig.OIDC.provider = https://provider.org
Ppci\Config\IdentificationConfig.OIDC.clientId = [clientId fourni au moment de l'enregistrement]
Ppci\Config\IdentificationConfig.OIDC.clientSecret = [secret associé]
Ppci\Config\IdentificationConfig.OIDC.email = 'email'
Ppci\Config\IdentificationConfig.OIDC.name = 'name'
Ppci\Config\IdentificationConfig.OIDC.firstname = 'given_name'
Ppci\Config\IdentificationConfig.OIDC.lastname = 'family_name'
Ppci\Config\IdentificationConfig.OIDC.scopeGroup = ""
Ppci\Config\IdentificationConfig.OIDC.groups = "supannEntiteAffectationPrincipale"
# verify the allowed scopes at this address : provider/.well-known/openid-configuration
Ppci\Config\IdentificationConfig.OIDC.scopes = "profile,email"
~~~

En général, les serveurs privés (d'organismes) fournissent les adresses email et souvent le groupe d'appartenance. Pour pouvoir récupérer le groupe de l'utilisateur, vous devez renseigner le *scope* qui contient le groupe dans la variable *scopeGroup* : le logiciel ira chercher le groupe d'appartenance dans ce scope à partir de l'attribut déclaré dans la variable *groups*.

### Vous identifiez les utilisateurs auprès d'annuaires publics, ou vous souhaitez proposer un mix

Voici les paramètres de base :

~~~
Ppci\Config\IdentificationConfig.disableTotpToAdmin=0
Ppci\Config\IdentificationConfig.identificationMode = MIXED
~~~

#### Identification locale

Si vous souhaitez utiliser une identification locale, renseignez la variable :

~~~
Ppci\Config\IdentificationConfig.mixedLocalIdentification = BDD | LDAP | LDAP-BDD
~~~

Sinon, laissez-là vide.

#### Utilisation de serveurs CAS

En principe, vous n'indiquerez qu'un seul serveur CAS, celui de votre organisme, mais le logiciel peut en supporter plusieurs. 

Pour cela, renseignez les paramètres suivants :

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

Par défaut, le serveur CAS vous renverra le groupe d'appartenance de l'utilisateur (variable *getGroups* positionnée à 1).

#### Utilisation de serveurs OIDC

Le comportement du logiciel sera différent selon que vous interrogez un serveur de votre organisation ou public :

- pour un serveur de votre organisation, vous pourrez probablement récupérer le groupe d'appartenance et le mail de vos utilisateurs, et les laisser accéder directement à l'application sans contrôle complémentaire ;
- pour un serveur public, par exemple ORCID, vous ne récupérerez que le nom et le prénom. Au moment de la première connexion, les comptes seront bloqués et devront être débloqués par un administrateur.

Les serveurs OIDC ne proposent pas tous de vous fournir les mêmes informations. Elles sont déclarées dans des *scopes*. Vous pouvez consulter ceux qui sont disponibles en consultant la page https://provider.org/.well-known/openid-configuration

Vous devez d'abord déclarer la liste des serveurs OIDC que vous souhaitez utiliser :

~~~
Ppci\Config\Oidc.servers = "orcid"
~~~

Si vous utilisez plusieurs serveurs, séparez leurs noms par une  virgule, sans espace.

Ici, il s'agit, à titre d'exemple, d'une configuration pour le serveur fourni par ORCID (mode *sandbox*).

Pour chaque serveur, vous devrez déclarer l'ensemble de ces paramètres, chaque variable préfixée par le nom du serveur :

~~~
Ppci\Config\Oidc.servers = "orcid"
Ppci\Config\Oidc.orcid.name = "Identification via ORCID"
Ppci\Config\Oidc.orcid.provider = "https://sandbox.orcid.org"
Ppci\Config\Oidc.orcid.clientId = "XXX"
Ppci\Config\Oidc.orcid.clientSecret = "YYYY"
Ppci\Config\Oidc.orcid.name = "name"
Ppci\Config\Oidc.orcid.firstname = "given_name",
Ppci\Config\Oidc.orcid.lastname = "family_name",
Ppci\Config\Oidc.orcid.email = "email"
Ppci\Config\Oidc.orcid.getGroups = 0
Ppci\Config\Oidc.orcid.isPublic = 1
Ppci\Config\Oidc.orcid.scopes = ""
Ppci\Config\Oidc.orcid.logo = "display/images/orcid.png"
~~~

Le logo pour ORCID est déjà fourni dans le logiciel.

Vous pouvez vérifier les *scopes* proposés par le serveur d'identification à cette adresse : https://sandbox.orcid.fr/.well-known/openid-configuration

### Vous voulez vous identifier auprès d'une fédération d'identités

La connexion auprès d'une fédération d'identités est complexe, et utilise le protocole shibboleth. Pour la mettre en place, il est préférable de s'appuyer sur un plugin du serveur web Apache, Mellon.

Consultez ce document pour connaitre les opérations à exécuter : [[Configurer le serveur web pour une identification auprès d'une fédération d'identités]]

*Attention* : la fédération française Renater n'accepte plus l'inscription de nouvelles instances Collec-Science.
## Les logos

Pour les serveurs CAS ou OIDC, des logos sont affichés. Vous devrez les placer dans le dossier (ou un sous-dossier) *public*, et indiquer leur chemin par rapport à cette racine (c'est le point d'accès vu par les navigateurs).