# Python: GeoPandas ou le Pandas spatial

dim 16\-10\-2016 [Martin Laloux](https://web.archive.org/web/20180831122249/http://portailsig.org/users/gene "Voir le profil utilisateur.")

*   [SIG OpenSource](https://web.archive.org/web/20180831122249/http://portailsig.org/category/actudossier/sig-opensource)

| ![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/icone/pythonlogo.jpg) |    
| **Niveau** | Intermédiaire |      
| **Logiciels utilisés** | 
**[Python 2.7.x ou Python 3.x](https://web.archive.org/web/20180831122249/https://www.python.org/)**    
**[Pandas (module Python)](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/)**    
**[GeoPandas (module Python)](https://web.archive.org/web/20180831122249/http://geopandas.org/)**   
 |
| **Plateforme** | Windows | Mac | Linux | FreeBSD |


Dans le monde géomatique, il y a ceux qui préfèrent les boutons, les menus, les pointer\-cliquer, ou glisser\-déplacer, le tout dans une jolie interface graphique (les SIGs quoi) et ceux qui préfèrent autre chose, comme la programmation directe et moi, malheureusement ou heureusement, je suis tombé dedans quand j’étais petit...

Parmi les nombreux modules Python existants, il y en a un qui me séduit de plus en plus, c’est [GeoPandas](https://web.archive.org/web/20180831122249/http://geopandas.org/) (vu sommairement dans [Python à finalité géospatiale: pourquoi débuter avec le module ogr alors qu’il existe des alternatives plus simples et plus didactiques ?](https://web.archive.org/web/20180831122249/http://www.portailsig.org/content/nouv)) de Kelsey Jordahl, car il permet de pratiquement tout faire (attributs, géométries, jointures, etc.). Comme son nom l’indique, il est intrinsèquement lié à [Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/), mais force est de constater que la plupart des géomaticiens qui utilisent Python dans leurs logiciels [SIG](https://web.archive.org/web/20180831122249/http://portailsig.org/glossary/4/letters#term28) ne connaissent pas ce dernier module et pourtant...

Créé il y a relativement peu de temps, [Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/) connaît un développement accéléré au point de devenir aujourd’hui l’un des principaux modules Python pour traiter les données de tout type ("Big Data", "Machine Learning", scientifique, économique, sociologique ...). Il s’appuie sur [NumPy](https://web.archive.org/web/20180831122249/http://www.numpy.org/) et permet de manipuler de grands volumes de données, structurées de manière simple et intuitive sous forme de tableaux.

Les exemples/tutoriels/videos sur [Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/) sont innombrables sur Internet ainsi que des livres, aussi je me limiterai ici à une simple présentation de la structure des données pour passer ensuite à [GeoPandas](https://web.archive.org/web/20180831122249/http://geopandas.org/).

### Pandas

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/pandas_logo.png)

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/pandasbase.png)

Figure modifiée de [Cheat Sheet: The pandas DataFrame Object](https://web.archive.org/web/20180831122249/http://www.webpages.uidaho.edu/%7Estevel/504/Pandas%20DataFrame%20Notes.pdf) ( Dr. Stephen Sauchi Le)

Le type de base est la Serie ([Pandas Series](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html)) qui peut être considérée comme un tableau de données à une dimension (grossièrement équivalent à une liste). L’extension en deux dimensions est un DataFrame ([Pandas DataFrame](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)). C’est un simple tableau dont les séries constituent les colonnes. Les index sont:

\- index de colonne (df.columns()): les noms des colonnes (généralement des chaînes de caractères);
\- index de ligne (df.index()): nombres entiers (numéros des lignes), chaînes de caractères, DatetimeIndex ou PeriodIndex pour les séries temporelles (time series).

C’est l’équivalent d’une matrice [NumPy](https://web.archive.org/web/20180831122249/http://www.numpy.org/) dont chaque colonne (Serie) est de même type (n’importe quel type de données, objets Python, nombres, dates, textes, binaires) et qui peut contenir des valeurs manquantes. C’est aussi l’équivalent des [Data Frame](https://web.archive.org/web/20180831122249/https://openclassrooms.com/courses/effectuez-vos-etudes-statistiques-avec-r/les-tableaux-de-donnees-dataframes) de [R](https://web.archive.org/web/20180831122249/https://www.r-project.org/) (il y a aussi moyen de travailler avec des données selon 3 dimensions ou plus avec les [Pandas Panels](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Panel.html/), mais le sujet ne sera pas abordé ici).

Cette manière de représenter les données oblige à changer quelque peu les habitudes de programmation. On travaille sur des colonnes, des lignes ou des cellules au lieu de parcourir l’ensemble des données avec des boucles et/ou des boucles imbriquées. Par exemple, pour modifier toutes les valeurs d'une colonne on utilisera [pandas.Series.map(fonction)](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.map.html).

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/pandas_col_ligne.png)

Pandas permet nativement:

*   la création et l'exportation de tables de données à partir d'objets Python (listes, dictionnaires, arrays NumPy,..), de fichiers textes (séparateurs, .csv, format fixe, compressés), de fichiers Excel ou LibreOffice, de fichiers HTML, XML, JSON ou à partir de nombreux systèmes de bases de données ([Pandas: IO Tools (Text, CSV, HDF5, ...)](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/io.html#io-html) ;
*   la gestion des tables : sélection des lignes, colonnes, gestion des types et formats, transformations, réorganisation, discrétisation de variables quantitatives, traitement des données manquantes, permutation et échantillonnage aléatoire, variables indicatrices, chaînes de caractères...([Pandas: Intro to Data Structure)](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/dsintro.html);
*   les statistiques élémentaires uni et bivariées, les statistiques par groupe, les détections élémentaires de valeurs atypiques et les graphiques associés...([Pandas: Computational tools](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/computation.html)):
*   les manipulation de tables : concaténations, agrégations, fusions, jointures, tri .([Pandas: Group By: split\-apply\-combine](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/groupby.html), [Pandas: Merge, join, and concatenate](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/merging.html), [Pandas: Database\-style DataFrame joining/merging](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/merging.html#database-style-dataframe-joining-merging), [Pandas: Reshaping and Pivot Tables](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/reshaping.html), ...)

Cette librairie n'est pas isolée, car un grand nombre de modules se sont développes autour de sa structure pour offrir des traitements supplémentaires. C'est l'[Ecosystème Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/pandas-docs/stable/ecosystem.html). Il est de plus, tout à fait possible d'utiliser [Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/) avec une multitude d'autres librairies Python.  Autant dire que ses possibilités deviennent presque infinies, d'où son succès actuel.

> "Essentially, you can think of pandas as a Numpy "on steroids" with a focus on real\-world data. It encapsulates and wraps around much of the low\-level functionality of numpy, scipy and matplotlib, exposing it to the end\-user in a much friendlier way." (tiré de [Brief introduction to the Python stack for scientific computing](https://web.archive.org/web/20180831122249/https://github.com/pysal/notebooks/blob/466656186fabd046617cf28024daf12a2257b469/notebooks/intro_scicomp_python.ipynb))

### GeoPandas

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/geopandas_0.png)

Figure réalisée avec GeoPandas (Delaunay, Voronoï) en s'inspirant de [Origami Panda Print](https://web.archive.org/web/20180831122249/https://www.etsy.com/listing/231278536/origami-panda-print-bear-print-origami)

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/geopandas.png)

Le monde géospatial ne pouvait pas rester en reste d'où la création de [GeoPandas](https://web.archive.org/web/20180831122249/http://geopandas.org/) qui est une extension geospatiale de Pandas. Elle rajoute les GeoSeries (géométries, en bleu clair) et les GeoDataFrames ou DataFrames avec une colonne GeoSerie aux structures de Pandas ([GeoPandas: Data Structures](https://web.archive.org/web/20180831122249/http://geopandas.org/data_structures.html)). Le résultat final est une structure où tous les traitements de Pandas sont possibles sur les colonnes oranges (attributs, Panda Series) et les traitements géomatiques sur la colonne bleu clair (geospatial, Geopandas GeoSerie). En pratique une GeoSerie est constituée de géométries [Shapely. ](https://web.archive.org/web/20180831122249/http://toblerity.org/shapely/manual.html) Une ligne d'un GeoDataFrame contient donc les attributs et la géométrie d'un élément.

GeoPandas utilise donc [Shapely](https://web.archive.org/web/20180831122249/http://toblerity.org/shapely/manual.html) (pour les traitements géométriques), mais aussi [Fiona](https://web.archive.org/web/20180831122249/http://toblerity.org/fiona/manual.html) (pour l'importation/exportation des données géospatiales), [pyproj](https://web.archive.org/web/20180831122249/https://github.com/jswhit/pyproj) (pour le traitement des projections), éventuellement [Rtree](https://web.archive.org/web/20180831122249/http://toblerity.org/rtree/) (facultatif, pour implémenter les index spatiaux) et [matplotlib](https://web.archive.org/web/20180831122249/http://matplotlib.org/) et [descartes](https://web.archive.org/web/20180831122249/https://pypi.python.org/pypi/descartes/1.0.2) pour les graphismes. Hormis Rtree, tous ces modules doivent être préalablement installés, [Pandas](https://web.archive.org/web/20180831122249/http://pandas.pydata.org/) y compris, bien évidemment. Le tout est particulièrement bien adapté aux [Jupyter/IPython notebooks](https://web.archive.org/web/20180831122249/https://ipython.org/notebook.html) (voir [Les notebooks IPython comme outil de travail dans le domaine géospatial ou le plaisir de partager, de collaborer et de communiquer](https://web.archive.org/web/20180831122249/http://www.portailsig.org/content/les-notebooks-ipython-comme-outil-de-travail-dans-le-domaine-geospatial-ou-le-plaisir-de-par)) sur le Portail).

### Quelques principes

Ouvrir et sauvegarder un fichier shapefile (ou autre) est enfantin et a été vu dans [Python à finalité géospatiale: pourquoi débuter avec le module ogr alors qu'il existe des alternatives plus simples et plus didactiques ?](https://web.archive.org/web/20180831122249/http://www.portailsig.org/content/nouv)

#### Le fichier shapefile d'origine

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/depart.png)

#### Transformation en GeoDataFrame

```Python
import geopandas as gpd
# Création d'un GeoDataFrame
gdf = gpd.read_file("test_portail.shp")
gdf.head()
```
![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/original.png)

#### Quelques manipulation avec Pandas

À ce stade il est possible de modifier la table (ajout/suppression d'un champ par exemple), d'appliquer toutes les fonctions de Pandas pour ajouter/manipuler les attributs, de traiter l'ensemble d'une colonne (somme, moyenne, ...) ou de plusieurs colonnes (corrélations, ...)

*   Ajout d'un nouveau champ, soit avec une fonction de Pandas soit avec une fonction de GeoPandas (ici):

```Python
gdf["surface"] = gdf['geometry'].area
gdf.head(2) # 2 premières lignes
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/surface.png)

*   Quelques statistiques basiques:

```Python
gdf[['Zn','Pb']].describe().transpose()
```

 ![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/stats1.png)
 
 ```Python
gdf[['Zn','Pb']].cov() # covariance
```
 ![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/stats2.png)

À tout moment il y a la possibilité de sauver le GeoDataFrame résultant

```Python
gdf.to_file("resultat.shp")
```

Je vous laisse découvrir Pandas pour tous les traitements possibles (une multitude), car ce qui nous intéresse ici ce sont les traitements géomatiques.

#### Quelques manipulations géométriques avec GeoPandas

Je vais vous montrer ici comment convertir ce GeoDataFrame en 4 fichiers shapefiles tout en gardant les attributs en illustrant les manières de procéder (je repars du fichier original):

*   la transformation de polygones en points se fera avec la fonction centroid de GeoPandas;
*   la transformation de polygones en lignes se fera avec Shapely et la commande map de GeoPandas et les [fonctions lambda](https://web.archive.org/web/20180831122249/http://sametmax.com/fonctions-anonymes-en-python-ou-lambda/) puisque la commande native n'existe pas et qu'il est nécessaire d'appliquer la fonction à chaque élément de la GeoSerie;
*   la transformation de lignes en points se fera de la même manière, mais le résultat aura évidemment plus de lignes.

Je vais sans doute être un peu long pour certains, mais il faut bien comprendre ici les manipulations géométriques sous peine d’être perdu dans la suite.

*   Transformation du GeoDataFrame en fichier shapefile de type point

```Python
# copie du GeoDataFrame original
points = gdf.copy()
points.geometry = points['geometry'].centroid
 # même crs que l'original
points.crs = gdf.crs
# sauvetage du fichier shapefile
points.to_file('centroid_portail.shp')
points.head()
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/geom_points.png)

*   Transformation du GeoDataFrame en shapefile de type polylignes. Ici il est nécessaire d'utiliser une fonction extérieure puis d'utiliser la fonction map
```Python
from shapely.geometry import LineString
# la fonction de transformation de polygones en polylignes
linear = gdf.copy()
def convert(geom):
    return LineString(list(geom.exterior.coords))
# application de la fonction à toutes les lignes de la colonne geometry
linear.geometry= linear.geometry.map(convert, linear['geometry'])
# ou directement avec les fonctions lambdas
linear.geometry= linear.geometry.map(lambda x: LineString(list(x.exterior.coords)))
linear.crs = gdf.crs
linear.head()
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/geom_line.png)

*   Extraction des noeuds des polylignes: ici il faut extraire les noeuds des lignes (LineString) de linear et créer un nouveau GeoDataFrame

```Python
col = linear.columns.tolist()[0:4]
print col
[u'POLY_NUM_B', u'Pb', u'Zn', 'geometry']
# création d'un nouveau GeoDataFrame avec ces colonnes
noeuds = gpd.GeoDataFrame(columns=col)
# extraction des noeuds à partir des lignes présentes dans linear et des valeurs d'attributs et intégration dans le nouveau GeoDataFrame
for index, row in linear.iterrows():
for j in list(row['geometry'].coords):
        noeuds = noeuds.append({'POLY_NUM_B': int(row['POLY_NUM_B']), 'Pb':row['Pb'],'Zn':row['Zn'], 'geometry':Point(j) },ignore_index=True)
noeuds.crs = {'init' :'epsg:31370'} # autre manière de spécifier les coordonnées
```

Comme je veux être sûr que mes valeurs soient de type entier, je le spécifie:

```Python
noeuds['POLY_NUM_B'] = noeuds['POLY_NUM_B'].astype('int')
noeuds['Pb'] = noeuds['Pb'].astype('int')
noeuds['Zn'] = noeuds['Zn'].astype('int')
# affichage des éléments 8 à 16
noeuds[8:16]
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/point_sur_ligne.png)

*   je crée maintenant un buffer autour de ces points
```Python
buffer = df.copy()
buffer.geometry = buffer['geometry'].buffer(5)
etc.
```

*   Résultat

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/restot.png)

### En pratique

1) Une des plus belles illustrations de la puissance de GeoPandas m'a été apportée suite à une de mes réponses sur [GIS Stack Exchange](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/). La question posée était "More Efficient Spatial join in Python without QGIS, ArcGIS, PostGIS, etc". J'ai répondu avec une solution classique de boucles imbriquées en parcourant les 2 fichiers shapefiles ([ma réponse](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/a/103066)) à comparer avec [la réponse avec GeoPandas](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/a/165413) qui illustre les jointures spatiales ([GeoPandas: spatial joins](https://web.archive.org/web/20180831122249/https://github.com/geopandas/geopandas/blob/master/examples/spatial_joins.ipynb))

```Python
points = geopandas.GeoDataFrame.from_file('points.shp') # or geojson etc
polys = geopandas.GeoDataFrame.from_file('polys.shp')
pointInPoly = gpd.sjoin(points, polys, how='left',op='within')
```

Et vous obtiendrez un GeoDataFrame avec tous les points de 'points.shp' qui sont dans les polygones de 'polys.shp'.

2) Transformer un fichier csv ou Excel en GeoDataFrame est très facile:

```Python
import pandas as pd
# transformation du fichier csv en Pandas DataFrame
points = pd.read_csv("strati.csv")
#transformation en GeoDataFrame
from shapely.geometry import Point
geometrie = [Point(xy) for xy in zip(points.x, points.y)] # colonnes du DataFrame résultants
points = gpd.GeoDataFrame(points,geometry=geometrie)
# ou directement
points = pd.read_csv("strati.csv")
points['geometry'] = points.apply(lambda p: Point(p.x, p.y), axis=1)
```

3) fusionner 2 ou plusieurs shapefiles, quelque soit le nombre et le type de champs, pourvu que le type de géométrie soit le même:
```Python
a = gpd.GeoDataFrame.from_file("shape1.shp")
b = gpd.GeoDataFrame.from_file("shape2.shp")
import pandas as pd
result = pd.concat([a,b],axis=0)
result.to_file("merged.shp")
```

4) un cas pratique auquel j'ai été confronté. J'ai un fichier shapefile reprenant les affleurements géologiques d'une carte (lignes) et un fichier csv avec leurs descriptions et je voudrai extraire les valeurs de schistosité de chacun d'entre eux pour créer un nouveau fichier shapefile de type point:
```Python
import geopandas as gpd
import pandas as pd
import re
affl = gpd.GeoDataFrame.from_file("aff.shp")
affl.head(2)
```

 ![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/affl1.png)

Traitement du fichier csv
```Python
affleurs = "schisto.csv"
# je choisis les colonnes que je veux importer
u_cols = ['IDENT','desc']
affleurs = pd.read_csv(aff, sep='\t', names=u_cols)
regex = re.compile("S1.\d{1,2}\W*\d{1,3}")
# je saute la partie du script pour chercher le regex et le résultat est
affleurs.head(2) # les 2 premiers éléments
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/affl2.png)

Je joins les 2 DataFrames sur base du champ 'IDENT' et je modifie la géométrie
```Python
df2 = gpd.GeoDataFrame( pd.merge(affl, affleurs, on='IDENT'))
df2['geometry'] = df2['geometry'].representative_point()
df2.head(2)
```

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/affl4.png)

Résultat:

![](https://web.archive.org/web/20180831122249im_/http://www.portailsig.org/sites/default/files/images/illustration/geopandas/resultat.png)

4) Pour le reste je vous renvoie (le choix n'est pas exhaustif):

\- aux exemples de Geopandas (notebooks Jupyter/IPython):

*   [Prototyping choropleth classification schemes from PySAL for use with GeoPandas](https://web.archive.org/web/20180831122249/https://github.com/geopandas/geopandas/blob/master/examples/choropleths.ipynb)
*   [GeoPandas: Overlays](https://web.archive.org/web/20180831122249/https://github.com/geopandas/geopandas/blob/master/examples/overlays.ipynb>)
*   [GeoPandas: Spatial Joins](https://web.archive.org/web/20180831122249/https://github.com/geopandas/geopandas/blob/master/examples/spatial_joins.ipynb)

\- à mes réponses ou à celles d'autres personnes sur [GIS Stack Exchange](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/) ou [Stack Overflow](https://web.archive.org/web/20180831122249/http://stackoverflow.com/):

*   [Finding if point exists in shapefile using shapely performance?](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/questions/210942/finding-if-point-exists-in-shapefile-using-shapely-performance/210999#210999)
*   [Check if a point falls within a multipolygon with Python](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/questions/208546/check-if-a-point-falls-within-a-multipolygon-with-python/208574#208574)
*   [Merging overlapping features using Geopandas?](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/questions/202958/merging-overlapping-features-using-geopandas/203044#203044)
*   [How to convert multiple csv files to shp using python and no arcpy?](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/questions/197825/how-to-convert-multiple-csv-files-to-shp-using-python-and-no-arcpy/197863#197863)
*   [Turn a GeoDataFrame of x,y coordinates into Linestrings using GROUPBY?](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/a/202274)
*   [How to check what changed inside the updated shapefile?](https://web.archive.org/web/20180831122249/http://gis.stackexchange.com/a/212336)
*   [How to create a Feature Collection from a GeoJSON](https://web.archive.org/web/20180831122249/http://stackoverflow.com/a/37854687)
*   [Write GeoDataFrame into SQL Database](https://web.archive.org/web/20180831122249/http://stackoverflow.com/a/38363154)

\- à des exemples de combinaisons avec d'autres librairies:

*   [Mapping in Python with geopandas](https://web.archive.org/web/20180831122249/http://darribas.org/gds15/content/labs/lab_03.html) (notebook Jupyter/IPython)
*   [Basic Interactive Geospatial Analysis in Python](https://web.archive.org/web/20180831122249/http://blog.yhat.com/posts/interactive-geospatial-analysis.html)
*   [Geodata manipulation with GeoPandas: Third in a series on scikit\-learn and GeoPandas](https://web.archive.org/web/20180831122249/https://michelleful.github.io/code-blog/2015/04/29/geopandas-manipulation/)
*   [Prepare data for clustering lab](https://web.archive.org/web/20180831122249/http://darribas.org/gds15/content/labs/lab_08_airbnb_data_prep.html) (notebook Jupyter/IPython)
*   [Clustering, spatial clustering, and geodemographics](https://web.archive.org/web/20180831122249/http://darribas.org/gds15/content/labs/lab_08.html) (notebook Jupyter/IPython)
*   [Programming a seismic program](https://web.archive.org/web/20180831122249/https://github.com/agile-geoscience/notebooks/blob/master/Programming_a_seismic_program.ipynb) (notebook Jupyter/IPython)

### Conclusions

Contrairement à la plupart des tutoriels, je n'ai pas développé ici les fonctionnalités graphiques de la librairie puisque j'utilise un logiciel [SIG](https://web.archive.org/web/20180831122249/http://portailsig.org/glossary/4/letters#term28) pour visualiser les résultats. GeoPandas est encore jeune, mais ses possibilités sont déjà énormes, si vous aimez programmer, bien entendu. Dans mon cas, les traitements sont beaucoup plus rapides qu'avec QGIS pour ce que je veux faire (je ne dois pas utiliser PyQGIS, PyGRASS et leurs contraintes pour travailler sur des fichiers shapefiles. Tant que la colonne *geometry* d'un GeoDataFrame demeure inchangée, il y a moyen de faire ce que l'on veut avec les attributs).

Du fait que la librairie utilise Fiona, elle est sujette aux mêmes restrictions (pas d'accès direct aux bases de données spatiales par exemple), mais il est possible de contourner cet aspect avec d'autres modules plus adéquats. De part sa jeunesse elle est encore sujette à des erreurs non rédhibitoires (voir [GeoPandas commits](https://web.archive.org/web/20180831122249/https://github.com/geopandas/geopandas/commits/master)).

Signalons aussi [OSMnx](https://web.archive.org/web/20180831122249/https://github.com/gboeing/osmnx), pour le traitement des couches OpenStreetMap avec Pandas et  [GeoRasters](https://web.archive.org/web/20180831122249/https://github.com/ozak/georasters) qui se veut l'équivalent de GeoPandas pour les rasters.

Tous les traitements présentés ont été effectués sur Mac OS X, Linux ou Windows avec les versions 0.1.x, 0.2.0 et 0.2.1 de GeoPandas et les versions 0.18.x puis 0.19.0 de Pandas.

![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_great_britain.gif) **Site officiel :** [Using geopandas on Windows](https://web.archive.org/web/20180831122249/http://geoffboeing.com/2014/09/using-geopandas-windows/)    
![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_great_britain.gif) **Site officiel :** [Pandas DataFrame Notes (PDF)](https://web.archive.org/web/20180831122249/http://www.webpages.uidaho.edu/~stevel/504/Pandas%20DataFrame%20Notes.pdf)   
![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_france.gif) **Site officiel :** [DataFrame et Matrice](https://web.archive.org/web/20180831122249/http://www.xavierdupre.fr/app/ensae_teaching_cs/helpsphinx/notebooks/td1a_cenonce_session_10.html)   
![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_france.gif) **Site officiel :** [DataFrame et Graphes](https://web.archive.org/web/20180831122249/http://www.xavierdupre.fr/app/ensae_teaching_cs/helpsphinx/notebooks/td2a_cenonce_session_1.html)   
![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_france.gif) **Site officiel :** [Le pandas c’est bon, mangez en](https://web.archive.org/web/20180831122249/http://sametmax.com/le-pandas-cest-bon-mangez-en/)   
![](https://web.archive.org/web/20180831122249im_/http://portailsig.org/sites/default/files/images/drapeau/flag_france.gif) **Site officiel :** [Introduction à Pandas](https://web.archive.org/web/20180831122249/http://www.python-simple.com/python-pandas/panda-intro.php)    
