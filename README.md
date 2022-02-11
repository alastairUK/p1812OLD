# Recommendation ITU-R P.1812-6 (MATLAB/Octave Implementation)

This code repository contains a MATLAB/Octave software implementation of Recommendation ITU-R P.1812. 
This Recommendation contains a path-specific propagation prediction method for point-to-area terrestrial services in the frequency range 30 MHz to 6 000 MHz.  
The reference version of this code (approved by ITU-R Working Party 3K) is published by Study Group 3 on their ([Software, Data, and Validation Web Page](https://www.itu.int/en/ITU-R/study-groups/rsg3/Pages/iono-tropo-spheric.aspx) 

| File/Folder                | Description                                                         |
|--------------------------------------------------------------------------------------------------|
|tl_p1812.m                  | MATLAB function implementing Recommendation ITU-R P.1812-6          |
|validate_p1812.m            | MATLAB script used to validate the implementation of                |
                               Recommendation ITU-R P.1812-6 as defined in the file 
                               tl_p1812.m using a set of test terrain profiles provided 
                               in the folder ./validation_profiles/

 ./validation_profiles/	     - Folder containing a proposed set of terrain profiles for
                               validation of MATLAB implementation (or any other software
                               implementation) of Recommendation ITU-R P.1812-6

 validation_result_log.csv  - Template for reporting final and intermediate results of basic
                               transmission loss computation according to Recommendation ITU-R P.1812-6

 ./validation_results/       - Folder containing all the results written during the transmission loss
                               computations for the set of terrain profiles defined
                               in the folder ./validation_profiles/

 ./private/                  - Folder containing the functions used by tl_p1812.m and validate_p1812.m



## Inputs ##

| Variable          | Type   | Units | Limits       | Description  |
|-------------------|--------|-------|--------------|--------------|
| `d__km`           | double | km    | 0 <= `d__km` | Great circle path distance between terminals |
| `h_1__meter`      | double | meter | 1.5 <= `h_1__meter` <= 20 000 | Height of the low terminal |
| `h_2__meter`      | double | meter | 1.5 <= `h_2__meter` <= 20 000 | Height of the high terminal |
| `f__mhz`          | double | MHz   | 100 <= `f__mhz` <= 30 000 | Frequency |
| `T_pol`           | int    |       |              | Polarization <ul><li>0 = Horizontal</li><li>1 = Vertical</li></ul> |
| `time`            | double |       | 1 <= `time` <= 99 | Time percentage |
 
## Outputs ##

Outputs to P.528 are contained within a defined `Results` structure.

| Variable   | Type   | Units | Description |
|------------|--------|-------|-------------|
| `d__km`    | double | km    | Great circle path distance.  Could be slightly different than specified in input variable if within LOS region |
| `A__db`    | double | dB    | Basic transmission loss |
| `A_fs__db` | double | dB    | Free space basic transmission loss |
| `A_a__db`  | double | dB    | Median atmospheric absorption loss |
| `theta_h1__rad` | double | rad | Elevation angle of the ray at the low terminal |
| `propagation_mode` | int |  | Mode of propagation <ul><li>1 = Line of Sight</li><li>2 = Diffraction</li><li>3 = Troposcatter</li></ul> |
| `warnings` | int    |       | Warning flags |
