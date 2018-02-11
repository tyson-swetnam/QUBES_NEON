This folder has Bash `.sh` files that can be used for installing OSGEO software on a Linux (Ubuntu) virtual machine.

If you haven't pulled the repository yet:

```
git clone https://github.com/tyson-swetnam/QUBES_NEON.git

cd QUBES_NEON/atmo

```

## Install GRASS GIS

Here I am building grass from source, installing several dependencies immediately before. 

GRASS also requires that its environment be set for graphical (GUI) interaction

Run the build shell file and immediately follow with the GUI setup:

```
. build_grass.sh && setup_grass.sh
```

## Install QGIS

Here I am installing QGIS from a binary (pre-built) 

Run the shell file:

```
. install_qgis.sh

```

## Install RStudio-Server

Because we are running on remote hardware, I want to use RStudio-Server, which I can access through my browser.

Here I am building RStudio-Server from its binary:

```
. install_rstudio.sh
```
