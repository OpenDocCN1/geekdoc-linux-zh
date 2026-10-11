
## HARDWARE REQUIREMENTS FOR LINUX

While Linux can be run on other types of workstations, such as Macs and Amigas, this book is more suitable for users familiar with Microsoft Windows run on IBM-compatible PCs. We also concentrate on Linux for the standalone computer, leaving aside its considerable capabilities for handling networks. This book is largely intended for the curious beginner with experience of Windows rather than the programmer or experienced network user.

### REQUIREMENTS FOR RUNNING LINUX

- You can run Linux on an ancient 386, but if you will have to run all your programs and commands from the command prompt. However, to use a Windows-type graphical desktop, you will need at least a fast 486 processor, and preferably a high-end Pentium processor.
- Specifications naturally vary depending on what you intend to run under Linux. Simple word processing and spreadsheet applications will require much less processor power than the serious number-crunching required by most graphics applications and the latest 3-D games. If your needs are very slight, you can even find stripped-down versions of Linux that will load from a single floppy disk.

![](img/773dce76f7b88c1faa45d71937dc4026_15_0.png)

![](img/773dce76f7b88c1faa45d71937dc4026_15_1.png)

For a dual-boot installation of Linux (Linux + Windows), leave plenty of space for the applications you will install later. If you also want to share your computer with others, leave sufficient space for the other users. However, as administrator, only you will be able to install new applications.

![](img/773dce76f7b88c1faa45d71937dc4026_16_0.png)

Note: Search the LDP mailing list archives at http://linux.scsyr.edu/docs/

The Linux Documentation Project at www.linuxdoc.com is a site to note. A search for “dual boot” returned 199 hits.

## LINUX INSTALLATIONS

These three specifications would enable the installation of Linux with a graphical Windows-like desktop and a typical combination of utilities and applications.

### LOW SPECIFICATION

- 40386, 8 MB RAM, 540 MB free hard-disk space.

### ACCEPTABLE CONFIGURATION

- Pentium, 32 MB RAM, 850 MB hard-disk space.

### RECOMMENDED SETUP

- Pentium processor, 200 MHz minimum, at least 32 MB RAM, at least 1500 MB hard-disk space.

### ALSO REQUIRED

- CD-ROM drive. Floppy disk-based installers exist, but most distributions occupy at least one CD.
- Supported video card. If you are intending to install Linux on an older PC, you must check whether your hardware is supported by Linux.

## LINUX DISTRIBUTIONS

When people refer to Linux, they are generally referring to the bundle of software, code, and documentation that companies such as Debian and Red Hat sell as a “distribution.”

### WHAT’S ALL THIS JARGON?

Linux can seem heavy on the jargon—especially for beginners—with terms such as X Windows, desktop environments, file managers, X servers, and GUIs. While it is not essential to understand how all the components fit together, it is useful to be familiar with the basic terminology.

Similarly, you don’t have to be a mechanic to drive a car, but it helps to know what all the main parts are called, and it is always useful to be able to carry out some routine maintenance. These pages introduce some of the terminology you will encounter when reading about Linux.

#### THE KERNEL

At the heart of Linux is the kernel. This is the code that is loaded before anything else when you launch Linux, and is unloaded last when you halt the system. On its own, the kernel doesn’t appear to do very much, but without it, nothing gets done. The kernel acts as the main link between your hardware and all the programs that run under Linux. It also handles crucial background tasks such as managing the memory and multitasking.

![](img/773dce76f7b88c1faa45d71937dc4026_17_0.png)

**The Linux Kernel HOWTO**

Brian Ward bri@cs.uchicago.edu

v1.25, 28 Mar 2001

*This is a detailed guide to kernel configuration, compilation, upgrades, and.*

1. **Introduction**
    1. Read this first. (1 min. 95)
    2. Good for 1.2.x, 2.2, and 2.4 kernels.
2. **Quick Steps – Kernel Compile**

Everything about the Linux kernel is in Brian Ward’s work at www.linuxdoc.org/HOWTO/Kernel-HOWTO.html.

### THE TOOLS

- Linux tools are a group of programs between the kernel and the software that displays Linux on the desktop. One of the most important tools is the C/C++ compiler. This tool compiles a program written in C or C++, and turns the code into an executable program that can be run by Linux.

### THE APPLICATION SOFTWARE

- In its raw state, Linux does not need a GUI to enable it to work. Here, however, we concentrate on the graphical applications that enable Linux to run as a window-based operating environment.

### X WINDOWS

- The X Window system is used to set up an “X server” on your computer. This holds information about the capabilities of your graphics card and display.

#### About This Page

Here are some C and C++ libraries, DLLs, source code, components, frameworks, class libraries, source code snippets, and the like. Pay no attention to the license terms in this section, as they are the same (or similar) to the license terms of any of the other sections in this book. Be sure to read the license notes under your distribution.

Free tools, libraries, and C/C++ utilities are available at www.thefreecountry.com/develop/ptty/freeclibraries.shtml.

![](img/773dce76f7b88c1faa45d71937dc4026_18_0.png)

![](img/773dce76f7b88c1faa45d71937dc4026_18_1.png)

### WINDOW MANAGERS

X-based desktop managers provide the graphical interface between your input (via keyboard/pointing device) and what happens on your monitor. Some window managers look and feel like Microsoft Windows and all are highly customizable. These programs manage the placement of windows including positioning, overlapping, and iconizing.

![](img/773dce76f7b88c1faa45d71937dc4026_19_0.png)

### DESKTOP ENVIRONMENTS

- The two leading desktop environments are GNOME and KDE. Gnome (GNU Network Object Model Environment), which were developed as open source software.
- KDE (the K Desktop Environment) was built using a GUI toolkit called Qt and KDE also widely used.
- Both desktop environments are supplied with Red Hat Linux. They are also available with most other popular distributions.
- Certain window managers are incompatible with some desktop environments, but the relevant sites will provide the necessary advice.

![](img/773dce76f7b88c1faa45d71937dc4026_19_1.png)

### WHAT DO I GET?

- Your choice of Linux distribution will depend on your assessment of the quality of the vendor's installation program, documentation, and after-sales support.
- The Linux bundle always contains the Linux kernel and a range of the following components:
    - Desktop manager
    - At least one text editor
    - Paint program
    - Web browser
    - Multimedia tools
    - Utilities
    - Games
    - Programmers' tools
- Many distributions will also provide:
    - Technical support
    - CDs of third-party applications, full versions of the StarOffice suite are bundled with Suse and Red Hat Linux
- You will also be supplied with manuals, sometimes running to several thousand pages.
- You can find an up-to-date list of the main Linux distributions, including descriptions and links to the websites of the developers, on the excellent *Linux online* website at www.linux.com

### WHERE DO I GET IT?

- Downloading Linux, even with only a fraction of the related applications and documentation, can be lengthy. And your online connection must be reliable because you don't want it dropping part way through a download. Also, you must know exactly what you're doing if you decide to download the kernel and build a version of the operating system from this source.

**BUY IT ON CD**

- Some vendors sell a CD containing the bare bones of a distribution, as downloaded from the net, for a couple of dollars. This gives you a lot of possibly expensive and time-consuming downloading. Again, you will have to know what you're doing, and not merely regarding installing the software.

**BUY A BOXED SET**

- Boxed sets are easy to find. Your software store is likely to sell a boxed set from a main distributor, such as Caldera, Debian, or Red Hat. With this method, everything you need is likely to be provided, including an installation program and printed materials. The only downside is that this method is usually the most expensive.

### ON A FREE BOOK OR MAGAZINE CD

- In this form, it's free – if you were going to buy the magazine or book anyway. However, you're not supplied with the distributor's documentation, and the book is likely to be generic rather than to deal with the specific version you are installing. You also receive little or no commercial support to try out.

### DOWNLOAD IT FROM THE INTERNET

- In this form, it's free – provided you are not paying telephone bills and you have a lot of spare time.
