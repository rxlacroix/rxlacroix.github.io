# Carte de Vidal de la Blache avec QGIS

On reproduit ici avec QGIS la carte scolaire de Vidal de la Blache sur le relief de la France : 

![](https://i.imgur.com/dKTamjr.jpg)


## Matériaux

Police : Francois One (gratuite, https://fonts.google.com/specimen/Francois+One)

Données : proviennent d'un peu partout selon leur praticité
* le réseau hydrographique : 15sec SHAPE River Network (https://www.eea.europa.eu/data-and-maps/data/external/15sec-shape-river-network) afin de pouvoir faire varier l'épaisseur des cours d'eau de façon plus adéquate
* les lacs : BD Topo Hydro Surfacique (https://geoservices.ign.fr/documentation/diffusion/telechargement-donnees-libres.html)
* les villes : AdminExpress-COG (https://geoservices.ign.fr/documentation/diffusion/telechargement-donnees-libres.html#admin-express)
* les frontières terrestres : GISCO (https://gisco-services.ec.europa.eu/distribution/v1/countries-2016.html)
* le relief : j'utilise un modèle qui compile les données ALOSv3 rééchantillonnées à 50m sur la France métropolitaine "élargie", disponible au téléchargement [ici ](https://drive.switch.ch/index.php/s/uMkpZOENrlhVicZ)


## Réalisation

L'échelle originale est au 1/1.100.000e, mais j'ai préféré descendre au 1/550.000e pour avoir plus de souplesse pour travailler.

L'essentiel du travail a concerné le placement des étiquettes des massifs montagneux et autres éléments toponymiques. Pour plus de liberté, il s'agit d'une couche de lignes dont les labels suivent la géométrie (théoriquement, en pratique ils sont bougés de façon à s'adapter au contexte).

Vous pouvez télécharger 
* le .tif géographique (Lambert-93, EPSG:2154) ici : https://drive.switch.ch/index.php/s/oYTzUKWEQPIL3CK
* le .tif géographique sans les toponymes ici : https://drive.switch.ch/index.php/s/6O5O0xofIj1qiSQ
* les données vectorielles ici : https://drive.switch.ch/index.php/s/cIMlq9EblxtNDw3
* le projet qgis ici : https://drive.switch.ch/index.php/s/BsfkgioqyMnNYVs

Malgré mes efforts, je n'arrive pas à faire en sorte que la couche d'étiquettes reste stable après partage du projet et des fichiers aussi, il faudra pour le moment vous contenter d'un projet à retoucher chez soi, en échelle 1:550000e.
