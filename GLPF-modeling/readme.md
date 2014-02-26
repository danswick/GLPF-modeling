

Written with [StackEdit](https://stackedit.io/).

### Table of Contents

[TOC]

### <i class="icon-check"></i> Project Setup
----------
The default folder, `C:\SWAT\ArcSWAT\`, is recommended.

Make sure that the installation folder is writeable to all. This is required, as some of the SWAT databases installed in this folder will be accessed for editing by the ArcSWAT interface.


###Model Inputs

----------

Gathering model inputs and making sure they're in the correct format is the very first step to running ArcSWAT and should be done before begginning to load data into your project environment. The model requires very specific formats in order to run and projections must be consistent, making these steps crucial to the modeling process.

<i class="icon-info"></i> The [ArcSWAT I/O documentation](http://swat.tamu.edu/documentation/2012-io/), [FAQ](http://swat.tamu.edu/media/50893/arcswat_faq.pdf), and [Do's and Don't's](http://swat.tamu.edu/software/arcswat/recommendations/) can be found on the TAMU site. 

<i class="icon-info"></i> The [release notes](http://swat.tamu.edu/media/88297/ArcSWAT_Version201210_013_ReleaseNotes.pdf) also contain some weird idiosyncrasies that should be checked out beforehand. 

<i class="icon-info"></i> The [ArcSWAT Google Group](https://groups.google.com/forum/#!forum/arcswat) has tons of good tips.

<i class="icon-info"></i> The ArcSWAT user guide is great, but can only be found as a `.pdf` within the download from TAMU. The default path is [`C:\SWAT\ArcSWAT\ArcSWATHelp\ArcSWAT_Documentation_2012.pdf`](C:\SWAT\ArcSWAT\ArcSWATHelp\ArcSWAT_Documentation_2012.pdf) It is recommended new users run through the demo data included. 

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
**Digital Elevation Model**
Filetype: `ESRI GRID` 

>*2012 User Guide*
>The interface allows the DEM to use integer or real numbers for elevation values. The units used to define the GRID resolution and the elevation are not required to be identical. For example, the GRID resolution may be in meters while the elevation may be in feet.

>The GRID resolution must be defined in one of the following units: meters, kilometers, feet, yards, miles, decimal degrees. The elevation must be defined in one of the following units: meters, centimeters, yards, feet, inches

* 3 and 10 meter DEM's are readily available. Delta attempting to integrate `LiDAR` from Fond Du Lac County. 3m DEM's are spotty across the US, while 10m is more widely available but may be older. 
* EPA BASINs has an automated downloader for DEM data, pre-clipped to HUC8 and already in ESRI GRID format. 
* <!--- BASINS has undefined datum and breaks spatial reference compatibility --->

**Land Cover**
Filetype: `ESRI GRID, Shapefile or Feature Class` 

>*2012 User Guide* 
>The categories specified in the land cover/land use map will need to be reclassified into SWAT land cover/plant types. The user has three options for reclassifying the categories. The first option is to use a land cover/land use lookup table that is built into the ArcSWAT interface. The interface contains the USGS LULC and NLCD lookup tables in the SWAT2012.mdb database that identifies the different SWAT land cover/plant types used to model the various USGS LULC or NLCD land uses. The second option is to type in the 4-letter SWAT land cover/plant type code for each category when the land cover/land use map theme is loaded in the interface. The third option is to create a user look up table that identifies the 4-letter SWAT code for the different categories of land cover/land use on the map. The format of the look up table is described in Section 3.3.

* Suggest using NLCD 2006 layer. May require some processing to get correct attributes and the like.
* When clipping national NLCD layer, you may encounter an error building an attribute table. [This solution](http://forums.arcgis.com/threads/53555-Build-raster-attribute-table?p=334190), exporting to another copy of the file, did the trick. 
* The landcover layer must be in the same spatial reference as the project. 

    <i class="icon-cog"></i> Requirements for attribues:
    * Definition file 
    * Other

**Soils**
Filetype: `ESRI GRID, Shapefile or Feature Class`

>*2012 User Guide*
>The categories specified in the soil map will need to be linked to the soil database (U.S. soils data only) included with the interface or to the User Soils database, a custom soil database designed to hold data for soils not included with the U.S. soil database. The user has four options for linking the map to the U.S. soil database. One method is to use the STATSGO polygon (MUID) number. Because the soils
database contains information for the entire U.S., the 3-digit state STATSGO number must be prefixed with the 2-digit numeric code for the state. (The 2-digit numeric codes are listed in Appendix 2.) For every polygon, the soil database contains data for all soil phases found within the polygon. When the "Stmuid" option is chosen, data for the dominant soil phase in the polygon is used for the map category. The "Stmuid + Seqn" option allows the user to specify the MUID number and the soil sequence number. This allows the user to choose a soil other than the dominant within the MUID. For example, if Seqn is set to 3, data for the third most common soil phase will be used to represent the map unit. The "Name + "Stmuid" option allows the user to specify a soil series within the STATSGO polygon by name. The interface will use data for the dominant phase of the soil series to represent the map category.

>The user may also link the soils map to the database via Soils5ID number. When the "S5id" option is chosen, data for the specified soil series is used to represent the map unit. In order to use the "S5id" option, the soil database for the entire US must be installed. The final option, "Name", is chosen when soils data from the User Soils database are to be utilized. The user will import SWAT soil files (.sol) or type the soil data into the User Soils database for each of the map categories prior to creating the project. The "Name" specified for each of the map categories is the name of the soil in the User
soils database. 

>To reclassify the map categories, the information may be manually entered within the interface. Alternatively, a look up table may be loaded which has this information listed. Section 3.3 summarizes the format of the look up table used to specify the soils information.

* **Gridded SSURGO** is easiest to find but will require export or possible `raster reformatting`.
<i class="icon-cog"></i> Raster definitions here

**Hydrology/Streams** (Optional)
Filetype: `Shapefile or Featureclass`

>*2012 User Guide*
>The interface allows a polyline shapefile or feature class with the stream delineation to be superimposed on the DEM. The stream delineation dataset is needed for areas where the relief is so low the DEM grid is unable to accurately delineate the location of the streams.

* Hydrologic layers can be used to `burn in` the DEM in use. 

**DEM Mask** (Optional)
Filetype: `ESRI GRID, Shapefile, Feature Class Format`

>*2012 User Guide*
>The interface allows a mask to be superimposed on the DEM. The interface differentiates the mask grid into areas classified as category 0 (no data) and areas classified as any category > 0. Areas of the DEM grid for which the Mask grid has a value of 0 will not be processed for stream delineation.

* Guide is incorrect. Filetype must be raster.

**User-Defined Watersheds and Streams** (Optional)
TBD



#### <i class="icon-download"></i> Non-Layer Inputs
- Weather Data
> A possible approach to weather data is to use the [**BASINS**](http://water.epa.gov/scitech/datait/models/basins/index.cfm) model to select a weather station, then download the full data using the built-in dialog. 

#### <i class="icon-pencil"></i> Dialog Parameters

###Steps 

----------


#### <i class="icon-check"></i> Watershed Delineation
1. Flow direciton and accumulation. In ArcSWAT, this step can take an extremely long time to process. It builds out a set of rasters, which unfortunately can't be referenced if the session is restarted. This means you should have all of your parameters gathered ahead of time so you can complete the Automatic Watershed Delineation process in one shot. FDA files: 
> * Results stored under `~/[project_folder]/Watershed/Grid/`
* Includes `sourcedem`, `targetdem`, `filedem`, `flowacc`, `flowdir`



#### <i class="icon-check"></i> HRU's and You
#### <i class="icon-check"></i> Weather
#### <i class="icon-check"></i> Running the Model
#### <i class="icon-upload"></i> Model Outputs
#### <i class="icon-help-circled"></i> ArcSWAT Idiosyncrasies 

 1. In project setup dialog, be sure the parameter database is set to `C:\SWAT\ArcSWAT\Databases\SWAT2012.mdb`
 2. Be sure to set up ArcSWAT extensions in ArcGIS extensions dialog before attempting to use automatic delineator. 
 3. Running ArcMap as administrator may be helpful with permissions issues. 
 2. DEM Setup
     3. Create a mask for target area, consider adding a buffer.
     4. DEM downloaded through BASINs has undefined datum, making reprojection very difficult.
     5. Rasterstore database is in access, so it has a limit of 2GB.
 5. Area of 80 (~35 ha) acres in watershed delineator
     6. It appears you can only set watershed delineation cell size once per project. need new project to change
 7. NLCD2001 dataset from BASINS works
 8. Left off on soil
     9. What soil dataset is actually used in BASINS?
     10. What are other soil options

 

> Fontello icon set - http://benweet.github.io/stackedit/res/libs/fontello/demo.html 