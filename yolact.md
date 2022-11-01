# YOLACT

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
$ nvcc -V
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

$ source ~/.bashrc

$ conda update conda

$ conda update anaconda

$ conda install python=3.7
```

## Yolact
### anaconda3
```
$ git clone https://github.com/haotian-liu/yolact_edge.git
$ cd yolact_edge
$ conda env create -f environment.yml

> name: yolact-env
> 
> channels:
>   - conda-forge
>   - defaults
> dependencies:
>  - python==3.7
>  - pip
>  - cython
>  - matplotlib
>  - pip:
>    - opencv-python 
>    - pillow <7.0 # bug PILLOW_VERSION in torchvision, must be < 7.0 until torchvision is upgraded
>    - pycocotools 
>    - PyQt5 # needed on KDE/Qt envs for matplotlib

$ conda install pytorch==1.6.0 torchvision==0.7.0 cudatoolkit=10.2 -c pytorch
$ sudo reboot now # essential
$ pip install scikit-image
$ pip install filterpy
```

### local
```
$ git clone https://github.com/haotian-liu/yolact_edge.git
$ cd yolact_edge

$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
$ sudo update-alternatives --config python3
> python==3.6.9

$ pip install torch==1.6.0 torchvision==0.7.0
$ pip install cython
$ pip install opencv-python pillow pycocotools matplotlib
$ pip install scikit-image
$ pip install filterpy
```
