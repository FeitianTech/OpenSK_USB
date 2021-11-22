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

To help and accelerate FIDO security key adoption, FEITIAN improves the housing and makes new designs of OpenSK USB Dongle, removes useless PCB components, public the design. Users can build firmware from the source code of [Google OpenSK Github repository](https://github.com/google/opensk "OpenSK") without changing anything, provision it to this OpenSK hardware, to experience and try [FIDO](https://fidoalliance.org/ "FIDO Alliance") authentications.

!!! warning "attention"
    Before you try or buy Feitian OpenSK Dongle, please be sure that you have read the important [caution](./caution.md) message.
