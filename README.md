# Installation environement ![CI status](https://img.shields.io/badge/build-passing-brightgreen.svg)



## OS : Linux Mint
Linux Mint 18.1 "Serena" - Cinnamon (64-bit)

`http://mirrors.evowise.com/linuxmint/stable/18.1/linuxmint-18.1-cinnamon-64bit.iso`



## Tools : CUDA / Nvidia driver

### Requirements
* GPU Graphic card


Check your driver version using NVIDIA Official website
(In our case we use cuda version 390.87) 

[NVIDIA](https://www.nvidia.fr/Download/index.aspx?lang=fr)

`https://www.nvidia.fr/Download/index.aspx?lang=fr`

Create global variable for NVidia driver by typing the following cmd :

`$ export CUDA_DRIVER_VERSION=390.87`

### Installation script 1

```bash
#!/bin/bash

sudo apt-get install -y gfortran git linux-image-generic linux-headers-generic linux-source linux-image-extra-virtual libopenblas-dev

if [ ! -e ./NVIDIA-Linux-x86_64-${CUDA_DRIVER_VERSION}.run ]
then
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/${CUDA_DRIVER_VERSION}/NVIDIA-Linux-x86_64-${CUDA_DRIVER_VERSION}.run
chmod +x ./NVIDIA-Linux-x86_64-${CUDA_DRIVER_VERSION}.run
fi

/etc/modprobe.d/blacklist-nouveau.conf
TMP_FILE=`mktemp`
cat << EOF > $TMP_FILE
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
EOF
sudo bash -c "cat $TMP_FILE >> /etc/modprobe.d/blacklist-nouveau.conf"
rm $TMP_FILE

sudo update-initramfs -u
echo -n "install_cuda_driver step 1 finished, press enter to reboot "
read TMP_VAR
sudo reboot

```

* Run script 

```
$ chmod 777 script.sh
$ ./script1.sh
```

### Installation script 2

```bash
#!/bin/bash

export CUDA_DRIVER_VERSION=390.87

chmod +x ./NVIDIA-Linux-x86_64-${CUDA_DRIVER_VERSION}.run
sudo sh ./NVIDIA-Linux-x86_64-${CUDA_DRIVER_VERSION}.run --no-opengl-files --silent
echo -n "install_cuda_driver step 2 finished, press enter to reboot "
read TMP_VAR
sudo reboot

```
* Follow this guidlines on another computer and go to terminal interface with the following steps:

`Ctrl+alt+f2`

* After login, kill x-server « mdm »  with :

`sudo service mdm stop`

Not working ? try with « gdm » or « xorg ».

* Run script 

```
$ chmod 777 script.sh
$ ./script2.sh
```
### Check NVIDIA

`lspci | grep -i nvidia`

### Update compiler
```
$ sudo apt-get update
$ sudo apt-get install gcc
$ sudo apt-get install linux-headers-$(uname -r)
```

### Download and install toolkit
[TOOLKIT](https://developer.nvidia.com/cuda-downloads?target_os=Linux)


`https://developer.nvidia.com/cuda-downloads?target_os=Linux`

* Install 

```
sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```


## Tools : Qt / QtCreator
```
# Installation de Qt

sudo apt-get install build-essential

sudo apt-get install qtcreator

sudo apt-get install qt5-default

#DONE

```

## Tools : Opencv 3.4.3

### Install Dependencies
```
sudo apt-get install build-essential 
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev

sudo apt-get install build-essential 
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev

sudo apt-get install libgtk-3-dev

sudo apt-get install libatlas-base-dev gfortran pylint

sudo apt-get install python2.7-dev python3.5-dev
```
### Install Opencv 3.4.3 

```
#Download Opencv and contrib
wget https://github.com/opencv/opencv/archive/3.4.3.zip -O opencv-3.4.3.zip
#contrib
wget https://github.com/opencv/opencv_contrib/archive/3.4.3.zip -O opencv_contrib-3.4.3.zip

sudo apt-get install unzip

#Extraction
unzip opencv-3.4.3.zip
unzip opencv_contrib-3.4.3.zip


cd  opencv-3.4.3
mkdir build
cd build

```

### CMAKE

```
$ cmake-gui

```
```
Change parameters :
WITH_CUDA -> OK
CUDA_ARCH_BIN -> 3.0 3.5 3.7 5.0 5.2 6.0 6.1 7.0
OPENCV_EXTRA_MODULES_PATH -> (YOUR OPENCV CONTRIB LOCATION)/opencv_contrib-3.4.3/modules

-> CONFIGURE -> GENERATE

close CMAKE-GUI
```
 *** 
### MAKE

Back to terminal and write :

```
$ make -j4
$ sudo make install
```

 *** 

## Editors
* AIT ABDELALI Hamd
* DERROUZ Hatim
* EL BOUZIADY Abderahim
* LHOUSSIN Mabrouk



## License
* [MoVITS](http://scholar.um5.ac.ma/movits)
