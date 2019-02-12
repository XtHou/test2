# Overview of tools for creating data maps

There are now a wide range of tools that can be used to create data maps. Business intelligence tools like Tableau provide basic data map functionality while R and Python both have packages for creating data maps. Those in R include **ggmap** and **Leaflet**. However if you need to do a lot of spatial data analysis then you should think about using specialised GIS software.

## GIS

Geographic Information Systems (GIS) date from the late 60s. A modern GIS can be used to capture, store, transform, analyse and visualise spatial or geographical data. Data maps are made by creating a different layers for different kind of data objects, such as towns, borders or rainfall.  Elements in the layers have a spatial and sometimes temporal coordinate and the layers are overlaid to form the data map.  GIS typically provide good spatial analysis tools and allow smooth transition between different levels of detail.

Spatial data is stored in a GIS system in two ways

* As _raster_ or pixel based data. Arial photos, satellite images, and elevation data are typically stored as raster data.
* Geographic shapes are typically stored as _vector_ data. Points are used to store location of zero-dimensional features like a mountain peak, lines or poly-lines to store the position of one-dimensional features like roads or rivers, and polygons to store the position and shape of two-dimensional features like lakes or countries.

## GIS tools & resources

* [Esri ArcGIS](https://www.esri.com/en-us/home) software is the industry standard in commercial GIS systems. It allows users to  combine a wide variety of data sources to create data maps, comes with its own cartographic data and can perform spatial analysis.
* [MapBox](https://www.mapbox.com), [CartoDB](https://carto.com), [MapInfo](https://www.pitneybowes.com/au/location-intelligence/geographic-information-systems.html), are other commercial GIS tools. The first two currently offer limited functionality for free.
* [QGIS](https://www.qgis.org/en/site/) is an open source GIS tool.
* Google provides Google Fusion Tables, Google Charts and APIs to Google Maps and Google Earth.
* [National Map](https://nationalmap.gov.au) is a great online GIS tool for quickly viewing Australian government data
* [Open Street Map](https://www.openstreetmap.org/#map=5/-28.153/133.275) (OSM) is a great online open source resource for maps.

## GIS data formats
Unfortunately a wide variety of different formats are used by GIS software to exchange spatial data. [JPEG2000](https://en.wikipedia.org/wiki/JPEG_2000) or [GeoTIFF](https://en.wikipedia.org/wiki/GeoTIFF) are often used for GIS raster data. Four common formats for GIS vector data exchange are

* [Keyhole Markup Language](https://en.wikipedia.org/wiki/Keyhole_Markup_Language) (KML) – XML based open standard that underlies Google Maps
* [Geography Markup Language](https://en.wikipedia.org/wiki/Geography_Markup_Language) (GML) – XML based open standard developed by the Open Geospatial Consortium that also includes raster data.
* [Esri shapefile](https://en.wikipedia.org/wiki/Shapefile) – widely used format developed by Esri
* [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON) – JSON format used by many open source GIS packages

There are tools to convert between these different formats. Vector data may also be specified using [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics) the W3C Scalable Vector Graphics standard.

***


