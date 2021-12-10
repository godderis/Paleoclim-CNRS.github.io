---
title: PALEO-PISCES offline Model
author: Anta
toc: true
toc_sticky: true

---
Reference paper for the PISCES model is [Aumont et al. 2015](https://gmd.copernicus.org/articles/13/3011/2020/gmd-13-3011-2020.html). You will find additional information about parameterization and appropiate references within this paper as well.

# Download & Compile the code

- In the $CCCWORKDIR directory, create a new PALEO-PISCES directory
- In PALEO-PISCES directory, do a svn to load the required files from the server

```bash
#Download Modipsl
cd $CCCWORKDIR
mkdir PALEOPISCES
cd PALEOPISCES

svn co http://forge.ipsl.jussieu.fr/igcmg/svn/modipsl/trunk modipsl

# Download PISCES
cd modipsl/util
./model NEMO_v6.1

# if NEMO version do not exists use ./model -h to check the existing version

# Compile XIOS (on Irene)
cd ../modeles/XIOS
./make_xios --arch X64_IRENE --full --prod --job 8

# ARCH file / key_xios
cp $WORKDIR/IPSLCM5A2/modipsl/modeles/NEMOGCM/ARCH/arch-X64_IRENE.fcm $WORK-DIR/PALEOPISCES/modipsl/modeles/NEMOGCM/ARCH/.

vi PALEOPISCES/modipsl/modeles/NEMOGCM/CONFIG/ORCA2_OFF_PISCES/cpp_ORCA2_OFF_PISCES.fcm
- add key_xios2


```

- Modify PISCES source code to have the updates about nutrient input
- Compile Nemo 

```bash
# Compile  NEMO
cd PALEOPISCES/modipsl/modeles/NEMOGCM/CONFIG/
./makenemo -n ORCA2_OFF_PISCES -m X64_IRENE -j 8

#Executable
cp PALEOPISCES/modipsl/modeles/NEMOGCM/CONFIG/ORCA2_OFF_PISCES/BLD/bin/nemo.exe   PI-SCES/modipsl/bin/orca2offpisces.exe

```

# Launch a new simulation

## Get the boundary conditions files from the coupled simulation

- In case it is the firs time you run an offline PISCES simulation, create a directory (ex: BC_PISCES_OFFLINE) where you will store the boundary conditions for the simulations. 
 
- Create a directory for the simulation and transfer grid_T.nc, grid_V.nc, grid_W.nc and grid_U.nc from OCE/ , ptrc.nc from MBG/ and icemod.nc from ICE/

In case siconc and wocetr_eff variables do not exist in you grid_T.nc anc grid_W.nc model output :

- ("clim" simulation) Use the script UpdateVariable.ksh to add them (you need to run the script twice : for woce and sic)
- ("IA" simulation) Use the script CopyVariable.ksh to add them 

You will probably need to change the writing rights on the files by doing _chmod +w file.nc_

Best is to directly add those variables in the simulation setup :
In file PARAM/file_def_nemo-opa.xml : 
 
```bash
- Replace 

 <field field_ref="iceconc"      name="siconc"  />  (l.205)
 
  by 
  
 <field field_ref="iiceconc"      name="siconc"  />
 
- And add 

 <field field_ref="wocetr_eff"   name="wocetr_eff"  /> (l.265)
 
```
## Compute scaling factor from runoff

To do so you need the grid_T.nc file from the coupled simulation and the script runoffs.jnl to obtain annually cumulated runoff.
To get the scaling factor, you have to divide this value by value from a modern simulation (2352948)

__Total nutrient input similar to present-day__

This scaling factor in use to calculate initial concentration of dissolved elements in the river. To do so you have to modify file PARAM/NAMELIST/namelist_pisces_cfg (l.70-76)

```bash

<    dicconc = xxxe-6    ! dissolved inorganic carbon concentration in rivers (in Mmol/m3)
<    docconc = xxxe-6   ! dissolved organic carbon concentration in rivers (in Mmol/m3)
<    dinconc = xxxe-8   ! dissolved inorganic nitrogen concentration in rivers (in Mmol/m3)
<    donconc = xxxe-8    ! dissolved organic nitrogen concentration in rivers (in Mmol/m3)
<    dipconc = xxxe-9    ! dissolved inorganic phosphorus concentration in rivers (in Mmol/m3)
<    dopconc = xxxe-9   ! dissolved organic phosphorus concentration in rivers (in Mmol/m3)
<    dsiconc = xxxe-6  ! dissolved silicate concentration in rivers (in Mmol/m3)

```

__Total nutrient input similar to present-day__

This scaling factor is used to scale damping value (l.81-84)

```bash
  alkmean = 2426.    ! Mean alkalinity concentration
  po4mean = 2.165    ! Mean phosphate concentration
  no3mean = 30.90    ! Mean nitrate concentration
  silmean = 91.51    ! Mean silicate concentration
```


as well as to modifiy initial state for the MBG/ component as explained below


## Generate initial state for MBG/ component

- To generate initial state for the ocean-biogeochmistry use the script ScaleNutrient.ksh 

__Total nutrient input similar to present-day__

In this case you just need to extract value from the ptrc.nc file and to scale the O2 variable to have the right unit.

__Nutrient input adapted to climate__

In this case you have, in addition, to be sure that each file has been scaled by the factor you calculated from the runoff of the coupled simulation. 

## Define value of nutrient concentration

__Total nutrient input similar to present-day__

At the end, the total supply should roughly correspond to the one from the control simulation (ORCA2_OFF_PISCES/PROD/ORCA2clim/PISC-Control-RunOff/DEBUG/MBG_PISC-Control-RunOff_05000101_05001231_ocean.output)

```
N Supply : 36.096027 TgN/yr
Si Supply : 154.645665 TgSi/yr
P Supply : 2.572411 TgP/yr
Alk Supply : 35.141530 Teq/yr
DIC Supply : 586.800500 TgC/yr
```

So it is better to run the simulation for one year only and to adjust initial concentration if it does not fit. In this case, after modifying concentrations in PARAM/NAMELIST/namelist_pisces_cfg, change the DateEnd in the config.card and the JobStatus to 'OnQueue' in the run.card and re-submit the Job.

__Nutrient input adapted to climate__
