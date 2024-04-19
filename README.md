# Southern Ocean Eddy Subduction
Code used in Chen and Schofield (2024): "Spatial and Seasonal Controls on Eddy Subduction in the Southern Ocean"

## Contents
#### Notebooks
1. detection.ipynb
2. figures.ipynb
#### Notebook outputs
1. outputs <br>
  a. ESP\_anomalies.pkl <br>
  b. profile\_summaries.pkl <br>
  c. ts\_allprofiles.pkl <br>
2. figures 
  a. Figures 1-4 <br>
  b. Figures S1-S5 <br>
  c. Example FSLE field used in Figure 1 <br>
#### Dependencies and data
1. environment.yml
2. orsi\_park-durand\_so\_fronts\_.nc

## Description and usage
### Additional requirements
- Before running any of the notebooks here, download the SOCCOM BGC-Argo float data from https://library.ucsd.edu/dc/collection/bb0488375t 
- Download the  2023-08-28 Data snapshot. Format: LIAR carbon algorithm, netCDF, low resolution 
- This download should be stored in the root directory in a folder named "SOCCOM_GO-BGC_LoResQC_LIAR_28Aug2023_netcdf" 

### detection.ipynb
- This notebook contains the primary analyses of the raw float data, generating derived data products stored in outputs/

- Derived variables include physical variables calculated using the Gibbs Seawater package (GSW)

- For each float profile, it computes summary statistics, such as mixed layer depth, maximum buoyancy frequency, as well as scalar summaries of biogeochemical variables in that profile, such as integrated and depth-averaged quantities (ex: POC) within the mixed layer and beneath the mixed layer. 
    - These summary statistics for each profile are stored in a pandas dataframe: profile\_summaries.pkl
    - Additional analyses conducted on each profile and stored in this dataframe include:
        - Spike analyses to detect the frequency of large particles sinking beneath the mixed layer. This is summarized in the dataframe for Navis floats only, which provide high-enough vertical resolution to conduct this analysis
        - FSLE matchups: described further below. The mean and the strongest (most negative, or "minimum") altimetry-derived FSLEs within a 1°x1° area of the float profile
        
- It stores all observed T/S quantities (for every observation in every float profile) in a pandas dataframe: ts\_allprofiles.pkl
    - This is used to generate TS diagrams later
    
- This notebook contains the algorithm to detect eddy subduction anomalies in float profiles. Methods are described in Chen and Schofield (2024). Briefly, it identifies co-occuring anomalies in spice and apparent oxygen utilization (AOU) beneath the mixed layer.
    - These anomalies, representing 4.4% of profiles, are stored in a pandas dataframe: ESP\_anomalies.pkl
    - This dataframe contains summary statistics for each subsurface eddy subduction pump (ESP) anomaly; including integrated quantities within the vertical extent of the anomaly, both total integrated quantities and with ambient integrated quantities subtracted (leaving only the integrated quantity attributable to subduction)
    
- Additionally, the notebook runs an API through AVISO+ to download satellite altimetry-derived Finite-sive Lyapunov Exponent (FSLE) data
    - It downloads a satellite matchup to each float profile, downloading a same-day FSLE field within a 1°x1° area
    - This portion of the code takes about a day to run, as it submits individual queries for each float profile (~9000)
    - It will store downloaded FSLE data (NetCDF) in a subdirectory: fsles/
    - This downloaded data is then summarized and appended to the profile\_summaries.pkl dataframe, providing an FSLE summary for each float profile
    
### figures.ipynb
- This notebook runs secondary analyses on the outputs derived from detection.ipynb and stored in outputs/
- It additionally requires raw float data stored in SOCCOM_GO-BGC_LoResQC_LIAR_28Aug2023_netcdf/
- The maps require the ACC front locations stored in orsi\_park-durand\_so\_fronts\_.nc
    
