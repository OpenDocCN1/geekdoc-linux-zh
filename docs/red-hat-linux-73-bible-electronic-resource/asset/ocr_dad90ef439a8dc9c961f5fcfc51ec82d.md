+   - **Keyboard and monitor** — Although this seems obvious, the truth is that you only need a keyboard and monitor during installation. You can operate Red Hat Linux quite well over a LAN using either a shell interface from a network login or an X terminal.

There are versions of Red Hat Linux that run on Alpha and Spare workstations, instead of just on PCs. The CD that comes with this book and the installation procedures presented here, however, are specific to PCs. Most of the other software described in this book, however, will work the same in any of those hardware environments.

> **NOTE:** The list of hardware supported by Red Hat Linux is available on the Internet at www.redhat.com/hardware.

If your computer's CD-ROM device is connected to a PCMCIA port (such as those that come on laptop computers), you will need to install PCMCIA support during installation. PCMCIA support is available only on Intel-based computers. See the sidebar on installing Red Hat Linux on a laptop for further information.

# Installing Red Hat Linux on a Laptop

Because laptops can contain non-standard equipment, before you begin installing on a laptop you might want to find out about other people's experiences installing Linux on your model. Do that by visiting the Linux on Laptops site (www.linux-laptop.net).

If your laptop doesn't have a built-in CD-ROM drive, you probably need to install from a device connected to a PCMCIA slot on your laptop. PCMCIA slots let you connect a variety of devices to your laptop using credit-card-sized cards (sometimes called PC Cards). Linux supports hundreds of PCMCIA devices. You may use your laptop's PCMCIA slot to install Red Hat Linux from several different types of PCMCIA devices, including:

+   - A CD-ROM drive
+   - A LAN adapter

If you would like to know which PCMCIA devices are supported in Linux, see the SUPPORTED.CARDS file (located in the `/usr/share/doc/kernel-pcmcia-cs*` directory). In any of these cases, you need the PCMCIA support disk to use the device as an installation medium. The section on creating install disks describes how to create these installation floppy disks.

# Beginning the installation

If you feel you have chosen the right type of installation for your needs, you can begin the installation procedure. Throughout most of the procedure, you can click Back to make changes to earlier screens. However, once you are warned that packages are about to be written to hard disk, there's no turning back. Most items that you configure can be changed after Red Hat Linux is up and running.