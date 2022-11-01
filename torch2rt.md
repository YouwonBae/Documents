# torch2trt


## install(conda env)

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