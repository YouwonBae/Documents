# tensorrRT 7.1.3.4


## cuda 10.2

## cuDNN 8.2.0

## pytorch 1.6.0

## opencv

## install tensorrRT 7.1.3.4

### tar - recommanded

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
> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/chlee/TensorRT-7.1.3.4/lib
$ source ~/.bashrc 
```

### deb

```
$ sudo dpkg -i nv-tensorrt-repo-ubuntu2004-cuda11.3-trt8.0.0.3-ea-20210423_1-1_amd64.deb
$ sudo apt-key add /var/nv-tensorrt-repo-ubuntu2004-cuda11.3-trt8.0.0.3-ea-20210423/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install tensorrt
$ sudo apt-get install python3-libnvinfer-dev

$ sudo apt-get install onnx-graphsurgeon

$ dpkg -l | grep TensorRT
```