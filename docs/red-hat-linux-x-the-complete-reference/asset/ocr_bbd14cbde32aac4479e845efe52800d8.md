# Hardware, Software, and Information Requirements

Before installing Linux, you must ensure that your computer meets certain minimum hardware requirements. You also need to have certain specific information ready concerning your monitor, video card, mouse, and CD-ROM drive. All the requirements are presented in detail in the following sections. Be sure to read them carefully before you begin installation. During the installation program, you need to provide responses that reflect the configuration of your computer.

# Hardware Requirements

Listed here are the minimum hardware requirements for installing a standard installation of the Linux system on an Intel-based PC:

+   - A 32-bit Intel-based personal computer. At least an Intel or compatible 80386, 80486, or Pentium-class microprocessor is required. A 400 MHz Pentium is recommended for a graphical interface and 200 MHz for text.
+   - A CD-ROM or DVD-ROM drive (if you are using the DVD-ROM included with this book, you will need a DVD-ROM drive).
+   - A 3 1/2-inch floppy disk drive and floppy disk, if your PC is not capable of booting from CD-ROM or DVD-ROM. A 3 1/2-inch, DOS high-density (HD) floppy disk drive is used to create an install disk (if you are installing from a floppy). If you install directly from a CD-ROM, you will not need it. A boot floppy can be created using either the Linux or Windows operating system.
+   - Normally, at least 64MB RAM for text, and 192MB for graphical. (Linux can run on as little as 12MB RAM.) At least 2GB free hard disk space for a standard installation, including applications (keep in mind that Linux can run on far less on a minimum installation, as little as 100MB and 16MB swap); 3GB to 6GB or more is recommended for a full installation (all applications). You need about 5GB to install all the software packages on most distribution CD-ROMs. The standard installation of basic software packages normally takes 3GB, plus 64MB to 512MB for swap space, depending on the amount of RAM memory you have. If you have less than 1GB of hard disk space, you can elect to perform a minimum install, installing only the Linux kernel without most of the applications. You could later install the applications you want, one at a time, using the redhat-config-packages tool accessible on the System Settings window.
+   - Hard disk requirements depend on the kind of installation you want:

+   - Custom Installation (minimum): 520MB
+   - Server (minimum): 870MB
+   - Personal Desktop: 1.9GB
+   - Workstation: 2.4GB
+   - Custom Installation (everything): 5.3GB

# Hard Drive Configuration

These days, Linux is usually run on its own hard drive, though it can also be run in a different partition on a hard drive that also contains a separate partition for a different operating system such as Windows.

If you want to install Linux and Windows on the same hard drive, you can use a partition management software package, such as fdisk, fips, Parted, or Partition Magic, to set up your Windows and Linux partitions. If you have already installed Windows on your hard drive and configured it to take up the entire hard drive, you would resize its partition to free up unused space. The freed space could then be used for a Linux partition. See the Red Hat Linux x86 Installation Guide for more details.

# Information Requirements

Part of adapting a powerful operating system like Linux to the PC entails making the most efficient use of the computer hardware at hand. In almost all configurations, your Linux installation process will automatically detect and configure your hardware components. Sometimes, however, particularly with older or very recent hardware, your installer may not be able to correctly identify a component. If you have such components, such as a new model monitor or video card, you should first check their manuals and take note of certain configuration settings.