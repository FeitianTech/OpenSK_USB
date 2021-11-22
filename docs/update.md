## OpenSK Model
We have two models of OpenSK USB Dongle, V1 and V2. They are designed according to the [nRF52840 USB dongle](https://www.nordicsemi.com/Software-and-tools/Development-Kits/nRF52840-Dongle), which is used by Google OpenSK firmware. The difference between V1 and V2 is the method to enter bootloader mode.  

To OpenSK V1, user should insert a paper clip or a SIM-eject tool to the RESET button hole to enter bootloader mode. This is similar to user push the RESET button on the nRF52840 USB dongle.  

To OpenSK V2, after user connects the device to a computer, he should push and hold on to the user button for more than 10 seconds, then OpenSK will be in bootloader mode.  

For detailed information, please refer to the [hardware description page](./hardware.md).

## Firmware Update
There are two ways to update firmware of OpenSK USB dongle.   
One way is to follow the steps listed on official OpenSK github pages.  
The other way is to use GUI Tool develop by Feitian Technologies.  

### 1. Official Way -- Command Line Tool
This way is mentioned officially by [Google OpenSK GitHub pages](https://github.com/google/opensk).  
By using this way, you should install develop environment, such as python, rust, nrfutil, openssl and etc, clone the source code and build the project. Then use command line to download the firmware.  
Please refer to [Official Way to update firmware](./originalway.md) to learn details.

### 2. Feitian GUI Tool
It is very hard for end user to setup the develop environment, install required tools, build from the source code. To facilitate people who are not familiar with software development, Feitian developed a GUI tool for any user to simply download the firmware.  
Please refer to [Feitian GUI tool](./feitianguiway.md) to find the detailed instruction.

## Test FIDO functions  
After you update the firmware, please refer to [Test Page](./test.md) to test FIDO functions.
