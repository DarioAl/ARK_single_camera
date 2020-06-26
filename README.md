# KilobotArena
## Augmented Reality for Kilobots (ARK)
### Installation

A GUI for running experiments using Kilobot Smart Arena with four tracking cameras

Ubuntu is the preferred OS for ARK

KilobotArena is a Qt program, and therefore uses the Qt build tools to generate the make file. There are two ways to do this - in both cases you need a recent version of Qt [v.5.6+](www.qt.io) installed - on Ubuntu the version in aptitude should do (`sudo apt-get install qtcreator` should install everything from Qt that you need).

You also need a CUDA supporting version of OpenCV 3 - you'll need to compile this yourself - here's a [guide](https://gist.github.com/filitchp/5645d5eebfefe374218fa2cbf89189aa) that should work. 

Now either use the QtCreator gui you installed in the previous step (click the hammer button to build - it will prompt you to choose), or run `qmake` in the ARK directory to generate the Makefile. There are lots of online guides to help if you have trouble [e.g.](http://doc.qt.io/qtcreator/creator-building-targets.html)

QtCreator will run the Makefile for you - from the command line you'll have to do it yourself. If you get build errors you may need to change the path to OpenCV in the .pro file (the syntax is quite simple).

You also need to install the calibration program to generate calibrated camera maps: [KilobotArenaCalibration](https://github.com/DiODeProject/KilobotArenaCalibration).

### Citation

If you use or adapt ARK in order to generate experimental results, please cite the following paper in any resulting publications:

* Reina A., Cope A.J., Nikolaidis E., Marshall J.A.R., Sabo C. (2017) ARK: Augmented reality for Kilobots. *IEEE Robotics and Automation Letters* **2, 1755-1761**.

### See Also

* ARK makes use of a redesigned overhead controller: [ARK_OHC](https://github.com/DiODeProject/ARK_OHC)
* [Kilobot Wiki](http://diode.group.shef.ac.uk/kilobots/index.php/Kilobots)

### UBUNTU 18 installation random notes
CUDA can be installed from the official repo (online installation is best) just be carefull to call the correct version of cuda-* instead of simply cuda. 
WARNING: Do not install CUDA 11 since it is not working with opencv 3

Follow Vanders guide https://github.com/vanderfreitas/KilobotArenato install OpenCV3.4.1 (I had issues with 3.4.5 and PvAPI) or follow this guide and be sure to add:
-D BUILD_opencv_cudacodec=OFF 
-D WITH_PVAPI=ON
-D PVAPI_LIBRARY="/usr/local/lib/libPvAPI.a"
when running cmake

#### As for Vander notes, follow these steps to have the mako camera working properly with opencv:
We are using a AV Mako camera, then we have to include its support in the OpenCV installation. Go directly to the OpenCV setup this is not your case.
We use the AVT Gige SDK for the camera. The new VIMBA SDK replaced the AVT Gige, but the OpenCV version we are using does not support it yet.
We followed the steps from this link: https://github.com/sightmachine/SimpleCV/wiki/Allied-Vision-(AVT)-GigE-Camera-Installation-Guide-for-Ubuntu-Linux

Download the SDK "PvAPI SDK for Linux v1.28" from: https://www.alliedvision.com/en/support/software-downloads.html
Choose: "Legacy Software (SDKs, apps, adapters, and interfaces)"
Unzip it at /opt with writing permission and:

cd AVT\ GigE\ SDK/inc-pc
sudo cp * /usr/local/include/

cd ../lib-pc/x64/4.4
sudo cp * /usr/local/lib/
cd ../../../bin-pc/x64
sudo cp *.so /usr/local/lib/
sudo cp SampleViewer CLIpConfig /usr/bin

Open the /etc/ld.so.conf file:
sudo nano /etc/ld.so.conf
Add the following line in the opened file:
/usr/local/lib


sudo ldconfig
sudo apt-get install libjpeg62
