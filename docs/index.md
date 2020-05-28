# <img alt="OpenSK logo" src="images/OpenSK.svg" width="200px">
## Welcome to OpenSK USB Dongle

OpenSK was [announced](https://security.googleblog.com/2020/01/say-hello-to-opensk-fully-open-source.html "Say hello to OpenSK: a fully open-source security key implementation") by Google at January 30, 2020. It is a fully open-source FIDO security key implementation, include hardware and software.  
In this [**announcement**](https://security.googleblog.com/2020/01/say-hello-to-opensk-fully-open-source.html "Say hello to OpenSK: a fully open-source security key implementation"), Google said  
```
    By opening up OpenSK as a research platform, our hope is that 
    it will be used by researchers, security key manufacturers, 
    and enthusiasts to help develop innovative features and 
    accelerate security key adoption.
```
The firmware of OpenSK is developed in Rust and it implements both FIDO U2F and FIDO2 [specifications](https://fidoalliance.org/specs/fido2/fido-client-to-authenticator-protocol-v2.1-rd-20191217.html). These specifications are released by [FIDO Alliance](https://fidoalliance.org/ "FIDO Alliance"), which is an open industry association with a focused mission: authentication standards to help reduce the world’s over-reliance on passwords. FEITIAN is the Board Member.

To help and accelerate FIDO security key adoption, FEITIAN improves the housing and makes new design of OpenSK USB Dongle, remove unused PCB components, public the design. Users can build firmware from source code of [Google OpenSK github repository](https://github.com/google/opensk "OpenSK") without changing anything, provision it to this OpenSK hardware, to experence and try [FIDO](https://fidoalliance.org/ "FIDO Alliance") authentications.

Before you try to program firmware to OpenSK, please read original [OpenSK guide](https://github.com/google/OpenSK) at first. The following documents are most like additional remarks.

### OpenSK Model
We have two model of OpenSK USB Dongle, V1 and V2. They are designed according to [nRF52840 USB dongle](https://www.nordicsemi.com/Software-and-tools/Development-Kits/nRF52840-Dongle), which is used by Google OpenSK firmware. The difference between V1 and V2 is the method to Trigger DFU mode after connect it to USB port.   

To OpenSK V1, user should insert a paper clip or a SIM-eject tool to the RESET button hole to switch it to DFU mode. This is similar as user push the RESET button on nRF52840 USB dongle.  

To OpenSK V2, after user connect the device to computer, he should push and hold on the user button for more 8 seconds, then OpenSK will be in DFU mode.  

For detailed informations, please refer to [hardware description page](./hardware.md).

## Programming firmware

### Pre-requisite

- The OpenSK USB Dongle V1 or V2.  
Before you program the firmware to OpenSK USB Dongle, you should switch it to DFU mode. Please refer to [Harware Page](./hardware.md) to learn how to switch OpenSK to DFU mode.
- Read Original OpenSK guide.  
Before you perform following opertaions, please read [OpenSK](https://github.com/google/opensk) and its [installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md) to learn how to customize your security key, for example, to change the signature counter mechnisam and Attestation Certificate.

### Develop Environment and configuration
1. Prepare develop environment.  
You should prepare developing environment by yourself according to [this section](https://github.com/google/OpenSK/blob/master/docs/install.md#software).
2. Clone [Google OpenSK github repository](https://github.com/google/opensk "OpenSK").  
    ```
    $ git clone --recursive https://github.com/google/OpenSK.git
    ```

3. Initial setup.  
If you just cloned this repository, you need to run the following script:  
    ``` 
        $ ./setup.sh
    ```  
For more information, please refer to [Initial setup](https://github.com/google/OpenSK/blob/master/docs/install.md#initial-setup).  

4. Configure the OpenSK security parameter.  
Please follow the description to change [Attestation Certificate](https://github.com/google/OpenSK/blob/master/docs/install.md#replacing-the-certificates) as you want. If you are not familar with OpenSK and FIDO, we recommend you do not change anything.

### LED status
The LEDs show different behaviour in DFU mode and working mode.

##### OpenSK V1
| LED behaviour |  Mode type | Triger Method |
| :-- | :-- | :-- |
| Blue LED is breathing | DFU mode | Use a paper clip or a SIM-eject tool to push RESET button in RESET button hole |
| Blue LED is flashing | DFU mode | Flashing the firmware |
| No LED on | Working mode | Idle |
| R/G/B LED is flashing | Working mode | Wait for user presence when receiving FIDO command |

##### OpenSK V2
| LED behaviour |  Mode type | Triger Method |
| :-- | :-- | :-- |
| Red LED is breathing | DFU mode | Use a paper clip or a SIM-eject tool to push RESET button in RESET button hole |
| Red LED is flashing | DFU mode | Flashing the firmware |
| No LED on | Working mode | Idle |
| R/G/B LED is flashing | Working mode | Wait for user presence when receiving FIDO command |

### Flashing the firmware

Although you can download the firmware to our OpenSK V1 and V2 by using J-LINK as described in [OpenSK installation guide](https://github.com/google/OpenSK/blob/master/docs/install.md), we recommend you program the firmware through USB interface, it is more convenient.  

1. Switch OpenSK to DFU mode.  
Please refer to [OpenSK Model](./index.md#opensk-model) or [hardware description page](./hardware.md) to learn how to switch OpenSK to DFU mode.  
The LEDs show different behaviour in differet mode. Please refer to [LED status](./hardware.md#LED) .
2. Program the OpenSK USB dongle.  
    ```
    $ ./deploy.py --board=nrf52840_dongle_dfu --opensk --programmer=nordicdfu
    ```  
    When prompt   
    ```
    Press [ENTER] when ready.  
    ```  
    Just press Enter, the firmware will be flahsed to your OpenSK USB Dongle.  

3. Lock the working mode.  
    ```
    $ ./deploy.py --board=nrf52840_dongle_dfu --programmer=nordicdfu --no-app --dont-clear-apps
    ```  
    When prompt   
    ```
    Press [ENTER] when ready.  
    ```  
    Please press Enter and wait for the progress bar to be end.

    Without Step 3, your USB Dongle will return to DFU mode when you remove and reinsert it. This step just locks the working mode unless you do Step 1 to swith it to DFU mode again.

!!! note "NOTE"
    1. Step 2 and Step 3 are learned from [this discussion](https://github.com/google/OpenSK/issues/81 "Flash USB dongle without additional hardware"). The steps may change in the future.
    2. Above commands are examples on macOS. If you use Linux and Windows, there may be some difference.

### Test FIDO functions  
Please refer to [Test Page](./test.md).  
