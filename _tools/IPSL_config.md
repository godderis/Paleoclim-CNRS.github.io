---
title: IPSL Config
author: Anta
toc: true
toc_sticky: true

---

# Download & Compile the code 

_Additional documentation can be found [here](https://forge.ipsl.jussieu.fr/igcmg_doc/wiki/DocHconfigAipslcm5a2)_

_First you have to choose the version of the model you want to install :_
- _Standard version  (ORCA grid - e.g. Modern simulations)_
- _Paleo version (PALEORCA)_

_Both can be run without ice, which requires additional changes in the code before compilation_

## Standard version
_In case you want to run simulations with a present-day land sea mask_

-	In the  $CCCWORKDIR directory, create a new IPSLCM5A2 directory
-	In IPSLCM5A2 directory, do a svn to load the required files from the server
-	Move to modipsl/util directory
-	Load the model files  [ ./model IPSLCM5A2.1 ]
-	Login & password are required in order to install ORCHIDEE =>login : sechiba, password : ipsl2000
-	In order to install LMDz : tape return so it ask for a login => login : lmdz-users, passwd : lmdz2020

```bash
# Load the model

 cd $CCCWORKDIR

 mkdir IPSLCM5A2

 cd IPSLCM5A

 svn co http://forge.ipsl.jussieu.fr/igcmg/svn/modipsl/trunk modipsl

 cd modipsl/util

 ./model IPSLCM5A2.1

```

__In case you want to remove ice in Antarctica, additional modification should be done before compiling the code. They are listed paleo section [here](#without-antarctic-ice-sheet).__

-	In modipsl/config/IPSLCM5A2 directory, uncomment line 100 from the Makefile
-	Compile with gmake

 ```bash
  cd ../config/IPSLCM5A2/

  vi Makefile

# Uncomment line 100

# Compile

 gmake

 ```
## Paleo version
_In case you want to run simulations with a paleo land sea mask_

In $CCCWORKDIR create new directory that will contain the model (e.g. PALEO-IPSL)

-	In PALEO-IPSLCM5A2 directory, do a svn to load the required files from the server
-	In  modipsl/util directory do ./model IPSLCM5A2.1 to load the code

```bash
# Load the model

 cd $CCCWORKDIR

 mkdir PALEO-IPSL

 cd PALEO-IPSL

 svn co http://forge.ipsl.jussieu.fr/igcmg/svn/modipsl/trunk modipsl

 cd modipsl/util

 ./model IPSLCM5A2.1

```

Additional modification have to be done to switch the code to paleo-version :

-	In /modipsl/modeles/NEMOGCM/NEMO/OPA_SRC, modify the files in TRA, LDF et  DIA directory (copy files from PATH/MODIFICATION-CODE)
-	In /modipsl/modeles/NEMOGCM/NEMO/TOP_SRC/PISCES, modify the files in P4Z (copy files from PATH/MODIFICATION-CODE/P4Z/)

### Without Antarctic ice-sheet

__In case you want to remove ice in Antarctica, additional modification should be done before compiling the code :__ 
_(If you want to run simulation with an ice-sheet on Antarctica, just skip this part and directly compile the code)_

Before compiling the code, you will have to modify the model component to remove ice:
-	In modipsl/modeles, create a new directory PALEO_LMDZ that contain two sub-directory PALEO_SRC and ORIGINAL_SRC
-	In ORIGINAL_SRC copy the 3 original files :
    - Modeles/LMDZ/libf/phylmd/hydrol.F90
    - Modeles/LMDZ/libf/phylmd/surf_landice_mod.F90
    - Modeles/LMDZ/libf/phylmd/fonte_neige_mod.F90
-	In PALEO_SRC, copy updated (from PATH/MODIFICATION-CODE/phylmd/) 
    - Paleorca_hydrol.F90_paleorca
    - Paleorca _surf_landice_mod.F90_paleorca
    - Paleorca_ fonte_neige_mod.F90_paleorca
-	In /modipsl/modeles/LMDZ/libf/phylmd, copy the 3 files you just added in PALEO_SRC instead of existing hydrol.F90 etc… files (be careful to keep original filel name).


Once all the modification have been done for the version of the model you need :

-	In modipsl/config/IPSLCM5A2 uncomment line 100 of Makefile
-	Compile the code  (gmake).

```bash
  cd ../config/IPSLCM5A2/

  vi Makefile

# Uncomment line 100

# Compile

  gmake

```
# Launch a new simulation
## Model architecture 
_Here are (very!) useful things to know on how the model is organized on the supercomputer_

1. Workspaces

Different model elements and output from simulation can be found in $CCCWORKDIR, $CCCSTOREDIR, $CCSSCRATCHDIR:
-	On $CCCWORKDIR you find the directory where you install & compile the model (contains code, boundary condition & parameterization files, executables) 
-	$CCCSCRATCHDIR is for temporary storage (it can be erased from time to time). Model output are stored there before being transferred to Storedir by post-processing 
-	$CCCSTOREDIR is the working space where model outputs are permanently stored 

2. Model architecture

 “MODELE/modipsl “ directory (exemple : IPSL-CM5A2/modipsl ou PALEOIPSL/modipsl) is subdivided in 4 directory :
-	« Config » contains parameterization files, experiments directory …  
-	« Modeles » contains code for each different model components 
-	« bin » contains executables. If compilation has been successfull, it should contains 4 individual files 
-	« libIGCM » contains model environment  (processor-related stuffs, error outputs etc...)

« MODELE/modipsl/config/IPSLCM5A2 »  directory contains several experiments directories :
- «  GENERAL » 
    -	POST : Post-processing files (Temporal evolution … 
    - PARAM : Initial parameters & part of boundary conditions (CO2, model timesteps, Orbital parameters etc…)
    -	DRIVER : Drivers for different model component. Deal with the year per year incrementation for example. 
-	« EXPERIMENTS «  : Classic setup for different types of simulations
    -	LMDZ : Atmosphere-only model
    -	LMDZOR : Atmosphere + land surface model
    -	IPSLCM : Coupled model (piControl=preindustrial ou pdControl=present-day)

## Run a simulation
_Here you will find general indications on which file you have to modify to setup a new simulation_

1. Generation of simulation directory

First you need to create a new directory for you simulation. For that you need to choose which model you want to use (Coupled, Atmosphere-Land surface) and to obtain a config.card file, that you can find in the MODELE/modipsl/config/IPSLCM5A2/EXPERIMENT directory. 

__The following example is to run a coupled simulation from scratch__

### ELC

- Copy the LMDZ config.card in the $CCCWORKDIR/MODELE/modipsl/config/IPSLCM5A2 directory
- Modify the config.card :
    -	JobName= Name_Experiment _(example : ELC-piControl)_
    -	DateBegin=1848-01-01
    -	DateEnd=1848-12-30
- Create the directory [../../libIGCM/ins_job]

 ``` bash
 
 cp EXPERIMENTS/LMDZ/CREATE_clim/config.card .
 
 ../../libIGCM/ins_job
 
 ```
 
2. Simulation setup
 
Then you will have to modify the following variables in the boundary condition file COMP/lmdz.card

- LMDZ_Physics=AP (l.8)
- Modify the config.def_actuel by config.def_preind (l.46) 

In the case of paleo simulation you migh need to modify the following lines as well :

_(be sure you only change the 1st part of each line and keep the name of the 2nd file in the line as it is in the original lmdz.card )_

__Example:__ (__PATH/mynew_TopoHR.nc__, Relief.nc), \



- Modify the relief file (Relief.nc), with a high resolution topography file (with masked bathymetry) (l.27)
- Modify the land-ice file (landiceref.nc), with the land-ice extension file (l.29)
- Modify the SST file (amipbc_sst_1x1.nc) with a SST file suitable for paleo (it can be one from previous coupled simulation or just take the generic 4X or 2X file depending on the pCO2 you will use) (l.31)
- Modify the sea-ice file (amipbc_sic_1x1.nc) with a SIC file suitable for paleo (it can be one from previous coupled simulation or just take the generic 4X or 2X file depending on the pCO2 you will use) (l.32)
- Uncomment the line relative to o2a.nc file (l.39) and modify it, with the o2a file you generated from the paleogeography



_Generic SST and SIC files can be found here:_
- PATH/BC_CM5A2/LMDZ/40Ma_ICE/sst_bc_clim_2X.nc
- PATH/BC_CM5A2/LMDZ/40Ma/no_sic_bc_clim.nc

You can also change some parameters in the PARAM/config.def_preind file:

__CO2 :__  

- co2_ppm = _AUTO_: DEFAULT = 0.280E+03 (l.32)

__Solar constant :__ 

- solaire = _AUTO_: DEFAULT = 1361.20 (l.27)

__Orbital configuration :__

- R_ecc = 0.06 (l.20)
- R_peri = 90 (l.22)
- R_incl = 24.5 (.24)


3. Launch the simulation

First you will need to reduce the time-wall (which is a 24h automaticaaly), because this type of simulation will run quickly:

 - In the Job_SimulationName file replace 84600 by 1800 (l.10 : #MSUB -T 86400  # Wall clock limit (seconds))

Then submit the job 

```bash

ccc_msub Job_SimulationName 

```

### LMDZOR

Once you have created the initial conditions with the ELC step you have to run an Atmosphere-Land Surface simulation


 
