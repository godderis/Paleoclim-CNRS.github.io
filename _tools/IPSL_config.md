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

__In case you want to remove ice in Antarctica, additional modification should be done before compiling the code. They are listed in the grey square in the following page__

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

__In case you want to remove ice in Antarctica, additional modification should be done before compiling the code :__ 

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
# Load the model

 cd $CCCWORKDIR

 mkdir PALEO-IPSL

 cd PALEO-IPSL

 svn co http://forge.ipsl.jussieu.fr/igcmg/svn/modipsl/trunk modipsl

 cd modipsl/util

 ./model IPSLCM5A2.1

```

