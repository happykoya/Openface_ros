# Intel Realsense OpenFace for ROS 

![OS](https://img.shields.io/badge/OS-Ubuntu_18.04-orange.svg) ![ROS_2](https://img.shields.io/badge/ROS-Melodic-brightgreen.svg) ![OPENFACE](https://img.shields.io/badge/OpenFace-2.2-lightgrey.svg)


This repository contains a ROS wrapper for [OpenFace](https://github.com/TadasBaltrusaitis/OpenFace), which allows to extract the following information from an RGB-D Stream.
- 2D/3D Facial Landmarks
- Head Pose and Orientation 
- 2D/3D Eye Landmarks
- Gaze
- Action Units



The software expects [ HIRO-group  Lab's fork of OpenFace](https://github.com/HIRO-group/openface_ros), it is easy to customize to any  platform that shares similar hardware features.


### Prerequisites

#### System Dependencies

This repository needs `openface` and `realsense`. To install, compile and test openface package, please refer to the [installation tutorial](https://github.com/TadasBaltrusaitis/OpenFace/wiki) in openface github wiki page. Also, for realsense package, please refer to the [installation tutorial](https://github.com/IntelRealSense/realsense-ros) in realsense github page.
#### Hardware
   *  [Intel® RealSense™ Depth Camera D415](https://www.intelrealsense.com/depth-camera-d415/)
#### Software   
   * [Ubuntu 18.04.4 LTS (Bionic Beaver)](https://releases.ubuntu.com/18.04/)

#### ROS Dependencies

This repository supports `ROS Melodic`. [Here](http://wiki.ros.org/melodic)'s a recently guide on how to install ROS.

##### Catkin Tools

We use the new Catkin Command Line Tools `catkin_tools`, a Python package that provides command line tools for working with the catkin meta build system and catkin workspaces. The following instructions apply to this new package, even though the repository can be used and compile with the old `catkin_make` without issues.

```sh
sudo apt-get install python-catkin-tools
```


## Installation

Guide for installing, compiling and testing the openface_ros package in your ROS environment.


```sh
sudo apt-get -y update

sudo apt-get -y install build-essential
sudo apt-get -y install gcc-8 g++-8

sudo apt-get -y install cmake

sudo apt-get -y install zip
sudo apt-get -y install libopenblas-dev liblapack-dev
sudo apt-get -y install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev
sudo apt-get -y install libtbb2 libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev


#Downloading and Installing OpenCV...

wget https://github.com/opencv/opencv/archive/4.1.0.zip
unzip 4.1.0.zip
cd opencv-4.1.0
mkdir -p build

cd bcmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_CUDA=OFF -D BUILD_SHARED_LIBS=OFF ..
make -j4
sudo make install
sudo ldconfig

cd ../..
rm 4.1.0.zip
sudo rm -r opencv-4.1.0uild

# dlib dependecy /  Installing dlib
wget http://dlib.net/files/dlib-19.13.tar.bz2;
tar xf dlib-19.13.tar.bz2;
cd dlib-19.13;
mkdir -p build;
cd build;

cmake ..;
cmake --build . --config Release;
sudo make install;
sudo ldconfig;
cd ../..;    
rm -r dlib-19.13.tar.bz2 

# OpenFace installation

mkdir -p build
cd build
cmake -D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D CMAKE_BUILD_TYPE=RELEASE ..
make
cd ..

```


 
# Setting up


Assuming your project is in a folder named "catkin_ws" on your home Directory.

```sh
source /opt/ros/melodic/setup.bash

mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make clean

cd src/ 
git clone https://github.com/HIRO-group/openface_ros

cd ..

catkin_make 

```



### Execution 

#### Initial steps 

 1. Connect Realsense camera with USB 3.0 port in your computer.


#### How to run this package

After cloning and building the repo, you can run the commands below.

```sh
roslaunch openface_ros openface_ros.launch
rosrun openface_ros openface_realsense
```



## License
This project is licensed under [BSD 3-Clause License](LICENSE).

You have to respect OpenFace, dlib, and OpenCV licenses, together with licenses of the datasets used for OpenFace model training.
