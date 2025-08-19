---
tags:
  - contenant
title: Les contenants et le stockage
authors: Éric Quinton
---
Les contenants sont des #objets ([[Les objets dans Collec-Science]]) qui vont pouvoir contenir d'autres objets.
Un contenant étant un objet, il peut donc être stocké dans un autre contenant : la gestion du stockage s'effectue selon le mécanisme des *poupées russes*.
## Les types de contenants
Les contenants sont forcément d'un *type*. Les types de contenants sont regroupés par *famille*, pour simplifier leur manipulation. La liste des familles est totalement configurable.
Les types de contenant contiennent des informations permettant de qualifier la nature du stockage :
- des informations sur le rangement : 
	- nombre de lignes et de colonnes
	- comment sont numérotées les lignes et les colonnes (alphabétique, numérique) et le point de départ de la numérotation (en haut à gauche, en bas à droite, par exemple)
	- le nombre d'objets maximum possibles (il est toujours possible de *tasser* les objets dans un contenant, c'est à dire de dépasser le nombre maximum autorisé)
- des informations sur le risque associé au stockage :
	- le produit de stockage utilisé
	- la condition de stockage (froid, à sec, etc.)
	- le risque CLP associé (cancérogène, irritant, etc.)
Les informations sur le risque peuvent être imprimées sur les #étiquettes
- un modèle d'étiquettes peut être associé à un type de contenant, sans que cela soit obligatoire ni n'empêche la sélection d'un autre type d'étiquettes au moment de l'impression.
## Les mouvements
Le stockage est géré uniquement à partir de #mouvements. Un objet peut subir un mouvement d'entrée dans un contenant, ce qui permet de savoir où il est stocké. Il peut également être sorti d'un contenant : il sort du stockage.
Pour savoir où est un objet, l'application recherche le dernier mouvement qui a été créé. Pour connaître les objets contenus dans un contenant, l'application recherche les objets dont le dernier mouvement d'entrée vise le contenant considéré.
Les mouvements créés dans l'application ne sont ni modifiables, ni supprimables : si un mouvement créé est erroné, il suffit d'en créer un nouveau pour corriger l'affectation.
Tout utilisateur qui dispose du droit de gestion peut créer un mouvement, sur n'importe quel objet : cette facilité a été implémentée pour permettre la gestion du stockage dans des cas d'urgence, par exemple lors de la panne d'un congélateur ; il faut alors pouvoir indiquer où sont déplacés les échantillons sans souci de l'*appartenance* de ceux-ci. À noter que le login de l'utilisateur qui a procédé au mouvement est enregistré.
Le logiciel permet de réaliser des mouvements selon plusieurs modalités :
- individuellement, depuis le détail d'un objet
- en sélectionnant une liste d'objets depuis la liste de recherche (opération possible si l'utilisateur dispose du droit *collection*)
- en séquence avec une douchette optique : il suffit de scanner en premier lieu le contenant, puis les objets que l'on souhaite déplacer, pour déclencher la création des mouvements correspondants. Cette fonctionnalité est disponible depuis le menu *Mouvements > Entrer ou déplacer / Sortir par lots*
- en utilisant un terminal de type tablette ou smartphone (tablette conseillée) : la caméra de la tablette peut être utilisée pour scanner le qrcode de l'objet, tant pour le contenant que pour l'objet manipulé. Lorsque l'objet à déplacer est scanné, son dernier emplacement connu est proposé, ce qui permet de le ranger à sa place. Cette fonctionnalité est disponible depuis le menu *Mouvements > Mouvements petit terminal*, ou depuis la page d'accueil de l'application.
