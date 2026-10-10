should read the Kernel-HOWTO (see “Kernel-HOWTO.html”). For information on how to configure kernel modules you should read the “Modules mini-HOWTO.” Also, the README file found in the kernel sources and the Documentation directory are very informative for the brave reader.

Unless specifically stated otherwise, I recommend you stick with the standard kernel release (the one with the even number as the second digit in the version number). Development release kernels (the ones with the odd second digit) may have structural or other changes that may cause problems working with the other software on your system. If you are uncertain that you could resolve those sorts of problems, then don’t use them.

On the other hand, some of the features described here have been introduced during the development of 2.1 kernels, so you must take your choice: you can stick to 2.0 while waiting for 2.2 and an updated distribution with every new tool, or you can get 2.1 and look around for the various support programs needed to exploit the new features. As I write this paragraph, in August 1998, 2.1.115 is current and 2.2 is expected to appear pretty soon.

# # Current Network Tools

The network tools are the programs that you use to configure Linux network devices. These tools allow you to assign addresses to devices and configure routes, for example.

Most modern Linux distributions are supplied with the network tools, so if you have installed from a distribution and haven’t yet installed the network tools, then you should do so.

If you haven’t installed from a distribution, then you will need to source and compile the tools yourself. This isn’t difficult.

The network tools are now maintained by Bernd Eckenfels and are available at: ftp.inka.de (see http://ftp.inka.de/pub/comp/ Linux/networking/NetTools/) and are mirrored at: ftp.uk .linux.org (see http://ftp.uk.linux.org/pub/linux/ Networking/base/).

Be sure to choose the version that is most appropriate for the kernel you wish to use and follow the instructions in the package to install. To install and configure the version current at the time of this writing, you need do the following:

```
user% tar xvzf net-tools-1.33.tar.gz
user% cd net-tools-1.33
```