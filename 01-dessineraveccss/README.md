# Bienvenue dans cette première leçon

Nous allons nous amuser un peu avec le HTML et les CSS pour expérimenter les possibilités offertes par ces langages.

## Dessiner un logo

Pour débuter nous allons ouvrir le fichier index.html dans lequel nous allons insérer l'ensemble du code nécessaire.

1. ** Faire un fork du dossier sur github ** - Créez vous un compte, si pas déjà fait, cliquer sur le lien en haut à droite _fork_ de cette page
2. ** Cloner le projet dans un répertoire local ** - Consulter la leçon #00 ou les aides appropriées
3. ** Ouvrir un éditeur de texte ** - Consulter la leçon #00 ou les aides appropriées

Vous devez maintenant avoir le fichier index.html ouvert.

### Contenu du fichier

#### Composition du code

Vous devez voir apparaître une division `<div>` qui contient 8 autres divisions.
La division parente représente la _tête_, elle comprend 7 autres divisions qui représentent :

* L'oreille 1
* L'oreille 2
* Le visage
* L'oeil 1
* L'oeil 1
* Le nez
* La dent 1
* La dent 2
* La bouche

Nous allons représenter une tête de souris en HTML et CSS. Si vous ouvrez (double clic) le fichier index.html dans un navigateur, vous observerez un carré entouré d'un liseré gris pointillé. Ce motif va vous servir de canevas pour le logo.

Dans votre éditeur de texte vous pouvez voir une ligne telle que celle-ci :

~~~

<div id="figure" style="position:relative;width:150px;height:150px;border:1px dotted #ccc;">

~~~

#### Les attributs

*1. L'attribut _id_*
L'attribut _id_ permet de nommer une balise en HTML, de donner un nom à un élément ; ici _figure_. Une _id_ est unique dans une page, il ne peut y avoir 2 éléments avec une id identique.
Le deuxième attribut présent est _style_, cet attribut permet d'indiquer des styles une élément HTML.

*2. L'attribut _style_*
L'élément _style_ permet d'insérer ce qu'on appelle des styles en ligne ; il était utilisé au début du web, alors que les CSS (fichier de définition des styles n'existaient pas encore). L'attribut est toujours fonctionnel mais peu pratique pour la mutualisation de styles entre plusieurs balises et la maintenance d'un site.

A l'intérieur de cet attribut, il est possible d'indiquer un certain nombre de propriétés afin de mettre en forme un élément HTML, dans notre cas une division `<div>`, une boîte.
	
Pour commencer nous allons jouer avec des propriétés de dimension, de bordures, de positionnement et de couleur :

* width : largeur, défini la largeur d'une boîte
* height : hauteur, défini la hauteur d'une boîte
* border : bordure, défini la taille, le style et la couleur d'une bordure
* top/left/right/bottom : défini le positionnement absolu d'une boîte.

~~~

<div id="figure" style="width:150px;height:150px;border:#cccccc 1px dotted;">
	<div id="ear1"></div><!--#ear1-->
	<div id="ear2"></div><!--#ear2-->
	<div id="face"></div><!--#face-->
	<div id="eye1"></div><!--#eye1-->
	<div id="eye2"></div><!--#eye2-->
	<div id="noze"></div><!--#noze-->	
	<div id="tooth1"></div><!--#tooth1-->
	<div id="tooth2"></div><!--#tooth2-->
	<div id="mouth"></div><!--#mouth-->
</div>

~~~ 

Dans le code ci-dessus, vous avez donc une boîte `<div>` qui se nomme _figure_ (id="figure"), ayant pour dimension 150px de largeur par 150px de hauteur et avec une bordure de 1px de large en pointillé de couleur grise (code : #cccccc).
	
Les autres boîtes sont invisibles car aucun style ne sont appliqués sur celles-ci.

### Dessiner & placer les éléments

#### Placer l'oreille droite de la souris

Dans la boîte parente, nous allons pouvoir dessiner chacun des organes de notre souris en stylisant chacune des boîtes. Dessinons une oreille, la droite (se trouvera à gauche sur notre dessin).

Cette oreille va se trouver sur le bord gauche et supérieur de notre boîte englobante (_figure_). Sa position est donc (0:0), soit 0 pixel du bord gauche et 0 pixel du bord supérieur. Ce qui se traduit par les propriétés _top_ et _left_ avec des valeurs de 0 pixel.
On ajoutera des propriétés de largeur (50 pixels), hauteur (50 pixels) et de bordure (1 pixel de large, plein et noire) pour voir s'afficher cette boîte.

~~~

<div id="ear1" style="top:0;left:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear1-->

~~~

La boîte _ear1_ est bien alignée en haut et à gauche de la boîte parente, tout va bien. Plaçons maintenant l'oreille gauche de la souris. Les propriétés sont identiques à l'exception du positionnement horizontal, nous allons donc retirer la propriété left pour la remplacer par right.
La boîte sera donc placée à 0 pixel du bord droit de la boîte parente.

~~~

<div id="ear2" style="top:0;right:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear2-->

~~~

#### Placer l'oreille droite de la souris

Hmmmmmm, moui, la boîte _ear2_ est placée en dessous de la boîte _ear1_ ? Que se passe-t-il ? Pourquoi le navigateur ne prend pas en compte la valeur de positionnement ? 

Tout simplement parce que, par défaut, le navigateur positionne les éléments les un à la suite des autres (dans le flux, comme actuellement). L'indication de propriétés de positionnement ne suffisent pas à passer dans un mode absolu ; à sortir les boîtes du flux de la page.
Pour sortir un élément du flux, il faut indiquer une propriété supplémentaire : _position_ avec comme valeur _absolute_.

~~~

<div id="ear1" style="position:absolute;top:0;left:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear1-->
<div id="ear2" style="position:absolute;top:0;right:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear2-->

~~~

Formidable, les boîtes sont hors du flux et sont positionnées de manière absolue... dans la page. L'oreille gauche de la souris est située en haut et à droite de la page et non de la boîte parente... dommage. Pourquoi ce fonctionnement ?

Les éléments positionnés en absolu le sont par rapport au premier parent avec la propriété _position_ en mode _relative_. Or dans notre cas, il s'agit de la page entière, rien ne dit à notre boîte englobante de prendre le mode _relative_.
Essayons pour voir, ajoutons position:relative; à l'élément _figure_ !

~~~

<div id="figure" style="position:relative;width:150px;height:150px;border:#cccccc 1px dotted;">
	<div id="ear1" style="position:absolute;top:0;left:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear1-->
	<div id="ear2" style="position:absolute;top:0;right:0;width:50px;height:50px;border:black 1px solid;"></div><!--#ear2-->
	<div id="face"></div><!--#face-->
	<div id="eye1"></div><!--#eye1-->
	<div id="eye2"></div><!--#eye2-->
	<div id="noze"></div><!--#noze-->	
	<div id="tooth1"></div><!--#tooth1-->
	<div id="tooth2"></div><!--#tooth2-->
	<div id="mouth"></div><!--#mouth-->
</div>

~~~

Formidable, les éléments se positionnent en mode _absolute_ dans leur boîte parente. Il s'agit d'une des règles les moins évidentes à comprendre lorsqu'on commence à mettre en forme des éléments HTML : faire la différence entre les mode _relative_ et _absolute_.

Maintenant, plaçons les boîtes restantes. Je vous donne les éléments à droite du visage de la souris à vous de placer ceux de gauche et de centrer le nez.

~~~

<div id="figure" style="position:relative;width:150px;height:150px;border:#cccccc 1px dotted;">
	<div id="ear1" style="position:absolute;top:0;left:0;width:50px;height:50px;border:1px solid;"></div><!--#ear1-->
	<div id="ear2" style="position:absolute;top:0;right:0;width:50px;height:50px;border:1px solid;"></div><!--#ear2-->
	<div id="face" style="position:absolute;top:30px;left:40px;width:70px;height:80px;border:1px solid;"></div><!--#face-->
	<div id="eye1" style="position:absolute;top:60px;left:50px;width:10px;height:1px;border:1px solid;"></div><!--#eye1-->
	<div id="eye2" style=""></div><!--#eye2-->
	<div id="noze" style="position:absolute;top:90px;left:0;width:10px;height:10px;border:1px solid;"></div><!--#noze-->	
	<div id="tooth1" style="position:absolute;top:111px;left:65px;width:10px;height:15px;border:1px solid;"></div><!--#tooth1-->
	<div id="tooth2" style=""></div><!--#tooth2-->
	<div id="mouth"></div><!--#mouth-->
</div>

~~~

Le dessin est simple, les boîtes peu nombreuses, la réalisation est agréable pour une première leçon ; mais pensez dès maintenant à la manière dont on peut maintenir un tel code.

Continuons et mettons un peu de couleur à tout cela grâce à la propriété _background_. Il est possible d'indiquer aussi bien des valeurs hexadécimale que des noms de couleurs interprétées par le navigateur, à vous de colorer les éléments :

* Les oreilles :: background:black;
* Le visage :: background:seashell;
* Les yeux :: background:grey;
* Le nez :: background:black;

~~~

<div id="figure" style="position:relative;width:150px;height:150px;border:#cccccc 1px dotted;background:black;">
	<div id="ear1" style="position:absolute;top:0;left:0;width:50px;height:50px;border:1px solid;"></div><!--#ear1-->
	<div id="ear2" style="position:absolute;top:0;right:0;width:50px;height:50px;border:1px solid;"></div><!--#ear2-->
	<div id="face" style="position:absolute;top:30px;left:40px;width:70px;height:80px;border:1px solid;"></div><!--#face-->
	<div id="eye1" style="position:absolute;top:60px;left:50px;width:10px;height:1px;border:1px solid;"></div><!--#eye1-->
	<div id="eye2" style=""></div><!--#eye2-->
	<div id="noze" style="position:absolute;top:90px;left:0;width:10px;height:10px;border:1px solid;"></div><!--#noze-->	
	<div id="tooth1" style="position:absolute;top:111px;left:65px;width:10px;height:15px;border:1px solid;"></div><!--#tooth1-->
	<div id="tooth2" style=""></div><!--#tooth2-->
	<div id="mouth" style=""></div><!--#mouth-->
</div>

~~~

Voilà, vous avez votre petite souris qui va faire office de logo de votre prochain site.



