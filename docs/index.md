# <img alt="OpenSK logo" src="images/OpenSK.svg" width="200px"><img alt="FIDO logo" src="images/FIDO_logo_black_RGB.png" style="margin: 0px 0px 40px 0px;" width="250px">
## Welcome to Feitian OpenSK USB Dongle

OpenSK was [announced](https://security.googleblog.com/2020/01/say-hello-to-opensk-fully-open-source.html "Say hello to OpenSK: a fully open-source security key implementation") by Google on January 30, 2020. It is a fully open-source FIDO security key implementation, include hardware and software.  

In that [announcement](https://security.googleblog.com/2020/01/say-hello-to-opensk-fully-open-source.html "Say hello to OpenSK: a fully open-source security key implementation"), Google said  
```
    By opening up OpenSK as a research platform, our hope is that 
    it will be used by researchers, security key manufacturers, 
    and enthusiasts to help develop innovative features and 
    accelerate security key adoption.
```
The firmware of OpenSK is developed in Rust and it implements both FIDO U2F and FIDO2 [specifications](https://fidoalliance.org/specs/fido2/fido-client-to-authenticator-protocol-v2.1-rd-20191217.html). These specifications are released by [FIDO Alliance](https://fidoalliance.org/ "FIDO Alliance"), which is an open industry association with a focused mission: authentication standards to help reduce the world’s over-reliance on passwords. FEITIAN is the Board Member.

To help and accelerate FIDO security key adoption, FEITIAN improves the housing and makes new designs of OpenSK USB Dongle, removes unused PCB components, public the design. Users can build firmware from the source code of [Google OpenSK github repository](https://github.com/google/opensk "OpenSK") without changing anything, provision it to this OpenSK hardware, to experience and try [FIDO](https://fidoalliance.org/ "FIDO Alliance") authentications.

Before you try to program firmware to OpenSK, please read the original [OpenSK guide](https://github.com/google/OpenSK) at first. The following documents are most like additional remarks.

### OpenSK Model
We have two models of OpenSK USB Dongle, V1 and V2. They are designed according to the [nRF52840 USB dongle](https://www.nordicsemi.com/Software-and-tools/Development-Kits/nRF52840-Dongle), which is used by Google OpenSK firmware. The difference between V1 and V2 is the method to enter bootloader mode.  

To OpenSK V1, user should insert a paper clip or a SIM-eject tool to the RESET button hole to enter bootloader mode. This is similar to user push the RESET button on the nRF52840 USB dongle.  

To OpenSK V2, after user connects the device to a computer, he should push and hold on to the user button for more than 8 seconds, then OpenSK will be in bootloader mode.  

For detailed information, please refer to the [hardware description page](./hardware.md).

## Programming firmware

### Pre-requisite

- The OpenSK USB Dongle V1 or V2.  
Before you program the firmware to OpenSK USB Dongle, you should switch it to bootloader mode. Please refer to the [Hardware Page](./hardware.md) to learn how to switch OpenSK to bootloader mode.
- Read the Original OpenSK guide.  
Before you perform the following operations, please read [OpenSK](https://github.com/google/opensk) and its [installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md) to learn how to customize your security key, for example, to change the signature counter mechanism and Attestation Certificate.
- Install [nrfutil](https://pypi.org/project/nrfutil/) tool.  
This tool allows you to directly flash firmware to OpenSK over USB without additional hardware.

### Development Environment and configuration
1. Prepare a Development environment.  
You should prepare a Development environment by yourself according to [this section](https://github.com/google/OpenSK/blob/master/docs/install.md#software).
2. Clone [Google OpenSK github repository](https://github.com/google/opensk "OpenSK").  
```
$ git clone --recursive https://github.com/google/OpenSK.git
```  

3. Initial setup.  
If you just cloned this repository, you need to run the following script:  

``` 
$ ./setup.sh
```  
For more information, please refer to the [Initial setup](https://github.com/google/OpenSK/blob/master/docs/install.md#initial-setup).  

4. Configure the OpenSK security parameter.  
Please follow the description to change the [Attestation Certificate](https://github.com/google/OpenSK/blob/master/docs/install.md#replacing-the-certificates) as you want. If you are not familiar with OpenSK and FIDO, we recommend you do not change anything.


### Flashing the firmware

Although you can download the firmware to our OpenSK V1 and V2 by using J-LINK as described in [OpenSK installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md), we recommend you program the firmware through the USB interface, it is more convenient.  

1. Switch OpenSK to bootloader mode.  
Please refer to [OpenSK Model](./index.md#opensk-model) or [hardware page](./hardware.md) to learn how to switch OpenSK to bootloader mode.  
The LEDs show different behavior in different mode. Please refer to the [hardware page](./hardware.md) to see LED status of OpenSK V1 and V2.
2. Program the OpenSK USB dongle.  
```
$ ./deploy.py --board=nrf52840_dongle_dfu --opensk --programmer=nordicdfu
```  
    When prompt   
```
Press [ENTER] when ready.  
```  
    Just press Enter, the firmware will be flashed to your OpenSK USB Dongle.    
    
    When the progress bar reaches 100%, OpenSK USB Dongle will be in working mode automatically. You can now test FIDO function.
!!! note "NOTE"
    If your dongle can not work well, please refer to https://github.com/google/OpenSK/pull/247 to erase the storage at first and then flash the firmware to try.
### Test FIDO functions  
Please refer to [Test Page](./test.md).  
