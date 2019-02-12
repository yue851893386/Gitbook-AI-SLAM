

# Process

- 2019-02-06->2019-02-08:
 try to build PTAM and its dependencies, however encounterred many compatible problems
- 2019-02-08: find a "PTAM with working dependencies" repo [egoist-sx/PTAM](https://github.com/egoist-sx/PTAM) in Github. Build PTAM successfully based on it, just a little modification.


# Source code

[yubaoliu/PTAM](https://github.com/yubaoliu/PTAM)

# Introduction
 PTAM (Parallel Tracking and Mapping) is a camera tracking system for augmented reality. It requires no markers, pre-made maps, known templates, or inertial sensors. If you're unfamiliar with PTAM have a look at some [videos](http://www.robots.ox.ac.uk/~gk/youtube.html) made with PTAM.


# Dependencies

- System: Ubuntu 16.04
- Refer [README](http://www.robots.ox.ac.uk/~gk/PTAM/README.txt) for INSTALLATION

The software has three principal dependencies:

The order of installation should be
1. TooN, 2. libCVD, 3. GVars3;:

save this file as dependent.sh

```sh
#!/bin/bash
sudo apt-get update
sudo apt-get install build-essential cmake pkg-config
sudo apt-get install libboost-dev libboost-doc
sudo apt-get install liblapack-dev libblas-dev
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev libv4l-dev
sudo apt-get install libavcodec-dev libavformat-dev libavutil-dev libpostproc-dev libswscale-dev libavdevice-dev libsdl-dev
sudo apt-get install libgtk2.0-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev
sudo apt-get install mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev freeglut3-dev

echo " Now pulling TooN..."
git clone git://github.com/edrosten/TooN.git
echo " TooN done for good!"

echo " Now pulling libcvd..."
git clone git://github.com/edrosten/libcvd.git
echo " libcvd done for good!"

echo " Now pulling gvars3..."
git clone git://github.com/edrosten/gvars.git
echo " gvars3 done for good!"

echo " All done."
```


## TooN
[TooN](http://savannah.nongnu.org/projects/toon/) (Tom’s Object-oriented numerics library) - a header library for linear algebra

```sh
git clone git clone https://git.savannah.nongnu.org/git/toon.git
./configure && make && sudo make install
make test
```

## libCVD
[libCVD](http://www.edwardrosten.com/cvd/) (computer vision library) - a library for image handling, video capture and computer vision

libcvd seems to be dependent on the following 3 libraries.

- lapack
- blas
- toon

From Synaptic Package Manager, search for the following packages:

- liblapack-dev
- libblas-dev

and install.

```sh
git clone https://github.com/edrosten/libcvd.git
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev libx11-dev libavformat-dev libavdevice-dev libavcodec-dev libavutil-dev libswresample-dev libglu-dev libdc1394-22
export CXXFLAGS=-D_REENTRANT
./configure --without-ffmpeg
make
sudo make install
```

Error Message:
```sh
yubao@yubao-Z370M-S01:~/Software/3rdPartyLibs/libcvd$ make
g++ -O3 -I. -I.  -INONE/include -D_REENTRANT -Wall -Wextra -pipe -std=c++14 -ggdb -fPIC -mmmx -msse -msse -msse2 -msse3 -c cvd_src/diskbuffer2.cc -o cvd_src/diskbuffer2.o -MMD -MP -MF cvd_src/diskbuffer2.d
In file included from ./cvd/image_ref.h:185:0,
                 from ./cvd/image.h:17,
                 from ./cvd/videoframe.h:13,
                 from ./cvd/localvideoframe.h:18,
                 from ./cvd/localvideobuffer.h:4,
                 from ./cvd/diskbuffer2.h:10,
                 from cvd_src/diskbuffer2.cc:2:
./cvd/internal/image_ref_implementation.hh: In member function ‘constexpr int& CVD::ImageRef::operator[](int)’:
./cvd/internal/image_ref_implementation.hh:194:1: error: expression ‘<throw-expression>’ is not a constant-expression
 }
 ^
./cvd/internal/image_ref_implementation.hh: In member function ‘constexpr int CVD::ImageRef::operator[](int) const’:
./cvd/internal/image_ref_implementation.hh:204:1: error: expression ‘<throw-expression>’ is not a constant-expression
 }
```

Solution:

The default C++ compiler on Ubuntu 16.04 will not compile libCVD.

```sh
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install g++-7
```

Now you can build libcvd with either:

```sh
CXX=g++-7 ./configure
make
```
or

```sh
mkdir build
cd build
CXX=g++-7 cmake -DCMAKE_BUILD_TYPE=Release ..
make
```

## GVars3
[Gvars3](http://www.edwardrosten.com/cvd/gvars3.html) (configuration system library) - a run-time configuration/scripting library, this is a
sub-project of libCVD.

> For GVars3, I recommend the following configure options:
> \# ./configure --disable-widgets --prefix=$HOME

```sh
sudo apt-get install libreadline6-dev

git clone https://github.com/edrosten/gvars.git
./configure CXXFLAGS=-std=c++14
make
sudo make install
```

## lib3ds

[Github-hoopoe/lib3ds](https://github.com/hoopoe/lib3ds)

```sh
git clone https://github.com/hoopoe/lib3ds.git
use cmake-gui
```


Make the libs work

```sudo ldconfig```



# Build PTAM

1. Copy the appropriate platform build files
```sh
cd PTAM
cp Build/Linux/* .
```
1. Edit the Makefile to reference custom include or linker paths
```sh
LINKFLAGS = -L /usr/local/lib -lGvars3 -lcvd -lGLU -lGL -llapack
```


## INSTALLATION


# References
- [Parallel Tracking and Mapping for Small AR Workspaces - Source Code](http://www.robots.ox.ac.uk/~gk/PTAM/)
- [libcvd API Doc](https://codedocs.xyz/edrosten/libcvd/)
- [ROS-PTAM](http://wiki.ros.org/ptam)
- [windows下PTAM的编译](https://blog.csdn.net/cgf_909/article/details/24457771)
- [PTAM Compilation on Linux-HowTo](http://hustcalm.me/blog/2013/09/27/ptam-compilation-on-linux-howto/)
