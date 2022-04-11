# lakeCoSTR example datasets

This repository is meant to aide lakeCoSTR users in understanding the output from the lakeCoSTR tool. In this repository, we present a subset (2015-2020, at the 'loon' location) of continuous data from a research buoy located near the deepest location of Lake Sunapee, NH, USA (43.391°N, 72.058°W) (LSPA et al., 2021).


## Example Output Landsat Datasets

There are two Landsat datasets output from the lakeCoSTR tool: 

1) a *LAKENAME_temp_stats.csv* file and 

2) a folder called *histograms* where histograms of the temperature estimates for each Landsat scene are stored. 

The folder *lakeCoSTR_output* in this repository is a copy of what a user would find in their Google Drive, if they ran the lakeCoSTRv1.11.ipynb notebook found at the [lakeCoSTR_colab repository](https://github.com/lakeCoSTR/lakeCoSTR_colab), utilizing the *sunapee_insitu_example.csv* *in situ* temperature file to create a Landsat-*in situ* paired dataset. A copy of the executed notebook is available at the filepath: lakeCoSTR_output/sunapee_example/lakeCoSTRv1.11_example.ipynb within this repository.

### lakeCoSTR_output/sunapee_example/sunapee_example_temp_stats.csv

This is the *.csv* represents the summary data for every available Landsat 4-8 scene, given the user-defined lake area and time period of interest. In this case, we used the extent of Lake Sunapee, NH, USA and the time period of May-October 2015-2020. This output file from lakeCoSTR has the same format no matter the lake or time period extent.

| Column Header | Column definition | Units | Source of data | 
|   --- | --- | --- | --- |
|   system:index    |   Landsat scene identifier: *PROCESSINGLEVEL* _ *LANDSATCOLLECTION* _ *LANDSATDATATIER* _ *LANDSATMISSION* _ *PATHROW* _ *ACQUISITIONDATE* | textString | scene-level metadata |
|	availablePixels_count | total pixels available for analysis, after pixel-level bit mask and geometry masks applied | pixel | GSWD masked by bit QA and geometry of lake |
|	cloudcover_pct_scene | percent cloud cover of entire Landsat scene | percent | Landsat scene metadata |
|	datetime_landsat | datetime stamp of image acquisition in Landsat datetime format | integer; milliseconds since epoch | Landsat scene metadata |
|	esd_au_scene | earth-sun distance | astronomical units | Landsat scene metadata |
|	lakeCoverage_pct | percent of coverage of the lake in a given scene, calculated as (availablePixels_count/total number of GSWD pixels) * 100 | percent | GSWD masked by bit QA and geometry of lake |
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
|   .geo |  artifact of GEE extract |   none |  GEE |


### lakeCoSTR_output/sunapee_example/histograms folder

This folder contains the exported .png files of the histograms of the pixel-level temperature estimates. 

The file names are formatted as the following:

*MISSION* _ *PROCESSINGLEVEL* _ *PATHROW* _ *ACQUISITIONDATE* _ *PROCESSINGDATE* _ *LANDSATCOLLECTION* _ *LANDSATTIER* _histo.png

An example is:
*LC08* _ *L1TP* _ *013030* _ *20150702* _ *20200909* _ *02* _ *T1* _histo.png

This would be the histogram for the *Landsat 8* mission, *Level 1* processing, path *013* row *030*, acquired ong *2015-07-02*, processed on *2020-09-09*, *Collection 2*, *Tier 1*.

An example of a histogram that is likely showing cloud contamination is LC08_L1TP_013030_20160805_20200906_02_T1_histo.png:

   ![LC08_L1TP_013030_20160805_20200906_02_T1_histo](https://raw.githubusercontent.com/lakeCoSTR/lakeCoSTR_examples/main/lakeCoSTR_output/sunapee_example/histograms/LC08_L1TP_013030_20160805_20200906_02_T1_histo.png)

    This bimodal distribution likely indicates a contaminated scene and likely should not be included in any further analysis.

We have found that using a kurtosis filter to remove scenes like that seen above has been the most useful in removing contaminated scenes. For the example lake here, we used a kurtosis value of < 2 as the cutoff for acceptable scenes.

## Example *in situ* Input File

We have provided an example *in situ* dataset for Lake Sunapee (sunapee_insitu_example.csv). Note that you can have more columns than the required 'datetime', 'location', 'depth_m', and 'temp_degC'. See the [User Guide](https://github.com/lakeCoSTR/lakeCoSTR_colab/blob/main/UserGuide_lakeCoSTR_colab.md) for formatting rules.


## Example Paired Dataset Output

If a user provides an *in situ* temperature dataset, lakeCoSTR will create a *.csv* of paired Landsat-*in situ* data for ground-truthing the remote sensing temperature estimates, as well as ancillary files that list the *in situ* records that matched with Landsat scenes. 

### lakecoSTR_output/sunapee_example/sunapee_example_temp_landsat_paired.csv

This is the *.csv* that is the result of using the Landsat-*in situ* pairing process in lakeCoSTR. Here, the primary output file(sunapee_example_temp_stats.csv) is filtered and matched with user-provided *in situ* data file (sunapee_insitu_example.csv). The paired dataset copies the columns from the lake_sunapee_temp_stats.csv. Because this example file only contains data from one location, there is only one set of median, mean, standard deviation and count columns.

| Column Header | Column definition | Units | Source of data | 
|   --- | --- | --- | --- |
|   landsat_time_utc    | datetime of the scene acquistion in UTC time |    YYYY-MM-DD HH:MM:SS |  Landsat scene metadata |
|	scene | Landsat scene identifier: *MISSION* _ *PROCESSINGLEVEL* _ *PATHROW* _ *ACQUISITIONDATE* _ *PROCESSINGDATE* _ *LANDSATCOLLECTION* _ *LANDSATTIER* | textString | Landsat scene metadata |
|	is_temp_avg | average *in situ* temperature measured in user-defined time window, across all locations | degreeCelsius | user-provided *in situ* data file |
|	is_temp_stdev | standard deviation of the mean for *in situ* temperature measured in user-defined time window, across all locations | degreeCelsius | user-provided *in situ* data file |
|	is_depth_avg | average depth of *in situ* values in user-defined time window, across all locations | meter | user-provided *in situ* data file |
|	is_depth_stdev | standard deviation of the mean for the depth of *in situ* values in user-defined time window, across all locations | meter | user-provided *in situ* data file |
|	is_temp_med | median *in situ* temperature measured in user-defined time window, across all locations | degreeCelsius | user-provided *in situ* data file |
|	insitu_count | total number of *in situ* measurements contributing to the aggregated values | count | user-provided *in situ* data file |
|	loon_median | median *in situ* temperature measured in user-defined time window, at 'loon' | degreeCelsius | user-provided *in situ* data file |
|	loon_mean | average *in situ* temperature measured in user-defined time window, at 'loon' | degreeCelsius | user-provided *in situ* data file |
|	loon_std | standard deviation of the mean *in situ* temperature measured in user-defined time window, at 'loon' | degreeCelsius | user-provided *in situ* data file |
|	loon_count| total number of *in situ* measurements contributing to the aggregated values at 'loon' | count | user-provided *in situ* data file |


### ancillary folder

This folder contains individual *.csv* files for each scene, listing the individual temperature measurements included in the aggregated data found in the sunapee_example_temp_landsat_paired.csv file. File names are labeled with the 'scene' value from the sunapee_example_temp_landsat_paired.csv file. We encourage users to check this file to make sure that they have selected the correct UTC offset in the lakeCoSTR tool. This file copies all columns from the user-provided *in situ* data file and then adds the following additional columns:

| Column Header | Column definition | Units | Source of data | 
|   --- | --- | --- | --- |
|	datetime_utc | datetime, converted to UTC time based on the user-defined timezone (in this case 'Etc/GMT+5') | YYYY-MM-DD HH:MM | user-provided *in situ* data file |
|	dt_delta |  difference between datetime_utc (*in situ* measurement) and Landsat acquisition time (landsat_time_utc in sunapee_example_temp_landsat_paired.csv file) | DAYS HH:MM:SS | lakeCoSTR calculation |
|	delta_secs | difference between datetime_utc (*in situ* measurement) and Landsat acquisition time (landsat_time_utc in sunapee_example_temp_landsat_paired.csv file) in seconds | second | lakeCoSTR calculation |



## Data Citation

The data used in this example are from the following data package:

LSPA, K.C. Weathers, and B.G. Steele. 2021. Lake Sunapee Instrumented Buoy: High Frequency Water Temperature and Dissolved Oxygen Data - 2007-2020 ver 2. Environmental Data Initiative. https://doi.org/10.6073/pasta/0c5298c55a128be56ba57449c795df63 (Accessed 2022-04-07).
