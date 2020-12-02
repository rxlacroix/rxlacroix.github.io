# Des courbes à la WEB du Bois

![](https://david.frigge.nz/30DayMapChallenge2020/maps/lacxrx_20.jpg)

Je suis assez admiratif de la dataviz dans les travaux de WEB du Bois et j'avais envie de créer une figure de ce type avec QGIS lors du [#30DayMapChallenge](https://twitter.com/search?q=%2330DayMapChallenge&src=typeahead_click).


![](https://images-na.ssl-images-amazon.com/images/I/41GMSpOgPbL._AC_UL600_SR429,600_.jpg)

# Données

Pour les besoins de l'exemple et pour la reproductibilité, j'utilise ici les données dispo par défaut dans QGIS, à savoir les pays du monde (vous pouvez obtenir la couche en tapant world dans l'input des coordonnées en bas au centre).
Pour plus de commodité dans les distances des tampons, on passe la couche dans un système métrique, par exemple EPSG:3857.

# Premiers tâtonnements avec le générateur de géométrie de QGIS

L'idée n'était pas de faire exactement une figure s'enroulant en spirale, mais simplement des arcs de cercles concentriques.

Pour cela, on prend la fonction wedge_buffer, qui sert en principe à faire des morceaux de disque, ou des parts de camembert. Elle accepte les arguments suivants :
- center : le centre du camembert 
- azimuth : l'angle (en degrés) du milieu de la part de camembert
- width : l'angle (en degrés) d'épaisseur de la part de camembert
- outer_radius : le rayon du camembert
- inner_radius : le rayon interne de la part de camembert que l'on veut enlever dans notre exemple

Par exemple, pour une part d'un angle de 90°, dans la direction nord, d'une largeur de 500 km depuis le centroïde des pays on écrira dans le générateur de géométrie (polygône) :
wedge_buffer(centroid($geometry),0,90,500000,0)

Cela donne le résultat suivant : 

![](https://i.imgur.com/Tn0wQ6H.png)

Si on veut alors une bande de 100km d'épaisseur en bordure externe on donne un inner_radius positif : 
wedge_buffer(centroid($geometry),0,90,500000,400000)
![](https://i.imgur.com/ijtqVJZ.png)

Bon on commence à voir à peu près la forme voulue, maintenant le placement

# Placement

On veut que notre buffer se propage depuis le 0° "nord", mais seulement d'un côté. Là il part dans les deux directions, c'est pas simple à lire.





