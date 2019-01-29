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
creates boundary and initial data for the forecast. Then you can run the main forecast  

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
Reading data directly from the netcdf files can be easily done with the utilities 

http://www2.mmm.ucar.edu/wrf/src/read_wrf_nc.f

Many more tools are available on the website   
http://www2.mmm.ucar.edu/wrf/users/download/get_sources.html#utilities    

This is an example reading the output from the forecast    

```
./read_wrf_nc wrfout_d01_2019-01-23_15_00_00 INPUT FILE IS: wrfout_d01_2019-01-23_15_00_00
  
  error opening netcdf file wrfout_d01_2019-01-23_15_00_00
[thomas@localhost WRFV3]$ ./read_wrf_nc run/wrfout_d01_2019-01-23_15_00_00
 INPUT FILE IS: run/wrfout_d01_2019-01-23_15_00_00
  
  
 GLOBAL ATTRIBUTES:
  
TITLE                                    :  OUTPUT FROM WRF V3.8.1 MODEL
START_DATE                               : 2019-01-23_12:00:00
SIMULATION_START_DATE                    : 2019-01-23_12:00:00
WEST-EAST_GRID_DIMENSION                 :   225
SOUTH-NORTH_GRID_DIMENSION               :   200
BOTTOM-TOP_GRID_DIMENSION                :    32
DX                                       :   12000.0000
DY                                       :   12000.0000
SKEBS_ON                                 :     0
SPEC_BDY_FINAL_MU                        :     1
USE_Q_DIABATIC                           :     0
GRIDTYPE                                 : C
DIFF_OPT                                 :     1
KM_OPT                                   :     4
DAMP_OPT                                 :     0
....
.....
......



```

For example, get the 2m Temperature for 15 UTC at grid point 114 120 , you would write    
```
./read_wrf_nc -S 114 120 1  run/wrfout_d01_2019-01-23_15_00_00 | grep T2
T2            2   XY  224  199    1   (x= 114 y= 120 z=   1)     271.0364990      K
```


