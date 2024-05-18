# Aarmbian Orange Pi Zero 2W

# wiringOP

Original instructions [source](http://www.orangepi.org/orangepiwiki/index.php/Orange_Pi_Zero_2W#How_to_install_wiringOP).

## Clone the repo

```shell
cd ~
sudo apt update && sudo apt install git
git clone https://github.com/orangepi-xunlong/wiringOP.git -b next
```

## Compile and install wiringOP

```shell
cd wiringOP
sudo ./build clean
sudo ./build
```

## Test the installation

```shell
gpio readall
```

Expected output:

# wiringOP-Python

Original instructions [source](http://www.orangepi.org/orangepiwiki/index.php/Orange_Pi_Zero_2W#How_to_install_wiringOP).

## Install packages

```shell
sudo apt install swig python3-dev python3-setuptools
```

## Ready the repo

```shell
cd ~
git clone --recursive https://github.com/orangepi-xunlong/wiringOP-Python -b next
cd wiringOP-Python
git submodule update --init --remote
```

## Compile and install

```shell
python3 generate-bindings.py > bindings.i
sudo python3 setup.py install
```
