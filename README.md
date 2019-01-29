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


# Example for Domain 1 in Central Europe Jan 23 2019 with 12km resolution

<img src="https://github.com/schoenemeyer/WRF-BASIC/blob/master/wrf.png" width="552">

