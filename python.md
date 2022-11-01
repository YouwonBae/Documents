# python

## configure
```
$ ls /usr/bin/ | grep python
```

## install
```
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt install python[version]
ex) sudo apt install python3.7
ex) sudo apt install python3.8
```

## version select
```
$ sudo update-alternatives --config python
```

## alternative add
### ex)
```
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
```
