
---
title: NCO tips
author: Anta
toc: true
toc_sticky: true

---
__Change variables attributes__ 

ncatted -a attribute_name,variable_name,m,f,value infile.nc

__Rename variable or dimension__

ncrename -v old_name,new_name infile.nc
ncrename -d old_name,new_name infile.nc

__Drop variables from a file__

ncks -x -v variable1,variable2 infile.nc outfile.nc
