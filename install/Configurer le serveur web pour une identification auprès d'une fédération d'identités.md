---
title: Configurer le serveur web pour une identification auprès d'une fédération d'identités
authors: Éric Quinton
license: CC-BY
tags:
  - sample_latlong
  - fédération
created: 29/07/2026
---
Le logiciel Collec-Science permet d’identifier les utilisateurs en s’appuyant soit sur la base de données interne, soit sur un annuaire LDAP, soit sur un service d’identification CAS (Common Access Service) ou OIDC (OpenID Connect), soit en utilisant une fédération d’identités. Cette dernière option permet notamment de pouvoir connecter des utilisateurs provenant de divers établissements. Pour les établissements français de recherche ou d’enseignement supérieur, il est possible de s’appuyer sur la fédération Renater, si l’établissement concerné y est affilié.

*L'original de ce document peut être consulté ici : https://www.collec-science.org/faq/divers/identifier-les-utilisateurs-en-s-appuyant-sur-une-federation-d-identites-renater-par-exemple.*
## Configurer Apache pour l’identification à partir d’une fédération

L’identification est réalisée en utilisant un module Apache dédié : Mellon ([https://github.com/latchset/mod_auth_mellon](https://github.com/latchset/mod_auth_mellon)).

Elle nécessite de récupérer les informations techniques liées à la fédération, et d’enregistrer l’application chez le fournisseur de l’identification.

### Installation du module Mellon

`apt−get install libapache2 −mod−auth−mellon`

Si le paquet libapache2-mod-auth-mellon n’est pas disponible (cas rencontré avec une distribution Debian strech), vous devrez récupérer et installer les paquets suivants (dans l’ordre) :

- libxmlsec1
- libxmlsec1-openssl
- liblasso3
- libapache2-mod-auth-mellon

Vous devrez également récupérer le fichier xml de votre provider, ainsi que son certificat.

### Génération des fichiers de configuration de l’application

Un certificat (et sa clé privée), un fichier xml doivent être générés pour l’application. Un script est disponible dans les distributions Debian. Il est également fourni dans l’application, dans le dossier install/apache2 (create_metadata.sh).

Pour générer les fichiers (remplacez collec-science.com par vos propres valeurs) :

~~~
cd /etc/apache2
mkdir mellon
cd mellon
/var/www/collec2App/collec-science/install/apache2/create_metadata.sh https://collec-science.com https://collec-science.com/mellon
~~~

Le certificat (fichier .cert) et le fichier xml doivent être transmis au provider, pour qu’il les intègre dans sa plate-forme. Vous devez également récupérer du provider sa clé publique et son certificat  
d’autorité racine, à mettre dans le dossier mellon. Il doit également vous fournir un fichier xml qui contient les adresses de toutes les entités participant à la fédération.

### Configurer le site virtuel

Recopiez le fichier _install/apache2/collec-science-mellon.conf_ dans le dossier _/etc/apache2/sites-available_, à la place du fichier _collec-science.conf_. Éditez le fichier, et remplacez toutes les chaînes collec.mysociety.com par votre DNS. Vérifiez également les certificats utilisés.

Par rapport au fichier classique, le fichier _collec-science-mellon.conf_ contient, dans la section <VirtualHost *443>, les commandes suivantes :

~~~
# Configuration Mellon for Renater
<location />
AuthType Mellon
MellonEnable "auth"
MellonSecureCookie On
MellonUser MAIL
MellonMergeEnvVars On
MellonSubjectConfirmationDataAddressCheck Off
MellonSPPrivateKeyFile /etc/apache2/mellon/https_collec.mysociety.com.key
MellonSPCertFile /etc/apache2/mellon/https_collec.mysociety.com.cert
MellonSPentityId "https://collec.mysociety.com"
MellonSPMetadataFile "/etc/apache2/mellon/https_collec.mysociety.com.xml"
MellonIdPMetadataFile "/etc/apache2/mellon/main-idps-renater-metadata.xml"
MellonIdPPublicKeyFile "/etc/apache2/mellon/renater-metadata-signing-cert-2016.pem"
MellonIdPCAFile "/etc/apache2/mellon/renater-metadata-signing-cert-2016.pem"
MellonProbeDiscoveryTimeout 1
MellonSetEnv "MAIL" "urn:oid:0.9.2342.19200300.100.1.3"
MellonSetEnv "GIVENNAME" "urn:oid:2.5.4.42"
MellonEndpointPath /mellon
MellonSetEnvNoPrefix REMOTE_USER NAME_ID
MellonDiscoveryURL "https://discovery.renater.fr/renater/WAYF"
</location>
~~~

Les rubriques _MellonIdP*_ doivent être adaptées aux fichiers fournis par votre _provider_. Les rubriques _MellonSetEnv_ permettent d'associer les urn avec des noms de variables lisibles. Ainsi, l'urn oid:2.5.4.42 sera transmise dans la variable MELLON_GIVENNAME

Une fois la configuration effectuée, redémarrez le serveur Apache :

~~~
systemctl restart apache2
~~~

### Enregistrer le site dans la fédération Renater

Pour les établissements français affiliés à la fédération Renater, vous pouvez enregistrer directement votre application dans celle-ci. Des validations seront réalisées par les contacts de la fédération dans votre établissement.

Pour réaliser l’enregistrement :

- Connectez-vous au site [https://federation.renater.fr/registry](https://federation.renater.fr/registry)
- cliquez sur _Ajouter un fournisseur de services_
- dans l’onglet Description, renseignez les champs demandés, avec notamment :
    - URL du service : https ://collec.mysociety.com (votre DNS)
- dans l’onglet Contacts, ne vous déclarez pas conforme au cadre de sécurité SIRTFI, sauf si vous savez ce que c’est (il y a des contraintes organisationnelles fortes pour être conforme)
- dans l’onglet _Attributs demandés_, demandez les attributs :
    - email : identification des utilisateurs (obligatoire)
    - commonName : affichage du nom des utilisateurs (obligatoire)
- dans l’onglet Informations techniques, indiquez l’adresse suivante pour récupérer les données de configuration :
    - URL de vos métadonnées : https ://collec.mysociety.com/mellon/metadata

Une fois le dossier validé, vous devrez attendre le retour de votre correspondant Renater dans votre établissement, qui doit valider votre demande.  
Une fois cette première demande réalisée, vous devrez vous reconnecter au site de la fédération ([https://federation.renater.fr/registry](https://federation.renater.fr/registry)), et activer le rattachement à la fédération choisie (onglet _Rattachement à une fédération_). Deux fichiers seront à récupérer (commande wget dans le dossier /etc/apache2/mellon) pour récupérer d’une part le certificat, et d’autre part le fichier XML contenant l’ensemble des fournisseurs attachés à la fédération.

Ce rattachement doit également être validé par votre correspondant Renater.

Attention : une fois le rattachement validé, vous devrez attendre 24 heures pour que votre application soit disponible auprès de l’ensemble des membres de la fédération, et donc pouvoir vous connecter.