---
title: Base technique
authors: Éric Quinton
license: CC-BY
tags:
  - doc
created: 19/08/2025
---
## Configuration de Obsidian

La documentation a été rédigée avec le logiciel Obsidian (https://obsidian.md/), avec les plugins suivants :
- *Excalidraw* pour la création des dessins
- Style settings : Bolt
- *Webpages HTML Export* pour générer la documentation en html

accompagnés des plugins utilitaires *Git* et *Advanced Tables*, non nécessaires pour la génération de la documentation, mais bien pratiques...

### Configuration de webpages HTML Export

De nombreux paramètres sont disponibles. La plupart de ceux utilisés par défaut conviennent, mais ont été adaptés :
- Pages features : 
	- désactivation de *file navigation*
- General settings
	- Favicon image : images/favicon.png
	- Site name : https://collec-science.github.io/userdocs
- Styles Option
	- Theme : Bolt
- Export Settings :
	- désactivation de *Use relative header links*
	- activation de *Make Offline compatible*
- Obsidian Settings :
	- Title property : title

## Publication Github

La documentation est stockée dans le dépôt https://github.com/collec-science/userdocs, avec deux branches : *develop* et *main*.

Le composant *pages* de Github a été activé pour générer la documentation à partir de la branche *main*, en utilisant le dossier *docs* :

![[Pasted image 20250831161744.png]]
