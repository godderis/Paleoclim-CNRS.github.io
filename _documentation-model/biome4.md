---
title: Biome4
author: Delphine
toc: true
toc_sticky: true
---

# Introduction

# Installation

## Install Netcdf

According to the [website](https://pmip2.lsce.ipsl.fr/synth/biome4.shtml) biome4 needs netcdf 3.X to work however netcdf 4.7.4 has been tested and everything seemed to work.

### Install from Package Manager

On Macs newer than Mojave you can use [brew](https://formulae.brew.sh/formula/netcdf). On Unix based systems you should also be able to do something similar:
- Mac `brew install netcdf`
- Unix `apt install libnetcdf-dev libnetcdff-dev`
- Windows ??

### Source

<div class='alert alert-info'>
    You will need to compile:
    <ul>
        <li>
            HDF5 (working)
        </li>
        <li>
            NetCDF c (working)
        </li>
        <li style="color:red">
            NetCDF Fortran (not working)
        </li>
    </ul>
</div>

You can also recompile the packages from Source if your system is not supported.

#### HDF5 (needed by NetCDF)

Do this from some directory where you want to keep the source files.

1. `mkdir hdf5 & cd hdf5`

1. `curl https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.12/hdf5-1.12.0/src/hdf5-1.12.0.tar.gz -o hdf5.tar.gz`
1. `tar -xvzf hdf5.tar.gz`
1. `cd hdf5-1.12.0`
1. `./configure --prefix=/usr/local/hdf5 --with-zlib`
1. `make`
1. `make install`
<div class='alert alert-info'>
    If `make install` fails with Permssion denied:
    <ol>
    <li>
        Create the folder (using sudo)
    </li>
    <li>
        Claims writes `chown YOUR_USERNAME FOLDERNAME`
    </li>
    </ol>
    Run `make install`
</div>

#### NetCDF-C

1. Go to Source dir (`cd ../..` normally?) and run `mkdir netcdf & cd netcdf`

1. `curl -L https://github.com/Unidata/netcdf-c/archive/v4.7.4.tar.gz  -o netcdf.tar.gz`
1. `tar -xvzf netcdf.tar.gz`
1. `cd netcdf-c-4.7.4`
1. `CPPFLAGS=-I/usr/local/hdf5/include LDFLAGS=-L/usr/local/hdf5/lib   ./configure --prefix=/usr/local/netcdf --enable-remote-fortran-bootstrap`
1. `make install`
<div class='alert alert-info'>
    If `make install` fails with Permssion denied:
    <ol>
    <li>
        Create the folder (using sudo)
    </li>
    <li>
        Claims writes `chown YOUR_USERNAME FOLDERNAME`
    </li>
    </ol>
    Run `make install`
</div>

#### NetCDF Fortran
<ol>

    <li> 
        `make build-netcdf-fortran`
    </li>
    <div class='alert alert-info'>
        You will need git for this to work the easiest way to do this on Mac is to install xcode.
        
        If you get an error about git and it is installed check line 23 `/dev/null1` doesn't seem to work on Mac you will need to replace it with `/dev/null`
    </div>

    <li>
        `make install-netcdf-fortran`
    </li>
</ol>

Add the `/usr/local/netcdf/bin` to your ~/.bashrc or ~/.zshrc to make netcdf executables availible everywhere

## Biome4

From Source directory

See [here](https://ubuntuforums.org/showthread.php?t=2247248) for bug online / doc.

1. `mkdir biome4 && cd biome4`
1. `curl https://pmip2.lsce.ipsl.fr/share/synth/biome4/biome41.tar.gz -o biome4.tar.gz`
1. `tar -xvzf biome4.tar.gz`
1. `make clean`
1. replace value after NETCDFINCDIRr with value from `nc-config --includedir`
1. replace `NETCDFLIB = -lnetcdff -lnetcdf`
1. replace NETCDFLIBDIR with the value from `nc-config --libdir`
1. replace `FC=g77` with `FC=gfortran` (please install before hand should be with xcode)
1. remove `-fno-silent` from FFLAGS (If problem with Rank Mismatch try adding `-fallow-argument-mismatch` to FFLAGS)
1. Edit biome4.f line 250 and replace with: `       write(*,'(A,2F7.2,3F7.1)')` 

# Usage