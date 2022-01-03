# linux-snippets
Useful Linux scripts for reference


# Tesseract compilation from source
# Run this from the main tesseract directory
# Set the necessary env variables below according to your system 
# The following example demonstrates when leptonica is installed in $HOME/local_packages
```
./autogen.sh
export LIBLEPT_HEADERSDIR=$HOME/local_packages/include  
export PKG_CONFIG_PATH=$HOME/local_packages/lib/pkgconfig  
./configure --prefix=$HOME/local_packages/ --with-extra-libraries=$HOME/local_packages/lib  
make -j10  
make install -j10 
```


# Installing tesserocr python package
```
export CPPFLAGS=-I$HOME/local_packages/include
export PKG_CONFIG_PATH=$HOME/local_packages/lib/pkgconfig
pip install tesserocr
```

# Updatinhg LD_LIBRARY_PATH
LD_LIBRARY_PATH environment variable should be updated to point to where tesseract is installed. 
Eg. export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/local_packages/lib
 
To update environment variables for jupyter notebook in docker containers, modify kernel.json which is located here path_to_anaconda/envs/pytorch38/share/jupyter/kernels/python3. ( will be different depending on your setup).  

Add "env" key:  
```
 "env": {"LD_LIBRARY_PATH":"$LD_LIBRARY_PATH:$HOME/local_packages/lib"}
```

