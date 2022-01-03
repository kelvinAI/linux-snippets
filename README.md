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
