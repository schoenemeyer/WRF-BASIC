# WRF-BASIC


## Basic Steps to create you input files to run WRF

The high level work flow looks like this:

<img src="https://github.com/schoenemeyer/WRF-BASIC/blob/master/wpswrf.png" width="552">
This figure is taken from the official User Guide under 
https://dtcenter.org/wrf-nmm/users/docs/user_guide/V3/users_guide_nmm_chap3.pdf


Install WPS
```
./geogrid.exe
./ungrib.exe
./geogrid.exe
```
Go to the main directory of WRF

```
mpirun -np n ./real.exe
```
creates boundary and initial data
run the main forecast  
```
mpirun -np n ./wrf.exe
```


## Example for Domain 1 in Central Europe Jan 23 2019 with 12km resolution

<img src="https://github.com/schoenemeyer/WRF-BASIC/blob/master/wrf.png" width="552">
If you are interested in specific date you can use ncdump, that will provide a list of variables.    

```
ncdump -h wrfout_d01_2019-01-23_15_00_00

```

e.g.  if you are looking for Temperatures, you would do    

```
ncdump -h wrfout_d01_2019-01-23_15_00_00 | grep TEMP
                T2:description = "TEMP at 2 M" ;
                TH2:description = "POT TEMP at 2 M" ;
                TSLB:description = "SOIL TEMPERATURE" ;
                SSTSK:description = "SKIN SEA SURFACE TEMPERATURE" ;
                TSK:description = "SURFACE SKIN TEMPERATURE" ;
                T00:description = "BASE STATE TEMPERATURE" ;
                TISO:description = "TEMP AT WHICH THE BASE T TURNS CONST" ;
                TMN:description = "SOIL TEMPERATURE AT LOWER BOUNDARY" ;
                SST:description = "SEA SURFACE TEMPERATURE" ;
                SST_INPUT:description = "SEA SURFACE TEMPERATURE FROM WRFLOWINPUT FILE" ;
[thomas@localhost run]$ 

```

