# Regional MITgcm setup

## Before you start
  - Download MITgcm source code from the github repo at https://mitgcm.org
  - Read the documentation, especially chapter 3
  - Compile and execute the global ocean circulation example in the verification folder, "global_ocean.90x40x15"
  - Have access to python3 with the following packages, numpy, matplotlib, scipy, pandas, netCDF4, xarray, xmitgcm 

## Bathymetry
  - Download etopo2.nc (Smith and Sandwell, 1997) from [here](https://o2.eas.gatech.edu/data/etopo2.nc)
  - Original data is documented [here](https://sos.noaa.gov/catalog/datasets/etopo2-topography-and-bathymetry-natural-colors/#description-data-source)
  - An example for North Pacific domain for lon-lat grid at 2 degree resolution: [create_bathymetry.ipynb](https://github.com/takaito1/MITgcm_regional_setup/blob/main/create_bathymetry.ipynb)
  - The result is in a binary file (.bin)
  - In this example, the domain is (lon,lat,depth) = (60,40,42), small enough to run on a single CPU on desktop/laptop

![alt text](https://github.com/takaito1/MITgcm_regional_setup/blob/main/bathymetry.png?raw=true)
    
## Atmospheric forcing for bulk formula
  - Several atmospheric reanalysis products are available. In this example, I will use JRA55do [(Tsujino et al., 2018)](https://climate.mri-jma.go.jp/pub/ocean/JRA55-do/)
  - [Stewart et al (2020)](https://www.sciencedirect.com/science/article/pii/S1463500319302768) suggests RYF (repeat year forcing) based on May-1-1990 - Apr-30-1991
  - The files I used in this example are available [here](https://www.dropbox.com/s/ezqbpab0r1z7vey/jra55do-1990-1991.nc.tar.gz?dl=0). These files are available from ESGF following the link above
  - It contains 10m wind (u, v), 2m air temperature, specific humidity, downward short/long wave radiation, rain precipitation, snow precipitation, river runoff, ice sheet calving, and mean sea level pressure (total of 11 fields). Most of them are 3 hourly field.
  - An example for North Pacific domain is: [create_atmos_forcing.ipynb](https://github.com/takaito1/MITgcm_regional_setup/blob/main/create_atmos_forcing.ipynb)
  - The result is in a set of binary files (.bin)

![alt text](https://github.com/takaito1/MITgcm_regional_setup/blob/main/atmos_forcing.png?raw=true)

## Oceanic side boundary condition
  - Similar to the atmospheric forcing, there are several oceanic reanalysis products. In this example, I will use SODA version 3.12.2 [Carton et al., 2018](https://www2.atmos.umd.edu/~ocean/)
  - The files I used in this example are available [here](https://www.dropbox.com/s/o4xco4k1ddpichs/soda3.12.2-1990-1991.nc.tar.gz?dl=0)
  - It contains U, V, T, S and SSH
  - An example for North Pacific domain is: [create_ocean_bc.ipynb](https://github.com/takaito1/MITgcm_regional_setup/blob/main/create_ocean_bc.ipynb)
  - The result is in a set of binary files (.bin)
    
## Oceanic initial condition
  - Oceanic initial condition will be the state of rest with T and S interpolated from SODA reanalysis product.
  - An example for North Pacific domain is: [create_ocean_init.ipynb](https://github.com/takaito1/MITgcm_regional_setup/blob/main/create_ocean_init.ipynb)
  - The result is in a set of binary files (.bin)

![alt text](https://github.com/takaito1/MITgcm_regional_setup/blob/main/initcond.png?raw=true)
    
## Modify the source code and build executable
  - code/ contains customization to source code for North Pacific domain
  - input/ contains runtime options for North Pacific domain
  - Tested with the latest version of MITgcm (downloaded in June 2023)

## Biogeochemistry

