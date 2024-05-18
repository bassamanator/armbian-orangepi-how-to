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

### Expected output

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

## Test the installation

```shell
 python3 -c "import wiringpi; help(wiringpi)"
```

### Expected output

```Python
Help on module wiringpi:

NAME
    wiringpi

DESCRIPTION
...
```

# Useful Aliases

```bash
# Live view of CPU core temperatures
alias wtemp='watch -n 1 "cat /sys/class/thermal/thermal_zone0/temp && cat /sys/class/thermal/thermal_zone1/temp && cat /sys/class/thermal/thermal_zone2/temp && cat /sys/class/thermal/thermal_zone3/temp"'

# Live view of CPU speed
alias wspeed='watch -n 1 "cat /sys/devices/system/cpu/cpufreq/policy0/scaling_cur_freq"'

# Live view of CPU speed and temperatures
alias wboard='watch -n 1 '\''echo "CPU Freq: $(cat /sys/devices/system/cpu/cpufreq/policy0/scaling_cur_freq)"; echo "CPU0: $(cat /sys/class/thermal/thermal_zone0/temp)"; echo "CPU1: $(cat /sys/class/thermal/thermal_zone1/temp)"; echo "CPU2: $(cat /sys/class/thermal/thermal_zone2/temp)"; echo "CPU3: $(cat /sys/class/thermal/thermal_zone3/temp)"'\'

```
