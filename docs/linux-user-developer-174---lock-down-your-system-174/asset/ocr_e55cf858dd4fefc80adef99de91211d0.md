![](bbox=[0.0, 0.15, 0.97, 0.56])

competitors are traditionally slow at undertaking. Away from that, Guinux also provides built-in system recovery and failsafe mechanisms as standard, as well as OTA updates with minimal downtime. For newer users, we’ve also made sure Guinux works instantly out of the box, providing hassle-free deployment and a pre-installed standard web-based configuration interface. Our final standout option is the pacman package management system, which combines a simple binary package format with an easy-to-use build system. The goal of pacman is to make it possible to easily manage packages, whether they are from the official repositories or the user’s own package builds.

# How much of the distribution is core Arch Linux? Has there been a lot of modifications to it?

Almost all of it is core Arch. We tied the core components together to allow for the development of enterprise solutions on top of the Arch Linux system.

Our main focus was to allow more applications to be deployed onto the core. We added components that are expected from embedded distributions, such as a web config site and modules/libraries

# Bringing Guinux to the Pi

One of the most interesting things that have come from the development of Guinux is that it now works with a number of third-party boards. While there’s a lot of interest in porting Guinux across to the Beagle Bone Black board, most users will want to familiarise themselves with the distribution on the Raspberry Pi. The availability of Guinux on the Pi is done through a NOOBS OS image, but with a twist. Unlike other NOOBS images, Guinux first installs the fail back rescue system, which in turn is then used to download and install the base Guinux packages. For end users, this keeps download and install times to an absolute minimum. Of course, users also have the option to download the NOOBS image directly onto an SD card and install.

Guinux, that way, but the process is vastly more complicated. Once the Guinux and Pi partnership is complete, users can then get stuck into a full configuration web interface, which can be tailored to meet your exact needs, and help optimise what the Pi can handle.

![](bbox=[0.39, 0.83, 0.93, 0.93])