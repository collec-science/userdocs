---
title: Installer la documentation dans son propre serveur
authors: Éric Quinton
license: CC-BY
tags:
  - install
created: 14/10/2025
---
La documentation en ligne est hébergée sur le site de Github (https://github.com/collec-science/userdocs). La version visualisable est stockée dans le dossier *docs* de l'arborescence, et c'est le composant *pages* de Github qui est utilisé par défaut pour publier celle-ci.

Si vous souhaitez héberger la documentation dans votre serveur, l'opération est assez simple à réaliser.

## Paramétrer votre serveur
### Créer une copie du dépôt dans votre serveur

```bash
cd /var/www
git clone https://github.com/collec-science/userdocs.git -b main
```

### Créer un lien depuis votre dépôt collec

```bash
cd /var/www/collecApp/collec-science/public
ln -s /var/www/userdocs/docs docs
```

### Modifier un paramètre dans votre fichier .env

Éditez le fichier */var/www/collecApp/collec-science/.env*, et rajoutez l'entrée suivante : 

```env
app.docroot=https://collec.local/docs
```

En remplaçant *collec.local* par l'adresse de votre instance.

## Pour mettre à jour la documentation

Pensez à mettre à jour régulièrement la documentation (au moins après chaque nouvelle version de Collec-Science) :

```bash
cd /var/www/userdocs
git pull origin main
```