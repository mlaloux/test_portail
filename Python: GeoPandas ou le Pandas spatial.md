
```Python
import geopandas as gpd
# Création d'un GeoDataFrame
gdf = gpd.read_file("test_portail.shp")
gdf.head()
```


```Python
gdf["surface"] = gdf['geometry'].area
gdf.head(2) # 2 premières lignes
