# coral tpu


## install

```
$ echo "deb https://packages.cloud.google.com/apt coral-edgetpu-stable main" | sudo tee /etc/apt/sources.list.d/coral-edgetpu.list
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get install libedgetpu1-std
$ sudo apt-get install libedgetpu1-max
$ sudo apt-get install python3-pycoral
```

## pycoral

```
$ mkdir coral && cd coral
$ git clone https://github.com/google-coral/pycoral.git
$ cd pycoral
$ bash examples/install_requirements.sh semantic_segmentation.py
```