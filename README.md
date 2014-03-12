

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
1. **DEM Setup**
    - **Mask.** ArcSWAT requires a raster for the mask, despite the guidance. You can also manually delineate the boundary of the mask (which is weird, because the manual delineation isn't a raster). 
    - **Burn In.** ArcSWAT turns flowlines into a raster dataset, which "burns in" the DEM to ensure it captures accurate flowlines. We used the `NHD flowline` file for burn-in. Immediate results appear to be random static at default scale, but zooming in reveals the full dataset. 
2. **Stream Definition**
    - **DEM-based vs Pre-Defined.**
    - **Flow direciton and accumulation.** In ArcSWAT, this step can take an extremely long time to process. It builds out a set of rasters, which unfortunately can't be referenced if the session is restarted. This means you should have all of your parameters gathered ahead of time so you can complete the Automatic Watershed Delineation process in one shot. 
    - **Area.** Area of 80 (~35 ha) acres in watershed delineator
        - It appears you can only set watershed delineation cell size         once per project. need new project to change
    
    ArcSWAT *also* doesn't seem able rebuilt FDA after it has already been   done, preventing the next steps in the Watershed Delineation wizard. FDA files: 
> * Results stored under `~/[project_folder]/Watershed/Grid/`
>   * Includes `sourcedem`, `targetdem`, `filedem`, `flowacc`, `flowdir`
3. **Outlet and Inlet Definition.** 
    - **Subbasin outlet, inlet of draining watershed, point source input...**
    - **Add points source to each subbasin**
        - **Edit manually** 
4. **Watershed outlets selection and definition**
    - Whole watershed outlets 
    - Delineate watershed 
5. **Calculation of subbasin parameters.**

 
#### <i class="icon-check"></i> Land Use/Soils/Slope Definition
**Land Use Data**
Land use data must be projected and must have the same spatial reference as the other layers in the project. Ensure SRS is the same before attempting this step with NLCD data (or whatever is being used). 

>For this project, I clipped the national NLCD dataset to the extent of our HUC8, then changed the SRS to NAD83, UTM Zone 16N (meters). 

Once you've pointed SWAT to the Land Use `grid` file, SWAT will rebuild it into the project database and create a new file called "LandUse1." Choose `VALUE` under the "Choose Grid Field" drop-down and click "OK." Click the "LookUp Table button and choose `NLCD 2001/2006 Table" and click "OK." This should populate the "LandUseSwat" column with class values. Once this has been done, click the "Reclassify" button. This will generate yet another grid file in your project database. In the case of this project, the resulting layer was named "SwatLandUseClass(LandUse2)."

**Soil Data**
*Attempt with SSURGO*
Trying to load gridded SSRUGO straight from the geodatabase resulted in the error:
>You have to choose datasets of the same type

Download ARCSWAT SSURGO database: 


*Attempt with STATSGO rather than SSURGO*
Counties for HUC8: Fond Du Lac, Sheboygan, Ozaukee, Washington, Dodge, Waukesha, Milwaukee. 
Downloaded from geospatial data gateway for above counties. 
1. Load STATSGO data (have to select all filters from "show of type" dropdown)
2. Once loaded, select MUID radio button
3. Choose "arcswat statsgo" radio button from "Soil database options"
4. Choose "stmuid"
5. Click "lookup table" and navigate to the ArcSWAT soils database in the ArcSWAT program folder
6. Invalid table dimensions
7. .NET implosion 
    > When loading the STATGSO layer, I get:
    > - Error Call Stack Sequence:
            createcoutputfilesdbate LUGridShp.vb Line: 3364
    > - Error Number: 5
    > - Description: Value does not fall within the expected range
    >
    > If I click through the errors and select "value" under "choose grid field," I get the error "Argument 'Expression' is not a valid value/ 

*Attempt with build-in ArcSWAT soils*
1. Soils layer needs to be reprojected (see link under soil resources below)
2. Built-in layer looks like it's missing WI, but this is just a rendering artifact. 
3. Once soils have been reprojected and saved with the original file name within the ArcSWAT_US_soils database, they can easily be loaded into the wizard. HOORAY! 

*Soil Resources*
>- [SSURGO class relationships](https://groups.google.com/forum/#!topic/ArcSWAT/ys6I3o4TgSQ)
>- [STATSGO vs SSURGO, troubleshooting](https://groups.google.com/forum/#!searchin/ArcSWAT/SSURGO/arcswat/pIry3MoEJKs/F6hFPGy9BgoJ)
>- [Integration of SSURGO maps and soil parameters within a geographic information system and non point source pollution model system](http://naldc.nal.usda.gov/download/15136/PDF)
>- [Better accuracy, higher computational load using SSURGO](https://groups.google.com/forum/#!searchin/ArcSWAT/SSURGO/arcswat/uTk1crGUSo0/vM0KdS5gfiEJ)
>- [This solution would be neat if the ArcSWAT soils DB raster included Wisconsin. But it doesn't](https://groups.google.com/forum/#!searchin/ArcSWAT/statsgo/arcswat/33PJXzjwqNE/Tai6uanl-KYJ)   

#### <i class="icon-check"></i> Slope
1. in the dialog box, look at watershed slope stats. Unsure of the best approach to defining classes, but I just went with 2 classes, 0-the mean and >mean. 

#### <i class="icon-check"></i> HRU's and You
- Under "HRU Definition," select "multiple HRU's" 
- Threshold should be %
- We need to develop a better methodology for setting thresholds. I just went with the BASINS guidance of:
    - Land use: 15%
    - Soil class: 10%
    - Slope class: 10% 
- Check "write HRU Report"
- Land Use Revinement tab
    - We did not get into this area
    
>*Resources* 
- [TetraTech Configuration, Calibration and Validation Report](http://www.epa.gov/region1/eco/tmdl/pdfs/vt/SWATModelConfigurationCalibrationValidation.pdf)



#### <i class="icon-check"></i> Weather
The inputs for weather can either be loaded from the SWAT2012 database or user-defined. For the purposes of expedience, the defaul option of `WGEN_US_COOP_1980_2010` was chosen under the "Weather Generator Data" tab. The other five tabs, which are optional, were left as default.  
> It is important to note that the default weather tables only represent data through 2010. 

When the default is selected, clicking "OK" will prompt ArcSWAT to calculate distance to weather stations. When this completes, a prompt will appear. Click "OK," then, somehwat confusingling, close out of the weather dialog. The option to write SWAT input tables should now be available.

**Using user-defined weather data**
This section will be completed should early model results suggest that the default data does not provide great enough precision. 

#### <i class="icon-check"></i> Running the Model
**Write SWAT Input Tables**
Once all of the above steps have been completed, the option to write SWAT input tables will be available. 

1. When the dialog is opened, a list of tables is available. There are some circumstances that might require writing tables one at a time, but most users should click the `Select All` button, then click the `Create Tables` button.  
    - This will run table-writing scripts for all of the tables. 
    - The first prompt will ask to use weather database to calculate heat units to (plant) maturity. This is only valid in the northern hemisphere. Most should click `Yes`. 
    - When the fig.fig file is written, you are asked, in sequence, if you would like to re-write 'pp' (point source), 'ppi' (inlet), and 'res' (reservoir). Users who have loaded in point source, inlet or reservoir data during Watershed Delineation should **not** click `Yes`. Otherwise, users can click `No`. 

>Error occured while writing .sol, but accidentally clicked away before being able to copy it down. The "do you want to re-write pp, pip, res prompt never appeared. The only text I can remember is "no error code available" and that it was a .NET error. Canceled the operation and re-opened ArcMap, but the option to write input tables had been grayed out. Rebooted and the option to write input tables was available and, upon re-starting the process, I got the prompt to re-write pp, pip and res. Seems to be yet another .NET problem only solvable via reboot. 


**Setup and Run SWAT Model Simulation**
This section describes the actual running of the model. The inputs are described below. 

- Period of simulation 
    - The default runs from 1901 to 2100. I set it to do a 30-year run (1/1/1990 - 1/1/2020)
- Rainfall sub-daily timestep 
    - This option was not available 
- Rainfall distribution 
    - Default of "skewed normal." See I/O documentation 
- SWAT.exe version
    - Allows to choose 32- or 64-bit versions, debug or release. Debug versions have more verbose error reporting and release runs considerably faster. 
- Printout settings 
    - Lets the user choose which parameters are printed into the results and the frequency (daily, monthly, yearly)
    - Chose Monthly and soil nutrient, water quality output, route headwaters, print snow, print soil storage and limit HRU output (default)
- Set CPU Affinity

Click `setup SWAT Run` to write your parameters, then click `Run SWAT`. 
>- With above parameters, got a `error (72): floating overflow` upon processing year 2. 
>- Changed timeframe from 1/1/2000 - 1/1/2015: same error.
>- Changed to 64-bit release - same error
>- Removed route headwaters - same error
>- Tried with just "soil nutrient" checked - same error
>- As per [this help article](https://groups.google.com/forum/#!topic/arcswat/mbuOOhVKG2s) changed `channel routing` to "Muskingum." - Same error. 
>- Checked SNO50COV value as in [this thread](https://groups.google.com/forum/#!msg/swat-cup/jsr2KGhVSW4/G4xhQRHqlPkJ). Was within bounds.
>- As in above article, uninstalled ArcSWAT and installed latetst version. Run with parameters above successful! 

**Run SWATCheck** 
Running the built-in SWAT Check application is used to check for errors and, to some extent, visualize the outputs from the model run. 

> First attempt at running swat check resulted in a system out of memory error. 



    
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

 
> Gist available here - https://stackedit.io/viewer#!provider=gist&gistId=2e7e04eb153a78d0ab37&filename=SWAT_model_notes 

> Fontello icon set - http://benweet.github.io/stackedit/res/libs/fontello/demo.html 