# bioRad
bioRad is an R package for extracting and visualising biological signals from weather radar data.

The version in this branch has been specifically prepared for review purposes of the paper "bioRad: biological analysis and visualization of weather radar data".

# installation
To install `bioRad` complete these four steps:

### 1. rhdf5
bioRad requires the rhdf5 library to read [hdf5](https://support.hdfgroup.org/HDF5/) files. This library is available through bioconductor (not CRAN). To install, run in R:
``` 
source("http://bioconductor.org/biocLite.R")
biocLite("rhdf5")
```


### 2. bioRad 
You are now ready to install the bioRad package. In R, first load the devtools package, then install using `install_github`:
```
library(devtools)
devtools::install_github("adokter/bioRad@ecography")
```
If your installation completed correctly, you can load bioRad with `library(bioRad)`, which should give you the following:

```
> library(bioRad)
Loading package ‘bioRad’ version 0.3.0 ...
Warning: no running Docker daemon found
Warning: bioRad functionality requiring Docker has been disabled

To enable Docker functionality, start Docker and run 'checkDocker()' in R
```

On Windows 7, some users have had an installation problem with 32-bits package versions. To suppress the building of 32-bits packages (and use 64-bits only) install with:
```
devtools::install_github("adokter/bioRad@ecography", args="--no-multiarch")
```

### 3. Docker (optional)
You only need to install Docker if:
* you want to run the [vol2bird](https://github.com/adokter/vol2bird) algorithm.
* you want to analyze NEXRAD data. The tools to convert NEXRAD data into ODIM format require Docker.

#### 3.a Install Docker
The functionality of [vol2bird](https://github.com/adokter/vol2bird), an algorithm to extract vertical profiles of birds from weather radar data, is available in bioRad through Docker.

Go to the [Docker](https://www.docker.com/) webpage for instructions on how to install Docker on your local system. On 8 Dec 2016 Docker is available for Windows 10 Professional or Enterprise 64-bit, MacOS Yosemite 10.10.3 or above, or any linux/unix distribution.

Without a Docker installation, the bioRad package disables volbird automatically. All the other tools will still work.

#### 3.b Setup Docker
Docker needs local drives to be available for Docker containers. To enable:
* right click the Docker (whale) icon on your task or menu bar
* select settings -> shared drives
* select the drives where you will be processing radar files
* click apply

### 4. run bioRad in R
To load the package:
```
library(bioRad)
```
To pull up the main help page:
```
?bioRad
```
To open the vignette with several exercises covering the functionality of bioRad:
```
vignette("bioRad-overview")
```

### install note 1: rgdal on linux and mac OS v10.11 or older:
bioRad requires an installation of rgdal, which can be fetched from CRAN. The GDAL and PROJ.4 libraries are external to the rgdal package, and, when installing the package from source, must be correctly installed first.

You can use the package managing systems, like Macports on Mac, to install these dependencies, e.g.
```
sudo port install proj
sudo port install gdal +expat
```
When compiling rgdal you need to specify the installation directory of the PROJ.4 and GDAL libraries that rgdal depends on. Install from source using the following command (example here with `/opt/local/` as the leading path, which is the directory where the Macports package managing system installs PROJ.4 and GDAL):
```
install.packages('rgdal',configure.args=c('--with-proj-include=/opt/local/include', '--with-proj-lib=/opt/local/lib', '--with-gdal-config=/opt/local/bin/gdal-config'),type="source")
```

### Install note 3: Virtualbox / Hyper-V conflicts
Unfortunately, Hyper-V can not run together with Virtualbox. When you want to use Virtualbox after running Docker, you need to disable Hyper-V, requiring a reboot of the system. [Here](https://marcofranssen.nl/switch-between-hyper-v-and-virtualbox-on-windows/) some instructions on how to set up a dual-boot system fairly easily (haven't tested this myself yet)
