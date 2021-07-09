# Geospatial Mapping Pipeline
A fully automated geospatial pipeline for ecologists.

## Citing this work
When using (part of) this modeling workflow, please cite Van den Hoogen et al., BioRxiv (2021). A geospatial mapping pipeline for ecologists, doi: 10.1101/2021.07.07.451145

## How to get started
1. Sign up for a GEE account on https://signup.earthengine.google.com
2. Install Python 3 on your local machine (e.g. using Anaconda)
3. Install the GEE Python API using pip or conda. See details on https://developers.google.com/earth-engine/guides/python_install
4. Authenticate the GEE Python API
5. Install the following packages: `pandas`, `numpy`, `subprocess`, `time`, `datetime`, `scipy`, `sklearn`, `itertools`, `pathlib`, `math`, `matplotlib` using your package manager
6. Recommended (when access to Google Cloud Storage is available): install `gsutil`

## Running the pipeline
The GMP is available as a executable python script, and can be run in the command line.

1. Create a folder on your local machine, to hold your project data
2. Place your data, as a csv file into this folder. This file should contain a column holding the response variable (of course...), and latitude+longitude. Default CRS: WGS84 EPSG:4326. At the moment, the pipeline assumes a continuous response variable, and will train a regression RF model.
3. Place the script into this folder and configure your project-specific details in the top part of the script. Make sure to direct the bash functions (lines 54-55) to the correct path where `ee` and `gsutil` are installed on your local machine
5. Execute the script

## Some notes in case Google Cloud Storage is not available
To automate the upload process, we routinely use GCS but as it's a paid service this might not be available to everyone. In case you want to bypass these steps, it's probably the easiest to manually upload the generated csv files (i.e., the training data file and the bootstrap samples) using the GEE web browser UI. You'll need to remove some parts of the script where `gsutil` is called. Just run the script until it complains that one of the assets can't be found, manually upload the file (make sure to give the GEE FeatureCollection the correct name and path) and re-run the script. You'll have to repeat this process a number of times; for the upload of the raw data and for the upload of the bootstrap subsamples. 

## Disclaimer
This script is still work in progress. If you spot any mistakes please let us know! We're also continously improving the workflow and developing new 'modules'. Watch this space for updates. 

We are aware that there are some steps that not necessarily follow GEE 'best practices'. Usually this is the result of a trade-off between computation time and flexibility. 
