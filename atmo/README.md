# Run software from Containers

## RStudio-Server w/ Docker

Run RStudio Server using Docker ([Boettiger and Eddelbuettel 2017](https://journal.r-project.org/archive/2017/RJ-2017-065/RJ-2017-065.pdf)).

First, install Docker on the Atmosphere VM:

```
ezd

# remove sudo privilege for using Docker by adding yourself to the `docker` group

sudo usermod -aG docker $USER

# exit the terminal and restart your ssh connection 

exit

```

Now, run the Docker container - here I'm using [Rocker Geospatial](https://github.com/rocker-org/geospatial) in a detached `-d` form, connected to the port `8787` of the VM.

```
docker run -d -p 8787:8787 rocker/geospatial:latest
```

Create an SSH tunnel to the VM:

```
ssh -nNT -L 8787:localhost:8787 $YOUR-USER-NAME@<VM IP ADDRESS>
```

Open your browser and navigate to `localhost:8787` the username and password for the instance are default `rstudio`. 

## QGIS, GRASS, ans SAGA w/ Singularity 

Instead of building GIS software from source (which can take a long time), you can pull the same build from [Singularity-Hub](https://www.singularity-hub.org/collections/567)

My [Github Repo](https://github.com/tyson-swetnam/osgeo-singularity) has the Singularity file and build instructions.

[Install Singularity](http://singularity.lbl.gov/docs-installation) on your local machine.

Install Singularity on the Atmosphere VM:

```
ezs

singularity pull --writable --name osgeo-singularity.simg shub://tyson-swetnam/osgeo-singularity

```

# Install binaries and build from source.

This folder has Bash `.sh` files that can be used for installing OSGEO software on a Linux (Ubuntu) virtual machine.

If you haven't pulled the repository yet:

```
git clone https://github.com/tyson-swetnam/QUBES_NEON.git

cd QUBES_NEON

```

## Install GRASS GIS

Here I am building grass from source, installing several dependencies immediately before. 

GRASS also requires that its environment be set for graphical (GUI) interaction

Run the build shell file and immediately follow with the GUI setup:

```
. atmo/build_grass.sh && setup_grass_env.sh
```

## Install QGIS

Here I am installing QGIS from a binary (pre-built) 

Run the shell file:

```
. atmo/install_qgis.sh

```

## Install RStudio-Server

Because we are running on remote hardware, I want to use RStudio-Server, which I can access through my browser.

Here I am building RStudio-Server from its binary:

```
. atmo/install_rstudio.sh
```
