# lakeCoSTR example datasets

This repository is meant to aide lakeCoSTR users in understanding the output from the lakeCoSTR tool. In this repository, we present a subset (2015-2020, at the 'loon' location) of continuous data from a research buoy located near the deepest location of Lake Sunapee, NH, USA (43.391°N, 72.058°W) (LSPA et al., 2021).


## Example Output Landsat Datasets

There are two Landsat datasets output from the lakeCoSTR tool: 1) a *LAKENAME_temp_stats.csv* file and 2) a folder called *histograms* where histograms of the temperature estimates for each Landsat scene are stored. The folder *lakeCoSTR_output* in this repository is a copy of what a user would find in their Google Drive, if they ran the lakeCoSTRv1.11.ipynb notebook found at the [lakeCoSTR_colab repository](https://github.com/lakeCoSTR/lakeCoSTR_colab), utilizing the *sunapee_insitu_example.csv* *in situ* temperature file to create a Landsat-*in situ* paired dataset. A copy of the executed notebook is available at the filepath: lakeCoSTR_output/sunapee_example/lakeCoSTRv1.11_example.ipynb within this repository.

### lakeCoSTR_output/sunapee_example/sunapee_example_temp_stats.csv

This is the *.csv* represents the summary data for every available Landsat 4-8 scene, given the user-defined lake area and time period of interest. In this case, we used the extent of Lake Sunapee, NH, USA and the time period of May-October 2015-2020. This output file from lakeCoSTR has the same format no matter the lake or time period extent.

Column headers, definitions, and units

| Column Header | Column definition | Units | Source of data | 
|   --- | --- | --- | --- |
|   system:index    |   Landsat scene identifier: LEVEL_COLLECTION_TIER_MISSION_PATHROW_DATE | textString | scene-level metadata |
|	availablePixels_count | total pixels available for analysis, after pixel-level bit mask and geometry masks applied | pixel | GSWD masked by bit QA and geometry of lake |
|	cloudcover_pct_scene | percent cloud cover of entire Landsat scene | percent | Landsat scene metadata |
|	datetime_landsat | datetime stamp of image acquisition | YYYY-MM-DD HH:MM | Landsat scene metadata |
|	esd_au_scene | earth-sun distance | astronomical units | Landsat scene metadata |
|	lakeCoverage_pct | percent of coverage of the lake in a given scene, calculated as (availablePixels_count/total number of GSWD pixels) * 100 | GSWD masked by bit QA and geometry of lake |
|	sunazi_deg_scene | sun azimuth angle | degree | Landsat scene metadata |
|	sunelev_deg_scene | sun elevation | degree | Landsat scene metadata |
|	surface_temp_kurtosis | measure of tailedness of histogram for temperature estimates of the lake for a given scene | none | pixel-level analysis |
|	surface_temp_max | maximum temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_mean |  mean temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_median |  median temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_min |  minimum temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_p25 |  25th percentile temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_p75 |  75th percentile temperature for a given scene | degreeCelsius | pixel-level analysis | 
|	surface_temp_skew | skew of the histogram for temperature estimates of the lake for a given scene | none | pixel-level analysis |
|	surface_temp_stdDev | standard deviation from the mean for the temeperature estimates of the lake for a given scene | degreeCelsius | pixel-level analysis |


### lakeCoSTR_output/sunapee_example/histograms folder


## Example Paired Dataset Output

If a user provides an *in situ* temperature dataset, lakeCoSTR will create a *.csv* of paired Landsat-*in situ* data for ground-truthing the remote sensing temperature estimates, as well as ancillary files that list the *in situ* records that matched with Landsat scenes. 

### lakecoSTR_output/sunapee_example/sunapee_example_temp_landsat_paired.csv


### ancillary folder


## Example *in situ* Input File


## Data Citation

The data used in this example are from the following data package:

LSPA, K.C. Weathers, and B.G. Steele. 2021. Lake Sunapee Instrumented Buoy: High Frequency Water Temperature and Dissolved Oxygen Data - 2007-2020 ver 2. Environmental Data Initiative. https://doi.org/10.6073/pasta/0c5298c55a128be56ba57449c795df63 (Accessed 2022-04-07).
