# HumanInfluence_TippingPoints
This is code and data for the project with Prashastha

# I. Constructing the state diagram: 
CODE: xxxx.R (from step b to e)
To construct the state diagram we follow a previously established method. The steps are descrobed below.
  a. Demarcate sub-Saharan Africa into regions corresponding to 50 PVC units of CEP: This was done on QGIS. After the CEP raster was imported into QGIS, we used RasterCalculator to obtain all pixels that had CEP value corresponding to a particular range. For instance, <Raster> >= 500 AND <Raster> <550 
would result in a new image where '1' was assigned to all pixels that satisfied this condition and '0' for all pixels that did not. 
This raster was then 'Polygonised' in QGIS to obtain the shapefile for the region corresponding to CEP regime between 500 and 550.

  b. The polygon mask thus generated (in step 1) was then used to 'CLIP' the EVI raster. This generated a clipped EVI raster corresponding to the regions falling within each 50 units CEP. 

  c. The frequency histogram for each of the masked EVI rasters was generated in R using the code: hist(raster), and the density kernels using density(raster). From the density kernels, the modes of the distributions were obtained using a small function: 

  d. The modes were verified by visually comparing to the density histograms and noted. In the case two modes were detected, we also noted if the smaller peak was less than 25% (height) of the larger peak.

  e. The modes were then input into R and state diagram was plotted. 
  
