---
title: PALEO-PISCES offline Model
author: Anta
toc: true
toc_sticky: true

---
Reference paper for the PISCES model is [Aumont et al. 2015](https://gmd.copernicus.org/articles/13/3011/2020/gmd-13-3011-2020.html). You will find additional information about parameterization and appropiate references within this paper as well.

If siconc and wocetr_eff variables do not exist in you grid_T.nc anc grid_W.nc model output :

- ("clim" simulation) Use the script UpdateVariable.ksh to add them (you need to run the script twice : for woce and sic)
- ("IA" simulation) Use the script CopyVariable.ksh to add them 
