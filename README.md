# Armbian Orange Pi Zero 2W

1. Download your preferred image from [Armbian](https://www.armbian.com/orange-pi-zero-2w/).
2. Burn the image onto a microSD card using something like [USBImager](https://bztsrc.gitlab.io/usbimager/).

## Wireless setup

I will be doing a headless setup. Armbian lets you `PRESET` certain things, you can find the full list [here](https://github.com/armbian/build/blob/66b0171516297ced0b0fead62c2f2763627176e5/extensions/preset-firstrun.sh).

1. On your microSD card, create a file named `/root/.not_logged_in_yet`.
2. You **must** adjust the following to your needs:

```
PRESET_NET_CHANGE_DEFAULTS=1
PRESET_NET_WIFI_ENABLED=1
PRESET_NET_WIFI_SSID='Wifi network name'
PRESET_NET_WIFI_KEY='Wifi password'
PRESET_NET_WIFI_COUNTRYCODE='CA'
PRESET_CONNECT_WIRELESS=n
SET_LANG_BASED_ON_LOCATION=n
PRESET_TIMEZONE=America/Toronto # Find via web search or type `timedatectl list-timezones` in a linux terminal
PRESET_ROOT_PASSWORD=tester123
PRESET_USER_NAME=opi # Add new user
PRESET_USER_PASSWORD=tester123
PRESET_DEFAULT_REALNAME='Orange Pi'
```

3. Boot the device with the microSD card.
4. Wait 3-4 minutes for the first boot, then you can `SSH` into the device.

# GPIO

To be able to use the GPIO pins, certain packages must be installed.

## wiringOP

Original instructions [source](http://www.orangepi.org/orangepiwiki/index.php/Orange_Pi_Zero_2W#How_to_install_wiringOP).

### Clone the repo

```shell
cd ~
sudo apt update && sudo apt install git
git clone https://github.com/orangepi-xunlong/wiringOP.git -b next
```

### Compile and install wiringOP

```shell
cd wiringOP
sudo ./build clean
sudo ./build
```

### Test the installation

```shell
gpio readall
```

#### Expected output

## wiringOP-Python

Original instructions [source](http://www.orangepi.org/orangepiwiki/index.php/Orange_Pi_Zero_2W#How_to_install_wiringOP).

### Install packages

```shell
sudo apt install swig python3-dev python3-setuptools
```

### Ready the repo

```shell
cd ~
git clone --recursive https://github.com/orangepi-xunlong/wiringOP-Python -b next
cd wiringOP-Python
git submodule update --init --remote
```

### Compile and install

```shell
python3 generate-bindings.py > bindings.i
sudo python3 setup.py install
```

### Test the installation

```shell
 python3 -c "import wiringpi; help(wiringpi)"
```

#### Expected output

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

# Sources

- [Armbian](https://)
- [wiringOP](https://)
- [wiringOP](https://)
- [wiringOP](https://)
