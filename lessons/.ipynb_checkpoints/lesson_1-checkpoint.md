# Working on Cloud

While these instructions are written for use on CyVerse Cloud service, called Atmosphere, you can also do the later lessons on a remote cluster, HPC, or localhost running Jupyter.

The following instructions involve the installation of data science software on CyVerse Atmosphere or XSEDE Jetstream instances.

## Step 1: Account Creation

[Create a CyVerse account](https://learning.cyverse.org/projects/cyverse-account-creation-quickstart/en/latest/) 

or

Create a [NSF XSEDE account](https://portal.xsede.org/#/guest) and request an allocation on [Jetstream](https://iujetstream.atlassian.net/wiki/spaces/JWT/pages/29720582/Quick+Start+Guide).

## Step 2: Starting a Cloud Instance

I suggest using a featured image with a Graphic User Interface (GUI). 

On Atmosphere, see: [Ubuntu 14.04](https://atmo.cyverse.org/application/images/1135) or [16.04 GUI base](https://atmo.cyverse.org/application/images/1453).

On Jetstream, see: [Ubuntu 14.04](https://use.jetstream-cloud.org/application/images/54) or [Ubuntu 16.04](https://use.jetstream-cloud.org/application/images/107).

Allow the instance to reach 'active' status. Instances  typically take 3-7 minutes to boot up the first time.

Log into the Apache Guacamole web shell to access terminal, or use `ssh` from a terminal on your local machine

```
ssh CyVerseUserName@<INSTANCE-IP-ADDRESS>
```

Or from the Apache Guacamole Desktop, right click mouse, select Terminal Emulator

### To access Clipboard in Guacamole

- Open Clipboard and virtual keyboard
  - On a standard keyboard: `ctrl` + `alt` + `shift` key
  - On a MAC OS X keyboard: `control` + `command ⌘` + `shift` key

- Select your text or paste text into the clipboard window.

- Close the Clipboard window by selecting `control` + `command ⌘` + `shift` keys again

- Right click with your mouse or double tap fingers on touchpad to paste in the web shell or Desktop

### Web Desktop screen resolution:

type `xrandr` in a Web Desktop terminal to see available resolutions.

an example for 1080HD screen size:

```
xrandr -s 1920x1080
```

## Step 3: Clone this Repository onto the VM

Open the Web Shell or `ssh` into the machine with the public IP address

Change into a directory you're comfortable installing into and have `sudo` privileges.

The next step is to `git clone` this repository onto your VM:

```
git clone https://github.com/cyverse-gis/focus-forum.git
```

change directory to the new repo with these installation scripts:

```
cd focus-forum
```

### Step 4: Setting up CyVerse Data Store and iRods iCommands 

[CyVerse Instructions](https://pods.iplantcollaborative.org/wiki/display/DS/Setting+Up+iCommands)

[Instructions from iRODS](https://packages.irods.org/)
[Download from iRODS](https://irods.org/download/)

```
wget -qO - https://packages.irods.org/irods-signing-key.asc | sudo apt-key add -
echo "deb [arch=amd64] https://packages.irods.org/apt/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/renci-irods.list
sudo apt-get update

sudo apt-get install irods-icommands
```

```
$ iinit
```
You will be queried to set up your `irods_environment.json`

Enter the following:

|statement  |input  |  
|-----------|-------|
| DNS | *data.cyverse.org* |
|port number|*1247*|
|user name| *your user name*|
|zone|*iplant*|

Set up auto-complete for iCommands
[instructions](https://pods.iplantcollaborative.org/wiki/display/DS/Setting+Up+iCommands)

Download [i-commands-auto.bash](https://pods.iplantcollaborative.org/wiki/download/attachments/6720192/i-commands-auto.bash).
In your home directory, rename i-commands-auto.bash to .i-commands-auto.bash
In your .bashrc or .bash_profile, enter the following: 
source .i-commands-auto.bash

## Step 5: EZ Installation Quick Start Tutorial

CyVerse has set up an `ez` installation for Docker, Singularity, and Jupyter Notebooks (via Anaconda)

Follow the [CyVerse Learning Center's Quick Start](https://cyverse-ez-quickstart.readthedocs-hosted.com/en/latest/) 

### Jupyter Notebooks & Lab

Install Anaconda with Python3 (Featured instances on Atmosphere and Jetstream)

```
ezj
```

Change ownership of the Anaconda installation

```
sudo chown $USER:iplant-everyone /opt/anaconda3 -R
```

Start [Jupyter Lab](https://github.com/jupyterlab/jupyterlab)

```
jupyter lab
```

Install [additional kernels](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)

```
sudo add-apt-repository ppa:chronitis/jupyter
sudo apt-get update
sudo apt-get install irkernel ijavascript
```

On your local host you can `ssh` tunnel to an Atmosphere or Jetstream VM running Jupyter:

```
ssh -nNT -L 8888:localhost:8888 $USER@$IP_ADDRESS
```

#### Install [Google Drive to Jupyter Lab](https://github.com/jupyterlab/jupyterlab-google-drive)

Note: This was broken recently...

Requires [Node.js 5+](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)

Google Drive requires port 8888 or 8889 with port forwarding to work

```
jupyter labextension install @jupyterlab/google-drive
```
