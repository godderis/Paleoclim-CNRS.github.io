---
title: IPSL-CM5A2 Model
author: Anta
toc: true
toc_sticky: true

---
Reference paper for the IPSL-CM5A2 model is [Sepulchre et al. 2020](https://gmd.copernicus.org/articles/13/3011/2020/gmd-13-3011-2020.html). You will find additional information about each component of the model and appropiate references within this paper as well. 

# Download & Compile the code 

_Additional documentation on how to download and compile the code can be found [here](https://forge.ipsl.jussieu.fr/igcmg_doc/wiki/DocHconfigAipslcm5a2)_.

_Information provided in the following text is well suited for running simulations on IRENE supercomputer (TGCC). Adaptation might be required to run the code on Jean Zay supercomputer (IDRIS) : [here](https://forge.ipsl.jussieu.fr/igcmg_doc/wiki/Doc/ComputingCenters/IDRIS)._


_First you have to choose the version of the model you want to install :_
- _Standard version  (ORCA grid - e.g. Modern simulations)_
- _Paleo version (PALEORCA)_

_Both can be run without ice, which requires additional changes in the code before compilation_


_/!\ Note that in case you want to compile the code on Jean-Zay supercomputer, you cannot compile the code login on your 'normal account'_ : 

```
_Note that there is a specific front-end to perform compilations tasks. 
This front-end allows you to compile faster and in one go : 
default XIOS compilation may crash because of restricted interactive ressources per user on the standard front-end. 
You can access the compilation front-end by using ssh protocol :
ssh your_login@jean-zay-pp.idris.fr_

```

__In case compilation failed you can use gmake clean to clean the directory__


## Standard version
_In case you want to run simulations with a present-day land sea mask_

-	In the  $CCCWORKDIR directory, create a new IPSLCM5A2 directory
-	In IPSLCM5A2 directory, do a svn to load the required files from the server
-	Move to modipsl/util directory
-	Load the model files  [ ./model IPSLCM5A2.1 ]
-	Login & password are required in order to install ORCHIDEE & LMdz => They are available upon request to ... 

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
_(If you want to run simulation WITH an ice-sheet on Antarctica, just skip this part and directly compile the code)_

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

First you need to create a new directory for you simulation. For that you need to choose which model you want to use (Coupled, Atmosphere-Land surface) and to obtain a config.card file, that you can find in the MODELE/modipsl/config/IPSLCM5A2/EXPERIMENT directory.


<div style="color: #8738b5">
 All the boundary conditions files you will need can be generated with the NetCDF_file_editor.
</div>


__The following example is to run a coupled simulation from scratch__

### ELC

#### 1. Generation of simulation directory

- Copy the LMDZ config.card in the $CCCWORKDIR/MODELE/modipsl/config/IPSLCM5A2 directory
- Modify the config.card :
    -	JobName= Name_Experiment [example : ELC-SimulationNAme)]
    -	DateBegin=1854-01-01
    -	DateEnd=1854-12-30
- Create the directory [../../libIGCM/ins_job]

 ``` bash
 
 cp EXPERIMENTS/LMDZ/CREATE_clim/config.card .
 
 ../../libIGCM/ins_job
 
 ```
 
#### 2. Simulation setup
 
Then you will have to modify the following variables in the boundary condition file COMP/lmdz.card

- LMDZ_Physics=AP (l.8)
- Modify the config.def_actuel by config.def_preind (l.46) 

In the case of paleo simulation you migh need to modify the following lines as well :

_(be sure you only change the 1st part of each line and keep the name of the 2nd file in the line as it is in the original lmdz.card )_

```
# Example:

 (PATH/mynew_TopoHR.nc,   Relief.nc),\
```


- Modify the relief file (Relief.nc), with a high resolution topography file (with masked bathymetry) (l.27)
- Modify the land-ice file (landiceref.nc), with the land-ice extension file (l.29)
- Modify the SST file (amipbc_sst_1x1.nc) with a SST file suitable for paleo (it can be one from previous coupled simulation or just take the generic 4X or 2X file depending on the pCO2 you will use) (l.31)
- Modify the sea-ice file (amipbc_sic_1x1.nc) with a SIC file suitable for paleo (it can be one from previous coupled simulation or just take the generic 4X or 2X file depending on the pCO2 you will use) (l.32)
- Uncomment the line relative to o2a.nc file (l.39) and modify it, with the o2a file you generated from the paleogeography



_Generic SST and SIC files can be found here:_
- PATH/BC_CM5A2/LMDZ/40Ma_ICE/sst_bc_clim_2X.nc
- PATH/BC_CM5A2/LMDZ/40Ma/no_sic_bc_clim.nc

You can also change some parameters in the PARAM/config.def_preind file:

- CO2 (l.32):

```
co2_ppm = _AUTO_: DEFAULT = 0.280E+03 
```

- Solar constant (l.27) :

```
solaire = _AUTO_: DEFAULT = 1361.20 
```

- Orbital configuration (l. 20-24):

```
R_ecc = 0.06 
R_peri = 90 
R_incl = 24.5 
```

#### 3. Launch the simulation

First you will need to reduce the time-wall (which is a 24h automatically), because this type of simulation will run quickly:

 - In the Job_SimulationName file replace 84600 by 1800 (l.10 : #MSUB -T 86400  # Wall clock limit (seconds))

Then submit the job 

```bash

ccc_msub Job_SimulationName 

```

### LMDZOR

Once you have created the initial conditions with the [ELC](#elc) step you have to run an Atmosphere-Land Surface simulation

#### 1. Generation of simulation directory


- Copy the LMDZOR config.card in the $CCCWORKDIR/MODELE/modipsl/config/IPSLCM5A2 directory (you can also copy it from a previous simulation)
- Modify the config.card :
    -	JobName= Name_Experiment [example : LMDZOR-SimulationNAme)]
    -	DateBegin=1854-01-01
    -	DateEnd=1854-12-30
- Create the directory [../../libIGCM/ins_job]

 ``` bash
 
 cp EXPERIMENTS/LMDZOR/clim_pdControl/config.card .
 
 ../../libIGCM/ins_job
 
 ```
 
#### 2. Simulation setup
 
Then you will have to modify the following variables in the boundary condition file COMP/lmdz.card

- LMDZ_Physics=AP (l.9)
- ConfType=preind (l.17)

### Without Antarctic ice-sheet

__In case you want to remove ice in Antarctica (and have compiled the code to do so), additional modification should be done for running the LMDZOR simulation :__ 
_(If you want to run simulation WITH an ice-sheet on Antarctica, just skip this part and see below)_

- In your WORKDIR (ideally you would have already created a directory where you store all you boundary conditions - $WORKDIR/YOUR_BC_DIRECTORY - ...), create a MOD-ETAT0-LMDZ/SimulationName directory
- Copy the following files into it :
    -	/ccc/store/cont003/gen2212/UserName/IGCM_OUT/LMDZ/SimulationName/ATM/Output/Boundary/ELC-SimulationName_clim_limit.nc
    -	/ccc/store/cont003/gen2212/UserName/IGCM_OUT/LMDZ/SimulationName/ATM/Output/Restart/ELC-SimulationName_clim_start.nc
    - /ccc/store/cont003/gen2212/UserName/IGCM_OUT/LMDZ/SimulationName/ATM/Output/Restart/ELC-SimulationName_clim_startphy.nc
    
- You then have to modify those files to add some ice on the south pole grid point (this is mandatory for the ORCHIDEE model to run) : 

``` bash

Ncap2 -s «FLIC(9025)=1.» -s «FTER(9025)=0.» ELC-SimulationName_clim_startphy.nc ELC-SimulationName_clim_startphy_corr.nc
Ncap2 -s «FLIC(:,9025)=1.» -s «FTER(:,9025)=0.» ELC-SimulationName_clim_limit.nc ELC-SimulationName_clim_limit_corr.nc

```

Then you need to specified boundary conditions files from the corresponding ELC simulation (l.53-54) and specifity the path for corresponding ELC start file as well as for the newely created startphy and limit files as below 

```
[InitialStateFiles]
List=   ($STOREDIR/IGCM_OUT/LMDZ/ELC-SimulationName/ATM/Output/Restart/ELC-SimulationName_clim_start.nc,    start.nc),\
        ($WORKDIR/YOUR_BC_DIRECTORY/MOD-ETAT0-LMDZ/SimulationName/ELC-SimulationName_clim_startphy_corr.nc, startphy.nc)
        
[BoundaryFiles]
List=()
ListNonDel= ($WORKDIR/YOUR_BC_DIRECTORY/MOD-ETAT0-LMDZ/SimulationName/ELC-SimulationName_clim_limit_corr.nc, limit.nc),\
```


### With a Antarctic Ice-sheet 
You need to specified boundary conditions files from the corresponding ELC simulation (l.53-54) :

- either specify CREATE=ELC-SimulationName (l.12) (Put the name of the ELC simulation you have done juste before) and be sure that the l.53-58 uses the CREATE variable to define the path. Or simply give the complete path to the start, starphy and limit files as below

```
[InitialStateFiles]
List=   ($STOREDIR/IGCM_OUT/LMDZ/ELC-SimulationName/ATM/Output/Restart/ELC-SimulationName_clim_start.nc,    start.nc),\
        ($STOREDIR/IGCM_OUT/LMDZ/ELC-SimulationName/ATM/Output/Restart/ELC-ELC-SimulationName_clim_startphy.nc, startphy.nc)
        
[BoundaryFiles]
List=()
ListNonDel= ($STOREDIR/IGCM_OUT/LMDZ/ELC-SimulationName/ATM/Output/Boundary/ELC-SimulationName_clim_limit.nc, limit.nc),\
```

### For all types of simulation
Then you will have to modify the following variables in the boundary condition file COMP/orchidee.card

- Modify the soil file (soils_param.nc), with a soil parameter file that has the correct geography  (l.14)
- Modify the routing file (routing.nc), with the new routing file (l.15)
- Modify the Plant Functional Type file (PFTmap.nc) with the PTF file that has the correct geography (l.16)


You can also change some parameters in the PARAM/config.def_preind file :

- CO2 (l.32):

```
co2_ppm = _AUTO_: DEFAULT = 0.280E+03 
```

- Solar constant (l.27) :

```
solaire = _AUTO_: DEFAULT = 1361.20 
```

- Orbital configuration (l. 20-24):

```
R_ecc = 0.06 
R_peri = 90 
R_incl = 24.5 
```

#### 3. Launch the simulation


```bash

ccc_msub Job_SimulationName 

```

### Coupled Model

Once you have the 1 year-length [LMDZOR](#lmdzor) simulation you can now run a coupled simulation. But before being able to launch it you will need to create restart files for the OASIS coupler. 

#### Create file for OASIS

- If it does not exist create a directory on your $CCCWORKDIR where you will generates the files ($CCCWORKDIR/BC_IPSLCM5A2) then download the CPLRESTART routines using a svn.

The CPLRESTART directory should contains 5 files :

   - README.txt
   -	FillOceRestart.py is used to add missing variables in the OASIS restarts 
   - Nemo.py is used with FillOceRestart.py
   -	CreateRestartOce4Oasis.bash is used to create atmosphee restart for OASIS
   -	CreateRestartAtm4Oasis.bash is used to create ocean restart for OASIS

In most of the case you will only need to create restart for the atmosphere : 
 - Copy the histmth.nc file from the corresponding LMDZOR simulation
 - Extract the last month with nco
 - Run the CreateRestartOce4Oasis.bash script
 - Move the files you generated in a directory spectific to you simulation

```bash
#Download the useful scripts

  mkdir $CCCWORKDIR/BC_IPSLCM5A2
  svn co http://forge.ipsl.jussieu.fr/igcmg/svn/TOOLS/CPLRESTART CPLRESTART

#Create atmospheric restart for OASIS

  cd CPLRESTART
  cp $STOREDIR/IGCM_OUT/LMDZOR/PROD/clim/SimulationName/ATM/Output/MO/SimulationName_xxxx_xxxx_histmth.nc .

  ncks -d time_counter,-1,-1 Nom_fichier_histmth.nc Nom_fichier_histmth_last_month.nc
  
# You need to modify the netcdf-hdf5 package otherwise it will not work

  module load netcdf-c/4.3.3.1
  #module load netcdf/4.3.3.1_hdf5_parallel # Version for XIOS
  
  bash ./CreateRestartAtm4Oasis.bash Nom_fichier_histmth_last_month.nc
  
  mkdir SimulationName

  mv add_dim.nco create_flxat.nco flxat_LMD9695_maskFrom_ORCA2.3.nc icbrg_LMD9695_maskFrom_ORCA2.3.nc icshf_LMD9695_maskFrom_ORCA2.3.nc lonlat2xyz.nco      
 SimulationName_xxxx_xxxx_histmth.nc lonlat2xyz.nco SimulationName
```

You will use the flxat_LMD9695_maskFrom_Unknown.nc file late to setup the coupled simulation.

#### 1. Generation of simulation directory

- Copy coupled-model config.card in the $CCCWORKDIR/MODELE/modipsl/config/IPSLCM5A2 directory (you can also copy it from previous coupled simulation)
- Modify the config.card :
    -	JobName= Name_Experiment [example : CPL-SimulationNAme)]
    -	CalendarType=360d [Choose leap years (leap) or no leap years (noleap) or 360 days-long years (360d = the one we usually use for paleo simulations)]
    -	DateBegin=1855-01-01
    -	DateEnd=4855-12-30 [This will fix the length of the simulation, we usually run coupled simulatios for at least 3,000 years]
- Create the directory [../../libIGCM/ins_job]

 ``` bash
 
cp EXPERIMENTS/IPSLCM/piControl/config.card .
 
 ../../libIGCM/ins_job
 
 ```

#### 2. Simulation setup

You can still modify the config.card :
 -	PeriodLength = 1Y
 - Restart : In case of standard coupled simulation you will only restart the components related to LMDZOR (LMDZ, SRF, MBG) so set the _Restart =_ field to 'y' and then specify the path of the related simulation as in the following example. For all the other component let the _Restart =_ field to 'n'.

__Example:__
```
#D-- ATM -
[ATM]
WriteFrequency="1M"
# If config_Restarts_OverRule == 'n' next 4 params are read
Restart= y
# Last day of the experience used as restart for this component if Restart=y
RestartDate=1854-12-30
#D- Define restart simulation name for all components
RestartJobName=LMDZOR_SimulationName
#D- Path Server Group Login
RestartPath=$STOREDIR/IGCM_OUT/LMDZOR/PROD/clim

```

 - PackFrequency=10Y (l.184)
 - TimeSeriesFrequency=NONE (l.187)
 -	SeasonalFrequency=100Y [Gives you the number of years that will be average in the SE outputs, usually we set up this field to 100Y] (l.190)


_If you do not run the code on Irene but on Jean-Zay or other super-computer you may need to modyfile the number of processor in the _Executable_ part (be careful in case you do that you will need to modify the jpni, jpnj and jpnij PARAM/namelist_ORCA2_cfg accordingly)_

Modify the boundary conditions files for the atmosphere in COMP/lmdz.card
 - LMDZ_Physics=AP (l.9)
 - ConfType=preind (l.14)
 - LMDZ_NMC_monthly=n (l.44)
 - Replace Post_1M_histmthNMC and Post_1M_paramLMDZ_phy by NONE (l.100-101)

```
(histmthNMC.nc,    ${R_OUT_ATM_O_M}/${PREFIX}_1M_histmthNMC.nc,    NONE),    \
(paramLMDZ_phy.nc, ${R_OUT_ATM_O_M}/${PREFIX}_1M_paramLMDZ_phy.nc, NONE), \

```

Then you will have to modify the following variables in the boundary condition file COMP/orchidee.card

- Modify the soil file (soils_param.nc), with a soil parameter file that has the correct geography  (l.14)
- Modify the routing file (routing.nc), with the new routing file (l.15)
- Modify the Plant Functional Type file (PFTmap.nc) with the PTF file that has the correct geography (l.16)


Modify the boundary conditions files for the Ocean in COMP/opa.card

- K1rowdrg.nc, M2rowdrg.nc, chlorophyll_surface_40Ma.nc, runoffs_ORCA2_depths.nc, sali_ref_clim_monthly.nc, coordinates.nc and mask_itf.nc are usually standard files you use in all the simulation (for Cenozoic simulation at least (?), except if you generate new tides files for example) and can be found in PATH/BC_CM5A2/NEMO/40Ma/filename.nc
- sss_data.nc, sst_data.nc, data_1m_potential_temperature_nomask.nc and data_1m_salinity_nomask.nc are also standardized files (?)
- bathy_meter.nc, ahmcoef.nc, subbasins.nc, geothermal_heating.nc are files you need to generates from paleogeography you use.

- Replace Post_1D files by NONE (l. 61-62)

```
# For example 

(${config_UserChoices_JobName}_1d_grid_T.nc, ${R_OUT_OCE_O_D}/${PREFIX}_1D_grid_T.nc     , NONE),\
```

In the COMP/pisces.card
 - Replace Post_1D_bioscalar by NONE (l.52)

```
(${config_UserChoices_JobName}_1d_bioscalar.nc     , ${R_OUT_MBG_O_M}/${PREFIX}_1D_bioscalar.nc , NONE)
```

In stomate.card
 - Replace Post_1M_stomate_history.nc and Post_1M_stomate_ipcc_history by NONE (l.28)

```
[OutputFiles]
List=   (stomate_history.nc,      ${R_OUT_SBG_O_M}/${PREFIX}_1M_stomate_history.nc,      NONE),    \
        (stomate_ipcc_history.nc, ${R_OUT_SBG_O_M}/${PREFIX}_1M_stomate_ipcc_history.nc, NONE)
```

You also need to modify the COMP/oasis.card with the file you created from the corresponding LMDZOR simulation. [If it does not remind you something, you may be have missed this step [here](#create-file-for-oasis)]
 - Specify the flatx and sstoc files. The sstoc file should correspond to the SST file you used in the previous ELC step. You can also create it using specific script in case you want to restart the ocean from an existing simulation. 

_Generic SST files can be found here:_
- PATH/BC_PALEOIPSL/COUPLER/40Ma-ICE-SL/sstoc_2X.nc

```
[InitialStateFiles]
List=   ($WORKDIR/CPLRESTART/SimulationName/flxat_LMD9695_maskFrom_Unknown.nc, flxat.nc), \
        (PATH/sstoc_2X.nc, sstoc.nc)
```

 - Specify the grids,masks,areas and MOZAIC-related files (l.15-21)

__Example:__
```
[BoundaryFiles]
List=   ()
ListNonDel= ($WORKDIR/IGCM/CPL/IPSLCM5A2/PALEORCA2.SimulationNamexLMD9695/grids.nc, grids.nc),\

```

Then in PARAM/field_def_nemo-opa.xml:

Then in PARAM/namelist_ORCA2_cfg. cp_cfg is the grid you use (orca2 or paleorca), rn_rdt is the timestep of the ocean, and jpni, jpnj and jpnij are the distribution of processor (have to correspond with the number of processors you setup in the config.card)

```
   cp_cfg      =  "paleorca"               !  name of the configuration
   
   rn_rdt      = 4800     !  time step for the dynamics (and tracer if nn_acc=0)
   
   jpni        =   4       !  jpni   number of processors following i (set automatically if < 1)
   jpnj        =  15       !  jpnj   number of processors following j (set automatically if < 1)
   jpnij       =  60       !  jpnij  number of local domains (set automatically if < 1)
```


You can also change some parameters in the PARAM/config.def_preind file :

- CO2 (l.32):

```
co2_ppm = _AUTO_: DEFAULT = 0.280E+03 
```

- Solar constant (l.27) :

```
solaire = _AUTO_: DEFAULT = 1361.20 
```

- Orbital configuration (l. 20-24):

```
R_ecc = 0.06 
R_peri = 90 
R_incl = 24.5 
```

#### 3. Launch the simulation

You need to change the number of year that will be done during one run (that can last up to 24h). In the Job_SimulationName file, change the period number (l.76). Usually we setup it to 60 or 70 years.

```
#D- Number of execution in one job
PeriodNb=60
```

Then you can finally launch your simulation

```bash

ccc_msub Job_SimulationName 

```

# Restarting from an existing simulation

## Normal restart

## Update bathymetry and restart
In some case you may want to do small bathymetry modification but you do not want to restart your simulation from scratch (because it will take to long). In this case you can (sometimes ?) re-generate salinity and temperature field from an existing simulation with similare paleogeography and use them as boundary conditions for the new simulation.
 
 - Modify the bathymetry locally using your favorite tool. Be sure you keep the variable names and dimension as in the initial file.
 - Extract salinity (so) and temperature (tethao) variables from the gridT.nc output of the simulation you want to restart from 

```bash
ncks -v so SimulationName_gridT.nc SimulationName_gridT_so.nc 
ncks -v thetao SimulationName_gridT.nc SimulationName_gridT_thetao.nc 
```

 - Regenerate the temperature and salinity fields using Create_thetao.f90, Create_so.f90 and Create_thetao_so.ksh scripts. Before running them you need to read the comments insides and modify the files path inside.
- Use the newly-created files in the PARAM/opa.card 


Then you need to regenerate restart files for OASIS (both atmosphere and ocean) and use them in the PARAM/oasis.card

In most of the case you can restart the LMDZOR-related components (LMDZ, SRF, SBG) in the config.card and specify the path from the coupled simulation you restart from.


# Useful tips

__1.  Where to find/store boundary conditions__

- Most of the time boundary conditions from a simulation can be find in user workdir withtin the BC_IPSLCM5A2 or BC_PALEOIPSL directory, classified by model component and by simulation (or at list it should !!). 

__2. (Normal) crash when you launch your 1st simulation ever__

- Check in the Job_SimulationName you did not make any mistake in the path of boundary conditions (in this case the error message is usually : 'xxx.nc does not exist')
- Useful bash command if grep -ir error . It can help you track 'error' or 'E R R O R' or other key_word that may help you (maybe to find the bug)

__3. How to generates missing SE__

- Well explained <a href="https://forge.ipsl.jussieu.fr/igcmg_doc/wiki/Doc/CheckDebug#Restartingtheseasonalmeancalculation" target="_blank">here</a> (point 4.5)

