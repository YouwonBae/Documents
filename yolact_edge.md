# YOLACT_EDGE

## cuda 10.2
### driver delete
```
$ dpkg -l | grep -i nvidia
$ sudo apt-get purge nvidia*
$ sudo apt-get autoremove
$ sudo apt-get autoclean
```
### cuda delete
```
sudo apt-get --purge remove 'cuda*'
sudo apt-get autoremove --purge 'cuda*'
sudo rm -rf /usr/local/cuda*
```

### graphic driver install
#### nouveau blacklist
```
$ lsmod | grep nouveau
$ sudo vi /etc/modprobe.d/blacklist-nouveau.conf
> blacklist nouveau
> options nouveau modset=0
$ sudo update-initramfs -u
$ reboot
```
#### install graphic driver
```
ctrl+alt+F4
$ sudo service gdm stop
$ ubuntu-drivers devices
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ sudo ubuntu-drivers autoinstall
$ reboot
$ nvidia-smi
```
### install cuda
#### runfile(recommanded 10.2)
```
$ wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
$ sudo sh cuda_10.2.89_440.33.01_linux.run
$ vim ~/.bashrc
> export PATH=$PATH:/usr/local/cuda-10.2/bin
> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.2/lib64
> export CUDADIR=/usr/local/cuda-10.2
$ source ~/.bashrc
```

## install cudnn
tar(recommanded 8.0.2.39)
```
$ cd Download
$ tar xvzf cudnn-10.2-linux-x64-v8.0.2.39.tgz

$ sudo cp cuda/include/cudnn* /usr/local/cuda-10.2/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda-10.2/lib64

$ sudo chmod a+r /usr/local/cuda-10.2/include/cudnn.h /usr/local/cuda-10.2/lib64/libcudnn*

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8

$ sudo ln -sf /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn.so.8.0.2 /usr/local/cuda-10.2/targets/x86_64-linux/lib/libcudnn.so.8

$ sudo ldconfig

$ ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn
$ cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2
```

## conda
### install
```
https://www.anaconda.com/products/individual

download: Anaconda3-2021.11-Linux-x86_64.sh

$ cd Downloads

$ sha256sum Anaconda3-2021.11-Linux-x86_64.sh

$ bash Anaconda3-2021.11-Linux-x86_64.sh

$ vim ~/.bashrc
> export PATH=~/anaconda3/bin:~/anaconda3/condabin:$PATH

$ source ~/.bashrc

$ conda update conda

$ conda update anaconda

$ conda install python=3.8
```
### use
```
$ conda env list 
: 가상환경 목록 보기

$ conda create -n <가상환경이름> python=<버젼> 
: 가상환경 생성 
ex) conda create -n TestEnv python=3.7

$ conda env remove -n <가상환경이름> 
: 가상환경 삭제

$ conda activate <가상환경이름> 
: 가상환경 실행

$ conda deactivate 
: 가상환경 종료

$ conda list 
: 현재 가상환경에서 설치되어있는 패키지 보기

$ conda install <패키지 이름> 
: 현재 가상환경에서 패키지 설치
ex1) conda install numpy
ex2) conda install numpy pandas
ex3) conda install tensorflow-gpu==1.13.1

$ conda uninstall <패키지 이름> 
: 현재 가상환경에서 패키지 삭제

$ conda create --name <복사하여 생성할 가상환경명> --clone <복사할 가상환경명>
ex) conda create --name NewProject --clone OldProject : OldProject를 복사하여 NewProject로 생성함

$ conda env create --file <yml파일명.yml or yaml> 
: yml/yaml로 가상환경 생성
ex) conda env create --file environment.yml

$ conda env update --file <yml파일명.yml or yaml> --prune 
: yml 덮어쓰기 (activate상태에서 사용가능)
ex) conda env update --file environment.yml --prune

$ conda env create -f <yml파일명.yaml or yaml> , conda env export > <yml파일명.yml> 
: 현재 가상환경의 yml 생성
ex) conda env create -f environment.yml
ex) conda env export > environment.yaml
```

## opencv_4.2.0
### 기존 opencv 삭제
```
$ sudo apt-get remove libopencv*
$ sudo apt-get autoremove
$ sudo find /usr/local/ -name "*opencv*" -exec rm {} \;
```
### install
#### local(4.2.0)
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

## Pytorch 1.6.0
### conda(recommanded)
```
$ conda install pytorch==1.6.0 torchvision==0.7.0 cudatoolkit=10.2 -c pytorch
$ python
> import torch
> print(torch.cuda.is_available())
```

## tensorrRT 7.1.3.4
> cuda 10.2
cuDNN 8.0.2.39
pytorch 1.6.0
opencv 4.2.0
install tensorrRT 7.1.3.4

### tar(recommanded)
```
download "TensorRT-7.1.3.4.Ubuntu-18.04.x86_64-gnu.cuda-10.2.cudnn8.0.tar.gz"
$ cd home
$ tar -xvzf TensorRT-7.1.3.4.Ubuntu-18.04.x86_64-gnu.cuda-10.2.cudnn8.0.tar.gz

$ cd TensorRT-7.1.3.4/python
$ pip3 install tensorrt-7.1.3.4-cp37-none-linux_x86_64.whl

$ cd TensorRT-7.1.3.4/uff
$ pip3 install uff-0.6.9-py2.py3-none-any.whl

$ cd TensorRT-7.1.3.4/graphsurgeon
$ pip3 install graphsurgeon-0.4.5-py2.py3-none-any.whl

$ cd TensorRT-7.1.3.4/onnx_graphsurgeon
$ python3 -m pip install 

$ vim ~/.bashrc
> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/maze/TensorRT-7.1.3.4/lib
$ source ~/.bashrc 
```

## torch2trt
### install(conda env)
```
$ git clone https://github.com/NVIDIA-AI-IOT/torch2trt
$ cd torch2trt
$ vim setup.py
> def trt_inc_dir():
>     return "/home/maze/TensorRT-7.1.3.4/include"
> def trt_lib_dir():
>     return "/home/maze/TensorRT-7.1.3.4/lib"
$ python setup.py install --plugins
```

## Yolact_Edge
### Install some other packages
```
$ pip3 install --target=/home/maze/anaconda3/envs/yolact/lib/python3.8/site-packages cython
$ pip3 install --target=/home/maze/anaconda3/envs/yolact/lib/python3.8/site-packages opencv-python pillow matplotlib
$ pip3 install --target=/home/maze/anaconda3/envs/yolact/lib/python3.8/site-packages git+https://github.com/haotian-liu/cocoapi.git#"egg=pycocotools&subdirectory=PythonAPI"
$ pip3 install --target=/home/maze/anaconda3/envs/yolact/lib/python3.8/site-packages GitPython termcolor tensorboard
```
### git clone
```
git clone https://github.com/haotian-liu/yolact_edge.git
cd yolact_edge
```
### inference
#### calib img
```
./data
├── coco
│   ├── annotations
│   ├── calib_images
│   └── images
├── FlyingChairs
│   ├── data
│   └── train_val.txt
└── YoutubeVIS
    ├── annotations
    ├── calib_images
    ├── JPEGImages
    └── train_all_frames
        └── JPEGImages
```
#### inferencing

##### directory
```
eval.py
my_image.png
weights
└── yolact_edge_54_800000.pth
data
└── coco
    ├── annotations
    ├── calib_images
    └── images
```
##### image
```
$ python eval.py --trained_model=weights/yolact_edge_54_800000.pth --score_threshold=0.3 --top_k=100 --image=my_image.png
```
##### cam
```
$ python eval.py --trained_model=weights/yolact_edge_54_800000.pth --score_threshold=0.3 --top_k=100 --video_multiframe=2 --trt_batch_size 2 --video=0
```
