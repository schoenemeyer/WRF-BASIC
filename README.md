# WRF-BASIC


## Basic Steps to create you input files to run WRF

The high level work flow looks like this:

<img src="https://github.com/schoenemeyer/WRF-BASIC/blob/master/wpswrf.png" width="552">

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


