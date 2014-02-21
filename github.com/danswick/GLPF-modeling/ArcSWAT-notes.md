

Written with [StackEdit](https://stackedit.io/).

### Table of Contents

[TOC]

###Model Inputs

----------

Gathering model inputs and making sure they're in the correct format is the very first step to running ArcSWAT and should be done before begginning to load data into your project environment. The model requires very specific formats in order to run and projections must be consistent, making these steps crucial to the modeling process.

<i class="icon-info"></i> The [ArcSWAT I/O documentation](http://swat.tamu.edu/documentation/2012-io/), [FAQ](http://swat.tamu.edu/media/50893/arcswat_faq.pdf), and [Do's and Don't's](http://swat.tamu.edu/software/arcswat/recommendations/) can be found on the TAMU site. 

<i class="icon-info"></i> The [release notes](http://swat.tamu.edu/media/88297/ArcSWAT_Version201210_013_ReleaseNotes.pdf) also contain some weird idiosyncrasies that should be checked out beforehand. 

<i class="icon-info"></i> The [ArcSWAT Google Group](https://groups.google.com/forum/#!forum/arcswat) has tons of good tips.

<i class="icon-info"></i> The ArcSWAT user guide is great, but can only be found as a `.pdf` within the download from TAMU. It is recommended new users run through the demo data included. 

#### <i class="icon-layers"></i> Basemap Layers
The basemap is used primarily to give the map context and ensure accuracy of model outputs.

- Watershed boundaries define the project area
Filetype: `shapefile`
>    - Also consider buffering these to add margin of area
>    - HUC8 for MKE river watershed
>    - 2 HUC12's for west branch 

- Hydrology 
Filetype: `shapefile`
> This is obtained from the [WI state DNR](http://dnr.wi.gov/maps/gis/datahydro.html) 

- Farmer field data
Filetype: `shapefile` 
> This is owned and managed by SCF

#### <i class="icon-layers"></i> Input Layers
- Digital Elevation Model
Filetype: `ESRI GRID` 
> 3 and 10 meter DEM's are readily available. Delta attempting to integrate `LiDAR` from Fond Du Lac County.

- Land Cover
Filetype: `ESRI GRID, Shapefile or Feature Class` 
> Suggest using NLCD 2006 layer. May require some processing to get correct attributes and the like. 
>
> <i class="icon-cog"></i> Requirements for attribues:
> - Definition file 
> - Other

- Soils
Filetype: `ESRI GRID, Shapefile or Feature Class`
> **Gridded SSURGO** is easiest to find but will require export or possible `raster reformatting`.
> - <i class="icon-cog"></i> Raster definitions here

- Hydrology
> Hydrologic layers can be used to `burn in` the DEM in use. 

#### <i class="icon-download"></i> Non-Layer Inputs
- Weather Data
> A possible approach to weather data is to use the [**BASINS**](http://water.epa.gov/scitech/datait/models/basins/index.cfm) model to select a weather station, then download the full data using the built-in dialog. 

#### <i class="icon-pencil"></i> Dialog Parameters

###Steps 

----------

#### <i class="icon-check"></i> Project Setup
#### <i class="icon-check"></i> Watershed Definition 
#### <i class="icon-check"></i> HRU's and You
#### <i class="icon-check"></i> Weather
#### <i class="icon-check"></i> Running the Model
#### <i class="icon-upload"></i> Model Outputs
#### <i class="icon-help-circled"></i> ArcSWAT Idiosyncrasies 

 1. In project setup dialog, be sure the parameter database is set to `C:\SWAT\ArcSWAT\Databases\SWAT2012.mdb`
 2. DEM Setup
     3. Create a mask for target area, consider adding a buffer.
     4. DEM downloaded through BASINs has undefined datum, making reprojection very difficult.
 5. Area of 80 (~35 ha) acres in watershed delineator
     6. It appears you can only set watershed delineation cell size once per project. need new project to change
 7. NLCD2001 dataset from BASINS works
 8. Left off on soil
     9. What soil dataset is actually used in BASINS?
     10. What are other soil options

 

> Fontello icon set - http://benweet.github.io/stackedit/res/libs/fontello/demo.html 