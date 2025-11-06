---
title: Créer ou modifier un modèle d’étiquettes
authors: Éric Quinton
license: CC-BY
tags:
  - étiquettes
created: 19/08/2025
---
Les étiquettes sont composées de deux parties : un ou deux codes lisibles avec un lecteur optique, et du texte. Il est également possible d'insérer un logo.

Les codes optiques peuvent être de deux types :

- soit un QRCODE: celui-ci peut contenir  :
  - plusieurs informations, stockées au format JSON : il devra alors comprendre au minimum l'UID de l'objet et le code de la base de données ;
  - une seule information. Dans ce cas, on privilégiera l'identifiant de type UUID, qui garantit l'unicité de l'objet au niveau mondial, sauf si le QRCODE généré est trop grand. Il faudra alors stocker uniquement l'UID de l'échantillon ;
- soit un code-barre 1D au format EAN 128. Ce format est utilisé pour les supports ronds (tubes), qui rendent la lecture optique 2D difficile. Dans ce cas, le code ne devrait contenir que l'UID de l'échantillon.

Les étiquettes sont créées en recourant au logiciel FOP, écrit en Java.

Voici les opérations réalisées par l’application pour générer les étiquettes :

- pour chaque objet concerné (des contenants ou des échantillons associés à un type de contenant, et si le type de contenant est rattaché à un modèle d’étiquettes), une image des codes optiques, ainsi que le logo, sont générés dans un dossier temporaire ;
- dans ce dossier temporaire, un fichier au format XML est généré qui contient les informations à imprimer sur l’étiquette ;
- un fichier au format XSL, qui contient les ordres de création de l’étiquette, est également créé dans le même dossier. Le contenu de ce fichier est issu d’un enregistrement provenant de la table *label* ;
- le programme PHP fait appel à FOP pour générer, à partir du fichier XML et en utilisant le fichier XSL, un fichier PDF. Une page du fichier correspond à une étiquette (mécanisme utilisé par les imprimantes à étiquettes pour les séparer).

La configuration du modèle d’étiquettes revient à définir à la fois le contenu des informations qui seront insérées dans les codes optiques et la forme que prendra l’étiquette, c’est à dire les informations qui seront imprimées, le format, etc. Cette forme reprend la syntaxe XSL comprise par FOP.

## Créer un nouveau modèle d'étiquette

Le logiciel est livré avec une étiquette type : il est préférable de dupliquer cette étiquette plutôt que de partir d'une "page blanche".

Pour cela, depuis la liste des modèles d'étiquettes, cliquez sur le bouton *Dupliquer* à partir du modèle livré : 

![[Pasted image 20251007154048.png]]
Pour mettre au point le modèle, nous vous conseillons d'utiliser deux navigateurs : l'un pour ajuster les différents paramètres, et l'autre pour visualiser le contenu en générant manuellement les étiquettes.

## Si vous rencontrez un problème lors de la création de votre étiquette

Lors de la génération des étiquettes, si rien n'est produit et que le logiciel vous indique une erreur, c'est probablement qu'une balise, dans le code de description de l'étiquette, n'est pas fermée. Malheureusement, les messages d'erreur détaillés ne peuvent être consultés qu'avec un accès au serveur, en consultant les logs du serveur web.

Techniquement, la commande suivante est lancée par l'application :

~~~bash
/usr/bin/fop -xsl /var/www/collecApp/collec-science/writable/temp/1.xsl -xml /var/www/collecApp/collec-science/writable/temp/b98ff1340b2e.xml -pdf /var/www/collecApp/collec-science/writable/temp/b98ff1340b2e.pdf
~~~

- le fichier 1.xsl contient la définition de l'étiquette (champ *Transformation XSL*). Le nom du fichier correspond à l'identifiant du modèle d'étiquette dans la base de données. Ce fichier est détruit automatiquement une fois que l'étiquette a été générée
- le fichier xml est conservé dans le dossier temporaire du serveur (*writable/temp/*). Le nom du fichier est généré automatiquement
- le fichier pdf contient les étiquettes prêtes à être imprimées.

Si vous souhaitez mettre au point un modèle d'étiquette en dehors du logiciel (et notamment le contenu du champ *Transformation XSL*), vous devrez :

- dans les paramètres de l'application, (*Administration > Paramètres de l'application*), positionnez la valeur *labelDebugMode* à 1
- lancez la génération d'une étiquette
- depuis le serveur web, récupérez les fichiers présents dans le dossier */var/www/collecApp/collec-science/writable/temp*, et notamment le fichier xml (les données à insérer), le fichier xsl (le modèle de l'étiquette) et les fichiers png (les codes optiques générés et le logo) 
- adaptez la commande fop à votre environnement et exécutez-là depuis un terminal.  

Vous pouvez récupérer le programme fop depuis ce site : https://xmlgraphics.apache.org/fop/download.html. Fop est également disponible dans les dépôts des principales distributions Linux.

Cette manière de faire vous permettra de visualiser plus facilement les messages d'erreur, suffisamment détaillés pour comprendre où le problème se pose.

Une fois votre étiquette mise au point, n'oubliez-pas de repositionner le paramètre *labelDebugMode* à 0.

## Définir le contenu des codes optiques

Le logiciel vous permet de générer un ou deux codes optiques, au format :

- QRcode : c'est un format de code barre normalisé en deux dimensions, qui permet de stocker jusqu’à 2000 caractères en 8 bits. Les QRcodes peuvent être lus facilement avec l'application depuis une tablette numérique, voire un smartphone.
- EAN128 : code barre 1D qui encode jusqu'à 128 caractères alpha-numériques. Compte-tenu de l'extrême densité des informations, il est difficile de lire un code de ce type avec une tablette, le recours à des lecteurs optiques (douchettes) est quasi-indispensable. Ce type de code est par contre adapté aux supports arrondis (tubes).

À noter que le module de lecture des codes-barres dans l'application qui utilise la caméra d'une tablette ou d'un smartphone, est actuellement incapable de lire autre chose qu'un QRCode.
### Définir le contenu du QRcode

Le contenu du QRcode peut être formaté selon deux méthodes : 
- soit le contenu contient plusieurs informations différentes, encodées en JSON : c'est le format initial (historique) utilisé par l'application
- soit le contenu ne contient qu'une information, avec ou non un radical (pour générer des url) : on privilégiera alors soit l'intégration de l'UUID, soit l'identifiant de la base de données d'origine (qui est généré automatiquement s'il n'existe pas au préalable).

Pour un contenu multiple, au format JSON :

- champs obligatoires :

| Nom | Description                                                                   |
| ----- | :------------------------------------------------------------------------------ |
| uid | Identifiant unique de l’objet dans la base de données                       |
| db  | Identifiant de la base de données. C’est la valeur du paramètre APPLI_code |

- autres champs utilisables :

| Nom                                       | Description                                                                                                                               |
| ----------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| id                                        | identifiant  métier général                                                                                                               |
| col                                       | code de la collection                                                                                                                     |
| pid                                       | identifiant de l'échantillon parent                                                                                                       |
| clp                                       | code de risque                                                                                                                            |
| pn                                        | nom du protocole                                                                                                                          |
| x                                         | coordonnée wgs84_x de l'objet (lieu de prélèvement ou de stockage suivant le cas)                                                         |
| y                                         | coordonnée wgs84_y de l'objet                                                                                                             |
| loc                                       | localisation du prélèvement (table des lieux de prélèvement)                                                                              |
| ctry                                      | code du pays de collecte                                                                                                                  |
| prod                                      | produit utilisé pour la conservation                                                                                                      |
| cd                                        | date de création de l'échantillon dans la base de données                                                                                 |
| sd                                        | date d'échantillonnage                                                                                                                    |
| ed                                        | date d'expiration de l'échantillon                                                                                                        |
| uuid                                      | UID Universel (UUID)                                                                                                                      |
| ref                                       | référent de l'objet                                                                                                                       |
| autre codes                               | tous les codes d’identification secondaires définis dans la table de paramètres Types d’identifiants                                      |
| les champs utilisés dans les métadonnnées | les codes des champs utilisés dans la description des métadonnées. Un modèle d’étiquette ne peut être associé qu’à un type de métadonnées |
À noter que plus vous utilisez d'informations, plus le code généré sera dense, et nécessitera une grande taille pour pouvoir rester lisible.

- Champs utilisables dans le QRCODE à contenu unique :

| Nom          | Description                                                                                                                |
| ------------ | :------------------------------------------------------------------------------------------------------------------------- |
| id           | identifiant  métier général                                                                                                |
| uid          | Identifiant unique de l’objet dans la base de données                                                                      |
| uuid         | UID Universel (UUID)                                                                                                       |
| autre        | tout identifiant secondaire non numérique - cf. paramètres > Types d'identifiants                                          |
| dbuid_origin | identifiant de la base de données d'origine. Pour un échantillon créé dans la base courante, la valeur sera de type db:uid |

Il est conseillé d'utiliser dans ce cas de figure de préférence le code UUID, qui garantit l'unicité du numéro de l'échantillon ou de l'objet au niveau mondial.

### Champ utilisable dans le code-barre EAN 128

Pour des raisons de lecture optique, il est fortement conseillé de n'insérer que le numéro *uid* de l'échantillon, ou *dbuid_origin*.

## Configuration du fichier XSL

La syntaxe particulière du fichier XSL ne doit être modifiée qu’en conservant la version initiale (recopie dans un bloc-notes, par exemple), pour éviter de perdre une configuration opérationnelle suite à un mauvais paramétrage.

Voici la description du contenu du fichier et les zones modifiables. Nous allons prendre comme exemple cette étiquette :
![Pasted image 20251005192821.png](app://8803250ddfff3033b41b816cf2ff0722a633/home/equinton/web/userdocs/attachments/Pasted%20image%2020251005192821.png?1759685301724)

Elle est organisée ainsi : 

La partie haute est un tableau, composé d'une ligne et de deux colonnes : 
- la première colonne contient un logo, un texte, puis sur la ligne inférieur, le code du labo dans l'application et l'uid de l'échantillon. La troisième ligne contient l'identifiant métier (id) de l'échantillon
- la seconde colonne contient le QRCODE)
La partie basse contient un code EAN128 centré, puis sur la ligne inférieure, le risque CLP.

### Entête du fichier

Elle permet de modifier la taille de l’étiquette (largeur et hauteur maximale). Vous ne devriez changer que les attributs page-height et page-width. Pour les marges (attributs margin-), soyez prudents et vérifiez notamment que les QRcodes ne soient pas rognés à cause de marges insuffisantes.


~~~xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0"
	xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
	xmlns:fo="http://www.w3.org/1999/XSL/Format">
	<xsl:output method="xml" indent="yes"/>
	<xsl:template match="objects">
		<fo:root>
			<fo:layout-master-set>
				<fo:simple-page-master master-name="label"
					  page-height="5cm" page-width="10cm" margin-left="0.5cm" margin-top="0.5cm" margin-bottom="0cm" margin-right="0.5cm">  
					  <fo:region-body/>
				</fo:simple-page-master>
			</fo:layout-master-set>
			<fo:page-sequence master-reference="label">
				<fo:flow flow-name="xsl-region-body">        
					<fo:block>
						<xsl:apply-templates select="object" />
					</fo:block>
				</fo:flow>
			</fo:page-sequence>
		</fo:root>
	</xsl:template>
~~~

### Le tableau

Le contenu proprement dit de l'étiquette est décrit dans *match="object"*. Nous allons commencer par déclarer le tableau (*table*), avec la largeur de chaque colonne.
~~~xml
	<xsl:template match="object">
		<fo:table table-layout="fixed" border-collapse="collapse"  border-style="none" width="9cm" keep-together.within-page="always">
			<fo:table-column column-width="6cm"/>
			<fo:table-column column-width="3cm" />
~~~

Nous allons maintenant déclarer le contenu du tableau, en commençant par déclarer une ligne, puis la première colonne (*table-cell*):

~~~xml
			<fo:table-body border-style="none" >
				<fo:table-row>
					<fo:table-cell>
						<fo:block>
							<fo:external-graphic>
								<xsl:attribute name="src">
									<xsl:value-of select="concat(label_id,'-logo.png')"/>
								</xsl:attribute>
								<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
									<xsl:attribute name="height">1cm</xsl:attribute>
									<xsl:attribute name="content-width">1cm</xsl:attribute>
									<xsl:attribute name="scaling">uniform</xsl:attribute>
								</fo:external-graphic>
								<fo:inline> Labo Collec-Science</fo:inline>
						</fo:block>
						<fo:block><fo:inline font-weight="bold"><xsl:value-of select="db"/>:<xsl:value-of select="uid"/></fo:inline></fo:block>
						<fo:block>id:<fo:inline font-weight="bold"><xsl:value-of select="id"/></fo:inline></fo:block>
					</fo:table-cell>
~~~

Chaque ligne dans la cellule du tableau est définie dans un bloc (balises *fo:block*).
Le logo est déclaré dans un *external-graphic*, et le nom du fichier est généré à partir de l'identifiant de l'étiquette (*label-id*) associé à *-logo.png*. Divers attributs sont précisés pour définir les paramètres du graphique, ici la hauteur est fixée à 1cm.

Le libellé *Labo Collec-Science* est rajouté à la suite du logo, en utilisant la balise *inline*. Divers attributs permettent d'indiquer soit des tailles de texte, soit du gras (ici, *font-weight="bold"*).

Les différentes informations de l'objet sont insérées dans l'étiquette en utilisant la balise : <xsl:value-of select="db"/> (pour le code de la base de données). Voici la liste des attributs utilisables :

| Nom                                       | Description                                                                                                                               |
| ----------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| id                                        | identifiant  métier général                                                                                                               |
| col                                       | code de la collection                                                                                                                     |
| pid                                       | identifiant de l'échantillon parent                                                                                                       |
| clp                                       | code de risque                                                                                                                            |
| pn                                        | nom du protocole                                                                                                                          |
| x                                         | coordonnée wgs84_x de l'objet (lieu de prélèvement ou de stockage suivant le cas)                                                         |
| y                                         | coordonnée wgs84_y de l'objet                                                                                                             |
| loc                                       | localisation du prélèvement (table des lieux de prélèvement)                                                                              |
| ctry                                      | code du pays de collecte                                                                                                                  |
| prod                                      | produit utilisé pour la conservation                                                                                                      |
| cd                                        | date de création de l'échantillon dans la base de données                                                                                 |
| sd                                        | date d'échantillonnage                                                                                                                    |
| ed                                        | date d'expiration de l'échantillon                                                                                                        |
| uuid                                      | UID Universel (UUID)                                                                                                                      |
| ref                                       | référent de l'objet                                                                                                                       |
| autre codes                               | tous les codes d’identification secondaires définis dans la table de paramètres Types d’identifiants                                      |
| les champs utilisés dans les métadonnnées | les codes des champs utilisés dans la description des métadonnées. Un modèle d’étiquette ne peut être associé qu’à un type de métadonnées |

La seconde cellule (seconde colonne) est alors rajoutée :

~~~xml
					<fo:table-cell> 
						<fo:block>
							<fo:external-graphic>
								 <xsl:attribute name="src">
										<xsl:value-of select="concat(uid,'.png')" />
								 </xsl:attribute>
								<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
								<xsl:attribute name="height">2.5cm</xsl:attribute>
								<xsl:attribute name="content-width">2.5cm</xsl:attribute>
								<xsl:attribute name="scaling">uniform</xsl:attribute>     
							</fo:external-graphic>
						</fo:block>
					</fo:table-cell>
				</fo:table-row>
		</fo:table-body>
	</fo:table>
~~~

Ici, le QRcode est inséré (sous la forme d'un graphique dont le nom est l'UID de l'objet). La ligne est alors fermée (*</fo:table-row>*), puis le tableau.

### La partie basse de l'étiquette

La partie basse de l'étiquette est générée de la même manière, mais sans utiliser un tableau :

~~~xml
	<fo:block text-align="center">
		<fo:external-graphic>
				 <xsl:attribute name="src">
						<xsl:value-of select="concat(uid,'-2.png')" />
				 </xsl:attribute>
				<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
				<xsl:attribute name="content-width">9cm</xsl:attribute>
				<xsl:attribute name="height">1cm</xsl:attribute>
				<xsl:attribute name="scaling">uniform</xsl:attribute>     
			</fo:external-graphic>
	</fo:block>
	<fo:block text-align="center">
		Risque:<fo:inline font-weight="bold"><xsl:value-of select="clp"/></fo:inline>
	</fo:block>
~~~

Le second code optique est identifié à partir de l'UID suivi de -2.

### Terminer le modèle

Il ne reste plus qu'à fermer les balises et à indiquer au processeur fop de générer un saut de page :

~~~xml
	   <fo:block page-break-after="always"/>
	  </xsl:template>
</xsl:stylesheet>
~~~


Pour aller plus loin dans la mise en page, vous pouvez consulter la [documentation du projet FOP](https://xmlgraphics.apache.org/fop/fo.html), et pour le formatage du texte, [celle concernant XSL](https://www.w3.org/TR/xsl11).
### Code complet de l'étiquette

~~~xml
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0"
	xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
	xmlns:fo="http://www.w3.org/1999/XSL/Format">
	<xsl:output method="xml" indent="yes"/>
	<xsl:template match="objects">
		<fo:root>
			<fo:layout-master-set>
				<fo:simple-page-master master-name="label"
					  page-height="5cm" page-width="10cm" margin-left="0.5cm" margin-top="0.5cm" margin-bottom="0cm" margin-right="0.5cm">  
					  <fo:region-body/>
				</fo:simple-page-master>
			</fo:layout-master-set>
			<fo:page-sequence master-reference="label">
				<fo:flow flow-name="xsl-region-body">        
					<fo:block>
						<xsl:apply-templates select="object" />
					</fo:block>
				</fo:flow>
			</fo:page-sequence>
		</fo:root>
	</xsl:template>
	<xsl:template match="object">
		<fo:table table-layout="fixed" border-collapse="collapse"  border-style="none" width="9cm" keep-together.within-page="always">
			<fo:table-column column-width="6cm"/>
			<fo:table-column column-width="3cm" />
			<fo:table-body border-style="none" >
				<fo:table-row>
					<fo:table-cell>
						<fo:block>
							<fo:external-graphic>
								<xsl:attribute name="src">
									<xsl:value-of select="concat(label_id,'-logo.png')"/>
								</xsl:attribute>
								<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
									<xsl:attribute name="height">1cm</xsl:attribute>
									<xsl:attribute name="content-width">1cm</xsl:attribute>
									<xsl:attribute name="scaling">uniform</xsl:attribute>
								</fo:external-graphic>
								<fo:inline> Labo Collec-Science</fo:inline>
						</fo:block>
						<fo:block><fo:inline font-weight="bold"><xsl:value-of select="db"/>:<xsl:value-of select="uid"/></fo:inline></fo:block>
						<fo:block>id:<fo:inline font-weight="bold"><xsl:value-of select="id"/></fo:inline></fo:block>
					</fo:table-cell>
					<fo:table-cell> 
						<fo:block>
							<fo:external-graphic>
								 <xsl:attribute name="src">
										<xsl:value-of select="concat(uid,'.png')" />
								 </xsl:attribute>
								<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
								<xsl:attribute name="height">2.5cm</xsl:attribute>
								<xsl:attribute name="content-width">2.5cm</xsl:attribute>
								<xsl:attribute name="scaling">uniform</xsl:attribute>     
							</fo:external-graphic>
						</fo:block>
					</fo:table-cell>
				</fo:table-row>
		</fo:table-body>
	</fo:table>
	<fo:block text-align="center">
		<fo:external-graphic>
				 <xsl:attribute name="src">
						<xsl:value-of select="concat(uid,'-2.png')" />
				 </xsl:attribute>
				<xsl:attribute name="content-height">scale-to-fit</xsl:attribute>
				<xsl:attribute name="content-width">9cm</xsl:attribute>
				<xsl:attribute name="height">1cm</xsl:attribute>
				<xsl:attribute name="scaling">uniform</xsl:attribute>     
			</fo:external-graphic>
	</fo:block>
	<fo:block text-align="center">
		Risque:<fo:inline font-weight="bold"><xsl:value-of select="clp"/></fo:inline>
	</fo:block>
	   <fo:block page-break-after="always"/>
	  </xsl:template>
</xsl:stylesheet>
~~~
