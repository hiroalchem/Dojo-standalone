# Dojo standalone

Varieties of software have been developed to manage electron microscopic (EM) images, some of which have provided functions to handle automated EM segmentation in connectomics. However, only few aim for the proofreading of automated EM segmentation that involves agglomeration/futher segmentation, most of which work only on a specific platform with databases, and some is not open-source.


   Here I present a open-source, multi-platform, and standalone version of such proofreading software - Dojo standalone from a part of Rhoana pipeline (Pfister lab/Harvard, 2014; http://www.rhoana.org/dojo/). Dojo has provided functions for proof reading and 3D visualization, and I modified this software for desktop use. Dojo standalone has been built on Python3.5/2.7, Javascript, and webGL on Windows10. It should also work on Linux and Mac (although I have not tested it). Thus, users can easily modify it for their own use.


## In addition to the original Dojo:

1) Codes were refactored for stability and Python3.5 compatibility. 
2) A small gui was equipped to control dojo at a desktop pc.
3) Many input/output image file formats are supported. 
4) Plugin section was created. Users can easily insert new Python functions.


## Requirements
A software package for Windows10/64bit is provided (pyinstaller version). If you do not use this, please build a Python3.5/2.7 anaconda environment on your pc with the following modules:


1) openCV3, pypng, pillow, libtiff, wxpython, mahotas, h5py, tornado, lxml, numpy, scipy, scikit-image, pypiwin32, stl

2) marching cubes from ilastik. This is necesssary only for a Plugin function. C-compilation is required: https://github.com/ilastik/marching_cubes

## How to use:

1-x. Download Dojo_pyinstaller.zip on Windows10/64bit from https://www.dropbox.com/s/95wraf6qwgbp9jf/Dojo_pyinstaller_Ver3.zip?dl=0 (120MB file). Unzip it, and click main.exe to confirm the launch of a small GUI.

1-y. Download all the github files on a PC with Python environment. Execute "python main.py" to confirm the launch of a small GUI.

2-a. Download a Dojo/Mojo-format file (eg. https://www.dropbox.com/s/pxds28wdckmnpe8/ac3x75.zip?dl=0 . This is a copy from Mojo web page, kasthuri15 ).

3-a. File -> Open Dojo folder, and specify the Dojo/Mojo-style file.

2-b. Prepare a stack of 2D EM images (tiff/png sequential files) and segmentation images (tiff/png sequential files).

3-b. File -> Import, and specify the stack of 2D EM images, the segmentation images, and a output mojo folder.

4. The message "please click here" appears if those files are successfully opened or imported. Plese click it, then the web-based dojo will launch for further editing ( http://www.rhoana.org/dojo/ ). Users can save/export the edited file through the small GUI (control panel). 

## A part of many unresolved problems:

1) Manual operation board (the bottom half of the small GUI) is under development.

2) Dojo accepts any size of 2D stack images, but unnecessary fringe appears if you do not import images with 512*n xy size.  

3) 3D viewer is buggy.

4) I have failed in importing the marching cubes module in the pyinstaller version.

5) In the pyinstaller version, developers have to manually move many files to appropriate folders (_web [$main.exe.link], _web/gtx [to dist/main/_web], _web/stl [to dist/main/_web], files in extra-dll [to dist/main], icons [to dist/main], Plugins [to dist/main]).

## Resolved problems:

180817) Solved. Asyncio now stops. It fully works on Python3.5.

It nearly works on Python3.5. But I do not know how to stop tornado.web.Application under asyncio.set_event_loop that is required by Python3 (tornado is provided in: DojoStandalone.py, stop signals are sent by wxMain/wxFileIO.py [TerminateDojo] and Filesystem/SaveChanges.py ). 


180817) The following mismatch occurs only on Python2.7.

The software package for Windows10/64bit provides limited functionality. This is due to unresolved miscommunication between pyinstaller and skimage (used for superpixelization and connected components). I will use CV2 instead in future.

https://github.com/pyinstaller/pyinstaller/issues/3473
 
https://stackoverflow.com/questions/50749124/pyinstaller-attributeerror-when-importing-packages-with-wildcards



180817) Resolved by use of offical pip numpy/scipy files and the copy of files in envs\py35\Lib\site-packages\scipy\extra-dll to dist/main.

Dojo_pyinstaller.zip ( https://www.dropbox.com/s/95wraf6qwgbp9jf/Dojo_pyinstaller_Ver3.zip?dl=0 ) is still large (300MB -> 120MB) even by use of the numpy without a very big MKL module.  



Hidetoshi Urakubo
2018/8/17

