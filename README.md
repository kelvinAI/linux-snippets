# linux-snippets
Useful Linux scripts for reference


# Tesseract compilation from source
# Run this from the main tesseract directory
# Set the necessary env variables below according to your system 
# The following example demonstrates when leptonica is installed in $HOME/local_packages
```
./autogen.sh
export LIBLEPT_HEADERSDIR=$HOME/local_packages/include  
export PKG_CONFIG_PATH=$HOME/local_packages/lib/pkgconfig:$HOME/local_packages/usr/lib  
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


