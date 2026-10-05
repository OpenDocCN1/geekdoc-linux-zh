*-dkms* packages installed (check with dpkg -l "*-dkms*" | grep ii). The other packages are generally not needed (Unless you know how you need them!)

# 9.3. Building Custom Kali ISO Images

Kali Linux has a ton of functionality and flexibility right out of the box. Once Kali is installed, you can perform sorts of amazing feats with a little guidance, creativity, patience, and practice. However, you can also create a Kali build that it contains specific files or packages (to scale up or down performance and features) and can perform certain functions automatically. For example, the Kali ISO of Doom and the Kali Evil Wireless Access Point are both excellent projects that rely on a custom-built implementation of Kali Linux. Let's take a look at the process of rolling a custom Kali Linux ISO image.

Official Kali ISO images are built with live-build, which is a set of scripts that allows for complete automation and customization of all facets of Kali image creation. The live-build suite uses an directory structure input for its configuration. We store this configuration and some associated helper scripts in a live-build-config Git repository. We will use this repository as a basis for building customized images.

Before going further, you must know that the commands shown in this section are meant to be run on an up-to-date Kali Linux system. They are very likely to fail if run on a non-Kali system or if the system is out of date.

# 9.3.1. Installing Pre-Requisites

The first step is to install the packages needed and to retrieve the Git repository with the Kali live-build configuration:

```
# apt install curl live-build
[...]
# git clone https://gitlab.com/kalinux/build-scripts/live-build-config
# cd live-build-config
# ls
  auto build_all.sh build.sh kali-config README
```

At this point, you can create an updated (but unmodified) Kali ISO image just by running ./build.sh --verbose. The build will take a long time to complete as it will download all the packages to include. When finished, you will find the new ISO in the images directory.

> ^5https://www.offensive-security.com/kali-linux/kali-linux-iso-of-doom
⁶https://www.offensive-security.com/kali-linux/kali-linux-evil-wireless-access-port/
⁷http://debian-live.alioth.debian.org/live-build/