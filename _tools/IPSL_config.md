---
title: IPSL Config
author: Anta
toc: true
---

# Download & Compile the code 

_Additional documentation can be found [here](https://forge.ipsl.jussieu.fr/igcmg_doc/wiki/DocHconfigAipslcm5a2)_

_First you have to choose the version of the model you want to install :_
- _Standard version  (ORCA grid - e.g. Modern simulations)_
- _Paleo version (PALEORCA)_

_Both can be run without ice, which requires additional changes in the code before compilation_

## Standard version
_In case you want to run simulations with de present-day land sea mask_

-	In the  $CCCWORKDIR directory , create a new IPSLCM5A2 directory
-	In  IPSLCM5A2 directory, do a svn to load the required files from the server
-	Move to modipsl/util directory
-	Load the model files  [ ./model IPSLCM5A2.1 ]

-	Login & password are required in order to install ORCHIDEE. Login :sechiba, passwd: ipsl2000

-	In order to install LMDz : tape return so it ask for a login => login/passwd
lmdz-users/lmdz2020
-	

__In case you want to remove ice in Antarctica, additional modification should be done before compiling the code. They are listed in the grey square in the following page__

-	In modipsl/config/IPSLCM5A2 directory, uncomment line 100 from the Makefile
-	Compile with gmake

 

