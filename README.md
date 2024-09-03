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

#stack the different raster file
ras_current<-stack(c(bio1, bio2, bio4, bio6, bio8, bio9, bio12, bio14, bio15, bio19))
```
upload the excel file with longitude (x) and latitude (y) data. In this case present in column 9 and 10 respectively

```
locations = read_excel("Dataset_west_olive.xlsx")

## Extracting environmental values for each source population
Env <- data.frame(extract(ras_current, locations[,9:10]))
write.table(Env, "Current_clim")

```

