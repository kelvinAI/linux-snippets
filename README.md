# linux-snippets
Useful Linux scripts for reference

## Compiling and install leptonica
1. Download the latest leptonica from http://www.leptonica.org/download.html
2. Extract, configure and install

```
./configure
sudo make
sudo checkinstall
```

# How to install packages in local folder without root
For debian distros, packages can be downloaded from https://packages.ubuntu.com/
```
dpkg -x libXXX.deb $HOME/target_dir 
```
The binaries, libs and pkgconfigs will now be in the target_dir. Make sure they are included in the PKG_CONFIG_PATH env variable (such as below) during installation 


# Tesseract compilation from source
# Run this from the main tesseract directory
# Set the necessary env variables below according to your system 
# The following example demonstrates when leptonica is installed in $HOME/local_packages
```
./autogen.sh
export LIBLEPT_HEADERSDIR=$HOME/local_packages/include  
export PKG_CONFIG_PATH=$HOME/local_packages/lib/pkgconfig:$HOME/local_packages/usr/lib/x86_64-linux-gnu/pkgconfig:$HOME/local_packages/usr/share/pkgconfig
./configure --prefix=$HOME/local_packages/ --with-extra-libraries=$HOME/local_packages/lib --enable-debug  
make -j10  
make install -j10 
```


# Installing tesserocr python package
```
export CPPFLAGS=-I$HOME/local_packages/include
export PKG_CONFIG_PATH=$HOME/local_packages/lib/pkgconfig
pip install tesserocr
```


# Updating LD_LIBRARY_PATH
LD_LIBRARY_PATH environment variable should be updated to point to where tesseract is installed. 
Eg. export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/local_packages/lib
 
To update environment variables for jupyter notebook in docker containers, modify kernel.json which is located here path_to_anaconda/envs/pytorch38/share/jupyter/kernels/python3. ( will be different depending on your setup).  

kernel.json
```
 "env": {"LD_LIBRARY_PATH":"$LD_LIBRARY_PATH:$HOME/local_packages/lib"}
```

# Download trained language models to tessdata directory
The trained models can be found here. https://tesseract-ocr.github.io/tessdoc/Data-Files.html
Download the desired language models and move them into the tessdata directory. Depending on where the tesseract installation path is, it should be located at $install_path/share/tessdata

# Training
- Set TESSDATA_PREFIX env variable to point to tessdata directory
- run make clean in tesstrain root to clean before training (may fix the issue with unable to read boxes in .tiff images)

# Useful commands
pkg-config
```
pkg-config --cflags --libs pangocairo
```

# Dockerfile
Steps: 
need to install:

wget
wget 
build-essential

docker run --name tess ubuntu:focal  
docker image ls -a  
docker container ls -a  
docker start container_name  
docker attach container_name (to get shell)  
docker commit CONTAINER_NAME(or hash) NEW_IMAGE_NAME 
docker save -o container.tar IMAGE_HASH

# Build singularity image from docker.tar savefile  
singularity build tesseract-5.0.1.sif docker-archive://tesseract-5.0.1.tar  

# Fix localtime issue for singularity while creating docker image  
https://github.com/apptainer/singularity/issues/5465  
export TZ=Asia/Singapore  
ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone  
