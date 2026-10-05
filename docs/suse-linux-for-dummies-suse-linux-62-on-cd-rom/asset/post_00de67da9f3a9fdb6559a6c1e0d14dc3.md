
# Chapter 5: Installation: Down to the Final Stretch

![](img/96a9ce6a13d8d15ed05f867f41574278_122_0.png)

Figure 5-50: Configuring your network card.

## SELECTION OF NETWORKING DEVICE
Here you may select your networking device. Your selections will be written to /etc/conf.modules

| Network type | eth0 |
|---|---|
| Networking device type | 3cm-3c01<br>3cm-3c03<br>3cm-3c05<br>3cm-3c07<br>3cm-3c11 |
| Module options: :io0=2xb0 | 3cm-3c51a<br>3cm-3c90<br>AMI PCI Power32 (AT1800/HE2100)<br>AMI PCI Power32 (PCI me2100)<br>Ansel Communications ISA 3200<br>Africot Xen-II on board ethernet<br>AT-LAN3/Realtek pocket adaptation<br>AT1700 |
| < Continue |

The Please enter the data required for the configuration of your network. These are the IP address you want to give the machine currently operating on the network and the mask is 255.255.255.0 for most of the (smaller) networks, but you may wish to set it to a different value. If you need a gateway for NFS server, please enter the IP address of the gateway host.

Figure 5-31: Configuring your IP address.

| Type of network: | eth0 |
|---|---|
| IP address of your machine: | 192.168.69.103 |
| Mask (usually 255.255.255.0): | 255.255.255.0 |
| Default gateway address (if required): | 192.168.69.1 |
| IP address of the Point-to-point partner: | |
| < Continue | Abort > |

The next four screens ask you about what kind of network service you want your machine to provide. In each case, we recommend that you select Yes if you are sure. At any time later, you can stop your machine from providing the different network services. The services that you will be prompted for are Inetd, portmaster, and NFS-Server. After accepting these services, you will be prompted to verify your From Address. The default will be fine, so you can press Enter.

The next screen asks whether you want to access a name server and DNS are used interchangeably. To access other machines on the Internet, you must access a name server. If you are unsure about the IP address of the name server, ask your network administrator. If you will be connecting to the Internet via an ISP, the ISP should have provided you with the IP address of the name server. If you are still confused, select No, because you can configure this information at any time later on.

# 96 Part II: Installing SuSE Linux

When you have completed all these steps, a screen appears indicating that all the network settings have been configured.

## Sendmail configuration

The next dialog box asks a slightly more detailed question about your network configuration (see Figure 5-32). If you do not have a permanent connection to a network but you will be using your modem, select the Host with Temporary Network Connection option.

If you have a permanent connection to a network, select the Host with Permanent Network Connection option and press Enter. A configuration script called SuConfig will run and your system configuration files will be updated by your selections in the previous dialog boxes. When the script is finished, press Enter.

![](img/96a9ce6a13d8d15ed05f867f41574278_123_0.png)

Figure 5-32: Selecting a Sendmail-configuration.

## Setting the root password

Linuxrc reappears and tells you that the system will be rebooted to commit the installation. Press Enter, and the system is rebooted.

The installation program now prompts you to select a password to use for logging in to your Linux system. The password that you are entering is for the root user, also known as the superuser, who has access to the entire system.

We recommend that you use a combination of uppercase and lowercase letters as well as numbers to make the password as difficult to compromise as possible. In addition, do not choose names or items that are easy to associate with you. In others, your name, your dog's name, or 12346, passwd, and the like are poor choices. Select a password and then be sure to write it down where it won't get lost. Don't write it on a sticky note attached to your monitor, please.

You have to enter the password two times to make sure that you typed it correctly; the password doesn't appear on the screen as you type it. Holy mol, Batman. You wouldn't want someone to be able to look over your shoulder and get your password now, would you?

When you've managed to type your password the same way twice, YaST restarts automatically to finish some configuration settings.

Logging in as the root user only to do system maintenance or administrative tasks is best. The root user is the only one with access to critical system files. To avoid unwanted changes or deletions, add another user for your use.

![](img/96a9ce6a13d8d15ed05f867f41574278_124_0.png)

# Chapter 5: Installation: Down to the Final Stretch

## Creating an account

When YaST restarts, a screen appears asking if you want to create a user account. This is not required, but it is recommended to have one for your daily use. If you choose to create one, you will be prompted to enter a username and a password. The password should be as strong as the root password.

## Configuring your modem

If you have a modem, you will be prompted to configure it. You will need to select the type of modem and the phone number. If you do not have a modem, you can skip this step.

## Configuring your mouse

The next screens ask you about what kind of mouse you are using. You can select from a PS/2 mouse or a USB mouse. If you are using a USB mouse, you may need to install the drivers. The mouse configuration boxes shown in 33,, 33 show show you to of your modem.
