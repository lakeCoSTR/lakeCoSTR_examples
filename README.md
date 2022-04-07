# lakeCoSTR example datasets

This repository is meant to aide lakeCoSTR users in understanding the output from the lakeCoSTR tool. In this repository, we present a subset (2015-2020, at the 'loon' location) of continuous data from a research buoy located near the deepest location of Lake Sunapee, NH, USA () (LSPA et al., 2021).


## Example Output Landsat Datasets

There are two Landsat datasets output from the lakeCoSTR tool: 1) a *_temp_stats.csv* file and 2) a folder with histograms of the temperature data for each Landsat scene. The folder *'lakeCoSTR_output'* in this repository is a copy of what a user would find in their Google Drive, if they ran the lakeCoSTRv1.11.ipynb notebook found at the [lakeCoSTR_colab repository](https://github.com/lakeCoSTR/lakeCoSTR_colab), utilizing the *sunapee_insitu_example.csv* *in situ* temperature file to create a Landsat-*in situ* paired dataset. A copy of the executed notebook is available at the filepath: lakeCoSTR_output/sunapee_example/lakeCoSTRv1.11_example.ipynb within this repository.

### lakeCoSTR_output/sunapee_example/sunapee_example_temp_stats.csv


### lakeCoSTR_output/sunapee_example/histograms folder


## Example Paired Dataset Output

If a user provides an *in situ* temperature dataset, lakeCoSTR will create a *.csv* of paired Landsat-*in situ* data for ground-truthing the remote sensing temperature estimates, as well as ancillary files that list the *in situ* records that matched with Landsat scenes. 

### lakecoSTR_output/sunapee_example/sunapee_example_temp_landsat_paired.csv


### ancillary folder


## Example *in situ* Input File


## Data Citation

The data used in this example are from the following data package:

LSPA, K.C. Weathers, and B.G. Steele. 2021. Lake Sunapee Instrumented Buoy: High Frequency Water Temperature and Dissolved Oxygen Data - 2007-2020 ver 2. Environmental Data Initiative. https://doi.org/10.6073/pasta/0c5298c55a128be56ba57449c795df63 (Accessed 2022-04-07).
