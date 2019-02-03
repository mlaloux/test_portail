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
