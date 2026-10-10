If your computer doesn’t have a DVD drive, you can use the `boot.iso` CD image that comes on the DVD with the book (see below) to start a network install (HTTP, FTP, or NFS). Just type `linux askmethod` at the boot prompt, to begin the installation process.

If you don’t have a bootable DVD or CD drive, there are other ways to start the Fedora installation. Unlike some earlier Fedora and Red Hat Linux versions, Fedora doesn’t support floppy disk boot images (the Linux 2.6 kernel is too large to fit on a floppy disk). Therefore, if you don’t have a bootable DVD or CD drive, you need to start the install process from some other medium (such as a USB device, PXE server, or hard drive, as described later in this chapter).

The following specialty installation types also may be of interest to you:

+   * **Boot CD** — You can create a boot CD from the boot images contained on the Fedora installation DVD that comes with this book. Copy and burn the file `boot.iso` from the `images` directory on the DVD. You can use the CD you create from that image to begin the install process if you have a DVD drive that is not bootable or if you have the Fedora 8 software available on any of the media described in the `linux askmethod` section.

+   * **USB or other bootable media** — If your computer can be configured to boot from alternate bootable media, such as a USB pen drive, that is larger than a floppy disk, you can copy the `diskboot.img` file to that medium and install from there. That image is contained in the `images` directory on the DVD.

+   * **Kickstart installation** — Lets you create a set of answers to the questions Fedora asks you during installation. This can be a time-saving method if you are installing Fedora on many computers with similar configurations.

A Fedora Installation Guide is now available from the Fedora Project, if you find you need further information. It may not be up to date, however. You can access the guide here: `http://docs.fedoraproject.org/install`

# ## Choosing computer hardware

This may not really be a choice. You may just have an old PC lying around that you want to try Fedora on. Or you may have a killer workstation with some extra disk space and want to try on Fedora on a separate partition or whole disk. To install the 32-bit PC version of Fedora successfully (that is, the version on the accompanying DVD), the computer must have the following:

+   * **x86 processor** — Your computer needs an Intel-compatible CPU. With the latest version, Fedora recommends that you at least have a Pentium-Class processor to run Fedora. For a text-only installation, a 200 MHz Pentium is the minimum, while a 400 MHz Pentium II is the minimum for a GUI installation.

+   * **DVD or CD-ROM drive** — You need to be able to boot up the installation process from a DVD, CD-ROM, or other bootable drive. (Other drives can include a USB