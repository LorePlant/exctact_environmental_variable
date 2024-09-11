# exctact_environmental_variable
The following code show how to extract environmental variable from raster file for specific georeferenced point.
In this example I'm going to exctract 10 different bioclimatic variable from CHELSA raster

```
library(raster)
library("readxl")

bio1<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio1_studyarea_ext.tif"))
bio2<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio2_studyarea_ext.tif"))
bio4<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio4_studyarea_ext.tif"))
bio6<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio6_studyarea_ext.tif"))
bio8<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio8_studyarea_ext.tif"))
bio9<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio9_studyarea_ext.tif"))
bio12<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio12masked_studyarea_ext.tif"))
bio14<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio14_studyarea_ext.tif"))
bio15<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio15_studyarea_ext.tif"))
bio19<- raster(paste("/lustre/rocchettil/biovar_studyarea/bio19_studyarea_ext.tif"))
names(bio1) = 'BIO1'
names(bio2) = 'BIO2'
names(bio4) = 'BIO4'
names(bio6) = 'BIO6'
names(bio8) = 'BIO8'
names(bio9) = 'BIO9'
names(bio12) = 'BIO12'
names(bio14) = 'BIO14'
names(bio15) = 'BIO15'
names(bio19) = 'BIO19'
#stack the different raster file
ras_current<-stack(c(bio1, bio2, bio4, bio6, bio8, bio9, bio12, bio14, bio15, bio19))
```

We can create a spatial grid x y with cell centered coordinates. 
The spatial grid is like a data frame with x long and y lat longitude derived from the center of each pixel and the value derived from all the raster layers
```
#spatial grid

coord_r<-rasterToPoints(ras_current, spatial = TRUE)
map_pts<-data.frame(x = coordinates(coord_r)[,1], y=coordinates(coord_r)[,2], coord_r@data)

```

upload the excel file with longitude (x) and latitude (y) data. In this case present in column 9 and 10 respectively

```
locations = read_excel("Dataset_west_olive.xlsx")

## Extracting environmental values for each source population
Env <- data.frame(extract(ras_current, locations[,9:10]))
write.table(Env, "Current_clim")

```

