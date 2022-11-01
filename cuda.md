# cuda 10.2


## driver delete

```
$ dpkg -l | grep -i nvidia
$ sudo apt-get purge nvidia*
$ sudo apt-get autoremove
$ sudo apt-get autoclean
```

## cuda delete
```
sudo apt-get --purge remove 'cuda*'
sudo apt-get autoremove --purge 'cuda*'
sudo rm -rf /usr/local/cuda*
```

## graphic driver install

### nouveau blacklist

```
$ lsmod | grep nouveau
$ sudo vi /etc/modprobe.d/blacklist-nouveau.conf
> blacklist nouveau
> options nouveau modset=0
$ sudo update-initramfs -u
$ reboot
```

## install cuda

### runfile(10.2) - recommanded

```
$ wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
$ sudo sh cuda_10.2.89_440.33.01_linux.run
$ vim ~/.bashrc
> export PATH=$PATH:/usr/local/cuda-10.2/bin
> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.2/lib64
> export CUDADIR=/usr/local/cuda-10.2
$ source ~/.bashrc
```

### deb(11.3)

```
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
$ sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget https://developer.download.nvidia.com/compute/cuda/11.3.0/local_installers/cuda-repo-ubuntu2004-11-3-local_11.3.0-465.19.01-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu2004-11-3-local_11.3.0-465.19.01-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-ubuntu2004-11-3-local/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get -y install cuda
#issue1
$ sudo apt-get remove --purge 'nvidia-.*'
```

### #issue1

```
remove nvidia driver 465 and install nvidia driver 470
$ sudo apt-get remove --purge 'nvidia-.*'
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ sudo ubuntu-drivers autoinstall
$ dpkg -l | grep -i nvidia
```

### install graphic driver

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

## install cudnn

### tar(8.0.2.39) - recommanded

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

### deb(8.2.0)

```
$ sudo dpkg -i libcudnn8_8.2.0.53-1+cuda11.3_amd64.deb
$ sudo dpkg -i libcudnn8-dev_8.2.0.53-1+cuda11.3_amd64.deb
$ sudo dpkg -i libcudnn8-samples_8.2.0.53-1+cuda11.3_amd64.deb

$ cd /usr/src/cudnn_samples_v8/mnistCUDNN/
$ sudo make clean && sudo make
$ ./mnistCUDNN
#issue1
```

### #issue1

```
$ cd /usr/include/
$ sudo vim cudnn.h
> driver_types.h --> <driver_types.h>
```