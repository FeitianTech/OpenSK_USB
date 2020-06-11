Congratulations that you have got your own OpenSK USB dongle, now you can try FIDO functions to do fast online authentication. OpenSK implements [FIDO2(CTAP2)](https://fidoalliance.org/fido2/) and FIDO U2F specifications, it can support any website leveraging [W3C WebAuthN](https://www.w3.org/TR/webauthn/).  

##Manage OpenSK
There are two ways to manage your OpenSK USB Dongle, include Reset, Set PIN and Change PIN.  
####Windows Settings
1. Open the **Windows Settings app**, select **Accounts**, select **Sign-in options**, select **Security Key**, and then select **Manage**.
2. You can then attach OpenSK to USB port to manage it as as you want.  

!!! note "NOTE"
    1. Please refer to [Microsoft Document](https://docs.microsoft.com/en-us/azure/active-directory/user-help/security-info-setup-security-key#manage-your-security-key-settings-from-windows-settings "Manage your security key settings from Windows Settings") for detailed information.
    2. **Security Key** option in **Windows Settings** is only available from Windows 10 1903. 

####Chrome Browser
1. From Chrome browser, open URL **chrome://settings/securityKeys**, or open menu "Settings” => “Privacy and security” (More)=> “Manage security keys”.  
2. You can see **Manage security keys** page, then you can do corresponding operations following the tips.

!!! note "NOTE"
    I don't know the exact version of Chrome which started to add this UI, but please update it to latest version to have this function.

##Demo Websites
There are a lot of Demo websites list [here](https://github.com/herrjemand/awesome-webauthn#demos), you can try and test.   
Here I recommend   
- https://webauthn.io/ (from DUO)   
- https://webauthndemo.appspot.com/ (from Google)

!!! warning "WARNING"
    I can not guaranty that all the demo websites can work well with OpenSK.

##Real use cases
There are a lot of online servides which can use FIDO2/U2F to do 2FA or passwordless authentication, please refer to [FEITIAN website](https://www.ftsafe.com/article/620.html) and click corresponding service ICON to learn.

Here just emphasize services from two big FIDO players, Google and Microsoft.

### Google
#### - Google 2-Step Verification
- Please refer to [Google's help](https://support.google.com/accounts/answer/185839?co=GENIE.Platform%3DAndroid&hl=en) to bind OpenSK to your Google services. Or   
- Take a look at 2.1 of [Feitian's help document](https://www.ftsafe.com/download/webdownload/FIDO/Manual/FEITIAN%20U2F%20scenarios%20instructions.pdf) to bind and try OpenSK instead of ePass FIDO security key.

#### - Googel Advanced Protection  
- Please refer to [landing page](https://landing.google.com/advancedprotection/) or [help page](https://support.google.com/accounts/answer/7519408?co=GENIE.Platform%3DAndroid&hl=en&oco=0) of Google Advanced Protection to get how to setup.  

### Microsoft
#### Microsoft Account Passwordless Logon
- Please refer to [Microsoft Blog](https://www.microsoft.com/en-us/microsoft-365/blog/2018/11/20/sign-in-to-your-microsoft-account-without-a-password-using-windows-hello-or-a-security-key/) to learn how to do Microsoft Account Passwordless Logon with FIDO2 security keys. Or  
- Take a look at Chapter 2.2 of [FEITIAN FIDO2 scenarios](https://download.ftsafe.com/files/FIDO/fido2/FEITIAN%20FIDO2%20scenarios%20instructions.pdf) to configure OpenSK with Microsoft Account step by step.

### Others
Surely there are a lot of other online services except for Google's and Microsoft's, you can learn from  
- [FIDO2 Scenarios](https://download.ftsafe.com/files/FIDO/fido2/FEITIAN%20FIDO2%20scenarios%20instructions.pdf) and [U2F Scenarios](https://www.ftsafe.com/download/webdownload/FIDO/Manual/FEITIAN%20U2F%20scenarios%20instructions.pdf) from Feitian's resources.  
- [Knowledge Base](https://xpass.freshdesk.com/support/solutions/60000318639) from Feitian  
- [fido.ftsafe.com](https://fido.ftsafe.com/catalog/) Dedicated FIDO website from Feitian. Here you can find list of online services to use FIDO.


