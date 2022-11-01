# opencv


## 기존 opencv 삭제
```
$ sudo apt-get remove libopencv*
$ sudo apt-get autoremove
$ sudo find /usr/local/ -name "*opencv*" -exec rm {} \;
```

## install

### repo

```
sudo apt update
sudo apt install python3-opencv
```

### pip

```
pip3 install opencv-python
pip3 install opencv-contrib-python
```

### local(4.2.0) - recommanded

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install build-essential cmake unzip
$ sudo apt-get install pkg-config
$ sudo apt-get install libjpeg-dev libtiff5-dev libpng-dev libtiff-dev
$ sudo apt-get install ffmpeg libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev
$ sudo apt install libdc1394-22-dev
$ sudo apt-get install libv4l-dev v4l-utils
$ sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev 
$ sudo apt-get install libgtk-3-dev
$ sudo apt-get install mesa-utils libgl1-mesa-dri libgtkgl2.0-dev libgtk2.0-dev libgtkglext1-dev
$ sudo apt-get install libatlas-base-dev gfortran libeigen3-dev
$ sudo apt-get install python3-dev python3-numpy
$ sudo apt-get install python2.7-dev python-numpy
$ sudo apt-get install libopencv-*

$ mkdir opencv
$ cd opencv
$ wget -O opencv-4.2.0.zip https://github.com/opencv/opencv/archive/4.2.0.zip
$ wget -O opencv_contrib-4.2.0.zip https://github.com/opencv/opencv_contrib/archive
$ unzip opencv-4.2.0.zip
$ unzip opencv_contrib-4.2.0.zip

$ cd opencv
$ mkdir build
$ cd build

$ cmake \
-D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_TBB=OFF \
-D WITH_IPP=OFF \
-D WITH_1394=OFF \
-D BUILD_WITH_DEBUG_INFO=OFF \
-D BUILD_DOCS=OFF \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D BUILD_EXAMPLES=OFF \
-D BUILD_PACKAGE=OFF \
-D BUILD_TESTS=OFF \
-D BUILD_PERF_TESTS=OFF \
-D WITH_QT=OFF \
-D WITH_GTK=ON \
-D WITH_OPENGL=ON \
-D BUILD_opencv_python3=ON \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.2.0/modules \
-D WITH_V4L=ON \
-D WITH_FFMPEG=ON \
-D WITH_XINE=ON \
-D OPENCV_ENABLE_NONFREE=ON \
-D BUILD_NEW_PYTHON_SUPPORT=ON \
-D OPENCV_SKIP_PYTHON_LOADER=ON \
-D OPENCV_GENERATE_PKGCONFIG=ON \
../

$ cmake \
-D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_C_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D OPENCV_GENERATE_PKGCONFIG=ON \
-D WITH_GTK=ON \
-D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.2.0/modules \
-D BUILD_EXAMPLES=ON \
../

$ lscpu
$ make -j4
$ sudo make install
$ sudo ldconfig

$ pkg-config --modversion opencv4
```