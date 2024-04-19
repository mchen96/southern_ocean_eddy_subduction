# Southern Ocean Eddy Subduction
Code used in Chen and Schofield (2024): "Spatial and Seasonal Controls on Eddy Subduction in the Southern Ocean"

## Contents
#### Notebooks
1. detection.ipynb
2. figures.ipynb
#### Notebook outputs
1. outputs
    a. ESP\_anomalies.pkl
    b. profile\_summaries.pkl
    c. ts\_allprofiles.pkl
2. figures
    a. Figures 1-4
    b. Figures S1-S5
    c. Example FSLE field used in Figure 1
#### Dependencies and data
1. environment.yml
2. orsi\_park-durand\_so\_fronts\_.nc

## Description and usage
### Additional requirements
Before running any of the notebooks here, download the SOCCOM BGC-Argo float data from https://library.ucsd.edu/dc/collection/bb0488375t
Download the  2023-08-28 Data snapshot. Format: LIAR carbon algorithm, netCDF, low resolution 
This download should be stored in the root directory in a folder named "SOCCOM_GO-BGC_LoResQC_LIAR_28Aug2023_netcdf"

### detection.ipynb
- This notebook contains the primary analyses of the raw float data, generating derived data products stored in outputs/
- 

