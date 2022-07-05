# Official Way -- Command Line Tool

## Background
This way is mentioned officially by [Google OpenSK GitHub pages](https://github.com/google/opensk) and [installation guide](https://github.com/google/OpenSK/blob/stable/docs/install.md).
Before you try to program firmware to OpenSK, please read the original [OpenSK guide](https://github.com/google/OpenSK) at first.  
By using this way, you should install develop environment, such as python, rust, nrfutil, openssl and etc, clone the source code and build the project. Then use command line to download the firmware.  
The following documents are most like additional remarks.

## Pre-requisite

- The OpenSK USB Dongle V1 or V2.  
During the programming, you may need to switch OpenSK USB Dongle to ^^**==bootloader==**^^ mode. Please refer to the [Hardware Page](./hardware.md) to learn how to switch OpenSK to ^^**==bootloader==**^^ mode. You can check to make sure it is in bootloader according to [this section](./hardware#check-bootloader-mode) .
- Read the Original OpenSK guide.  
Before you perform the following operations, please read original [OpenSK](https://github.com/google/opensk) and its [installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md) to learn how to customize your security key, for example, to change the signature counter mechanism and Attestation Certificate.
- Install [nrfutil](https://pypi.org/project/nrfutil/) tool. (```sudo pip3 install nrfutil``` or ```sudo pip3 install nrfutil --user```)  
This tool allows you to directly flash firmware to OpenSK over USB without additional hardware.  
Please find right version nrfutil and python. Make sure you have noted that nrfutil 6.x requires: Python ==>=3.6, <3.9== .
- Apply udev rule (Linux only).  
If you are using Linux, you should add a udev rule to make OpenSK work well with FIDO applications and browsers.
```
sudo cp rules.d/55-opensk.rules /etc/udev/rules.d/
sudo udevadm control --reload
```
Then unplug and replug the key for the rule to trigger.

- Development Environment and configuration  
You should prepare a Development environment by yourself according to [this section](https://github.com/google/OpenSK/blob/master/docs/install.md#software).

## Firmware build and update
### 1. Build firmware
The command and scripts showed below have been tested on **Linux** and **macOS**. We haven't tested them on Windows and other platforms.  

- Clone [Google OpenSK Github repository](https://github.com/google/opensk "OpenSK").  
```
$ git clone --recursive https://github.com/google/OpenSK.git
```  

- Initial setup.  
If you just cloned this repository, you need to run the following script:  
``` 
$ ./setup.sh
```  
For more information, please refer to the [Initial setup](https://github.com/google/OpenSK/blob/master/docs/install.md#initial-setup).  

- Configure the OpenSK security parameter.  
Please follow the description to change the [Attestation Certificate](https://github.com/google/OpenSK/blob/master/docs/install.md#replacing-the-certificates) as you want. If you are not familiar with OpenSK and FIDO, we recommend you do not change anything.

### 2. Flash firmware

Although you can download the firmware to our OpenSK V1 and V2 by using J-LINK as described in [OpenSK installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md), we recommend you program the firmware through the USB interface, it is more convenient.  

- Switch OpenSK to bootloader mode.  
Please refer to [OpenSK Model](./index.md#opensk-model) or [hardware page](./hardware.md) to learn how to switch OpenSK to bootloader mode.  
The LEDs show different behavior in different mode. Please refer to the [hardware page](./hardware.md) to see LED status of OpenSK V1 and V2.
2. Program the OpenSK USB dongle.  
!!! note "NOTE"
    If your USB dongle can not work well, you can erase the storage at first.
    ```
    ./deploy.py --board=nrf52840_dongle_dfu --programmer=nordicdfu --erase_storage
    ```
    After this command, you should switch your OpenSK to bootloader mode again to perform following operations.


```
$ ./deploy.py --board=nrf52840_dongle_dfu --programmer=nordicdfu --opensk
```  
    When prompt   
```
Press [ENTER] when ready.  
```  
    Just press Enter, the firmware will be flashed to your OpenSK USB Dongle.   
When the progress bar reaches 100%, OpenSK USB Dongle will be in working mode automatically.   

!!! note "Linux"
    If ```deploy.py``` returns error "==Permission denied: /dev/ttyxxxx==",   
    please change access permission of this device ```sudo chmod 666 /dev/ttyxxxx```


Please provision Attestation Certificate and Private Key before you test your OpenSK.


### 3. Configure Attestation Certificate and Private Key
You need to inject the cryptographic material if you enabled batch attestation or CTAP1/U2F compatibility (which is the case by default), otherwise, it can not work well.
```
./tools/configure.py \
    --certificate=crypto_data/opensk_cert.pem \
    --private-key=crypto_data/opensk.key
```
!!! warning "WARNING"
    When you add a security to Google services, you may encount problem because OpenSK uses self attestation. So plesae click "Skip" when Chrome prompts "allow this site to see your security key? google.com wants to see the make and model of your security key."
    
Now you can test your OpenSK according to [Test Page](./test.md).  
