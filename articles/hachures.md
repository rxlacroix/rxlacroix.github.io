# Hachures

On essaye de reproduire ici avec QGIS des hachures  : 

![](https://image.prntscr.com/image/p-W3wpaWQX_AZC8Qjyzzjw.png)


## Matériaux

Données : un raster projeté ni trop dégueu, ni trop gros on est par exemple ici sur du 790*623 avec une résolution de 25m


## Réalisation

On utilise d'abord l'algorithme de SAGA "Gradient vectors from surface" avec les paramètres suivants :
  - Step : 1
  - Size Range Min : 0
  - Size Range Max : 500
  - Aggregation : mean value
  - Style : simple line
  
On obtient une couche avec des lignes qui partent de chaque centre de cellule orientées selon le gradient moyen de déformation du terrain :

![](https://image.prntscr.com/image/zQT_c7hnTSykRT8yb4hcXw.png)

Il faut filtrer les entités ayant une déformation très faible (peu de pente), on fait donc un clic-droit sur la couche, filtrer, avec l'expression LEN > 0.1

![](https://image.prntscr.com/image/LS-YHEQMQda1kowAcGAnzQ.png)

L'idée est maintenant de fusionner les lignes très proches pour obtenir un semblant de généralisation en courbe, pour le moment je n'arrive pas à trouver mieux qu'une polyligne mais selon l'échelle de visualisation c'est suffisant. Pour cela, on utilise l'algorithme "Snap Geometries to Layer" avec les paramètres suivants :
  - Input : la couche filtrée
  - Reference layer : la couche filtrée aussi
  - Tolerance : 10m (éventuellement à adapter suivant la résolution de la couche)
  - Behavior : Prefer closest point, don't insert new vertices
  
![](https://image.prntscr.com/image/16Eot-T2RcyL484Yb1EKWw.png)

On a nos lignes à peu près continues, on lance ensuite une série de "Fix geometries" + "Merge lines" + "Fix geometries"
![](https://image.prntscr.com/image/jaCpauIKTJ2_x98OGwRyCQ.png)

Cela donne un résultat assez convaincant, mais en traficotant le style il y a moyen d'améliorer un peu : pour cela j'utilise une palette de gris dégradée sur les quantiles de l'intensité de la déformation du terrain 

![](https://image.prntscr.com/image/MeGqEGY5TSGGplMl5fiKRw.png)

Je trouve le résultat assez satisfaisant :)

![](https://image.prntscr.com/image/LK_CxvaSS2OZdVX9yhpFbQ.png)

Bonus : en plus il y a l'attribut d'azimuth qui est disponible, on peut alors s'amuser avec !

![](https://image.prntscr.com/image/N0oMKBpFTAWVqzQuXybMnw.png)


-----------

J'ai fait un *modèle pour QGIS* qui reprend les différentes étapes, vous pouvez le télécharger ici : 
