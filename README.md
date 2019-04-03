# HumanInfluence_TippingPoints
Codes and data for reconstructing the state diagrams.

# I. Determining 'Natural' and 'Human-impacted' areas
The HII raster was aggregated to 25degrees (so that it is consistent with the scale at which the EVI and the climate data was considered). Following this, it was imported into R 
    library(raster)
    dat <- raster('hiiraster.tif')
Following this, the density kernel for the raster was generated using density(). The values corresponding to the 15th, 25th, and 33rd percentiles (henceforth thresholds) were obtained. 

The HII raster was then imported into QGIS. Using RasterCaluclator (Raster --> RasterCaluclator), all pixels with values above and below the thresholds were obtained and saved separately. For instance,
    <HII Raster> >=4.1 [saved as human-impacted for 25th percentile]
    <HII Raster> <4.1 [saved as natural for 25th percentile]
Each of these clipped rasters were then polygonised for future masking.

# II. Constructing the state diagram: 
CODE: xxxx.R (from step b to e)
The entire procedure is performed separately for the human-impacted and the natural regions.
To construct the state diagram we follow a previously established method. The steps are descrobed below.
  a. Demarcate human-impacted/natural areas into regions corresponding to 50 PVC units of CEP: This was done on QGIS. After the CEP raster was imported into QGIS, we used RasterCalculator to obtain all pixels that had CEP value corresponding to a particular range. For instance, <Raster> >= 500 AND <Raster> <550 
would result in a new image where '1' was assigned to all pixels that satisfied this condition and '0' for all pixels that did not. 
This raster was then 'Polygonised' in QGIS to obtain the shapefile for the region corresponding to CEP regime between 500 and 550.

  b. The polygon mask thus generated (in step 1) was then used to 'CLIP' the EVI raster. This generated a clipped EVI raster corresponding to the regions falling within each 50 units CEP. 

  c. The frequency histogram for each of the masked EVI rasters was generated in R using hist(raster), and the density kernels using density(raster). From the density kernels, the modes of the distributions were obtained using a small function: 

  d. The modes were verified by visually comparing to the density histograms and noted. In the case two modes were detected, we also noted if the smaller peak was less than 25% (height) of the larger peak.

  e. The modes were then input into R and state diagram was plotted. (See below for data in case you want to reproduce the plots)
  
# III. Data for plotting the state diagram
The data for plotting the state diagram is included in the EXCEL sheet named ''. The column names are:
  Bin: corresponding to the 50 units CEP bin 
  Mode: One or two modes determined from the histogram (see above)
  Cat: An index assigned to each unique bin
  Ratios: 1 if the ratio of the smaller mode is greater than 25% of the larger mode and 0.25 if it is smaller. 
Note: The code to plotting the state diagram using this spreadsheet is included in the code shared above. 
  
