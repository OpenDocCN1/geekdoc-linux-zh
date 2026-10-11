![](bbox=[0.06, 0.15, 0.19, 0.27])

# Create a custom image of OpenWRT

Creating a custom build of OpenWRT enables you to take intimate control of the content of your router’s firmware

**Tam Hanna**
Tam’s experience in the creation of embedded systems instilled him with a deep interest in build systems. Even though OpenWRT’s build system cannot stand up to Yocto’s, its simplicity nevertheless makes for some interesting learning!

# Resources

OpenWRT
openwrt.org

The end of the last tutorial on OpenWRT was somewhat discouraging: as the OpenWRT team did not populate many of the packages, our experiments on the Raspberry Pi were severely limited due to the lack of available products.

Fortunately, solving this problem is not particularly difficult. OpenWRT, after all, is but another version of Linux — when this tutorial’s author was a young code, compiling our own kernel was a badge of honour for every professional user. When this is done, the amount of software available to our OpenWRT build is limited only by our imagination and the memory of the target device.

The following guide will show you how to create your own OpenWRT image for Raspberry Pi process computers. Be aware that this operation is not resource-cheap: the following project was written on an AMD octa-core workstation equipped with SSD flash memory, 16GB of RAM and a cooling system optimised for permanent high performance. Performing the same steps on notebooks — HP’s compact sub-notebook families such as the 2540p are common suspects — is likely to lead to thermal issues that could damage your hardware.

As in most other operations, creating a working directory is a great first step. In the case of OpenWRT, be careful: the build system does not allow spaces or weird characters in its path. We used the following working directory:

```
```
tamhan@TAMHAN14:~$pwd
/home/tamhan/wrtspace
```
```

Compiling complex operating systems requires the presence of a variety of tools on the host. The installation instructions recommend Ubuntu users to execute the following commands:

```
```
$ sudo apt-get install git-core build-essential
libssl-dev libcurlss5-dev unzip gawk zlib-dev
$ sudo apt-get install subversion mercurial
```
```

In the next step, code must be downloaded from OpenWRT’s repositories. This is accomplished by git — due to the limited speed of the service, be prepared to wait a minute or two:

```
```
tamhan@TAMHAN14:~$wrtspace$ git clone https://
github.com/openwrt/openwrt.git
Cloning into 'openwrt'...
---
Receiving objects: 100% (360595/360595), 132.89
MiB | 1.32 MiB/s, done.
---
```
```

Our downloaded code must be expanded by a few external modules. This is best accomplished by changing into the OpenWRT directory, where you must then run two additional commands that download optional packages from various sources:

```
```
cd openwrt
./.scripts/feeds update -a
./.scripts/feeds install -a
```
```

![](bbox=[0.08, 0.78, 0.17, 0.85])

Tutorial files
available:
fileso.co.uk