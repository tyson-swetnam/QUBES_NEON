# Build VM on CyVerse Atmosphere or XEDE Jetstream

When using the Atmosphere 'Web Shell' emulated terminal on either Atmosphere or Jetstream, there is a secret key command to open the clipboard:

`⌘ command` + `control` + `shift` on a Mac

`alt` + `control` + `shift` on a PC

Install Jupyter notebooks with Anaconda3

```
ezj
```

After the installation completes, a Jupyter Notebook will be running on port `8888` you can exit the notebook by depressing `control` + `c` twice.

change user permissions to install new programs in the Anaconda directory

```
sudo chown $USER:root /home/anaconda3/ -R
```

Install [Jupyter Lab](https://github.com/jupyterlab/jupyterlab)

```
conda install -c conda-forge jupyterlab
```

Start Jupyter Lab

```
jupyter lab
```

