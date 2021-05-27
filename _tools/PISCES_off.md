---
title: PALEO-PISCES offline Model
author: Anta
toc: true
toc_sticky: true

---
Reference paper for the PISCES model is [Aumont et al. 2015](https://gmd.copernicus.org/articles/13/3011/2020/gmd-13-3011-2020.html). You will find additional information about parameterization and appropiate references within this paper as well.

In case siconc and wocetr_eff variables do not exist in you grid_T.nc anc grid_W.nc model output :

- ("clim" simulation) Use the script UpdateVariable.ksh to add them (you need to run the script twice : for woce and sic)
- ("IA" simulation) Use the script CopyVariable.ksh to add them 

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
