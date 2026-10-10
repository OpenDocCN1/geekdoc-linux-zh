Subsequenty, the Linux installation will format only the partition(s) that will be used by Linux.

# Virtualization

But the big buzzword in computing these days is virtualization, the process of running one operating system on top of another. The base, or native, operating system is called the *host*. It runs a *virtual machine manager*, VMM, that in turn runs one or more virtual machines called *guests*. Whereas in the dual-boot scenario one or the other operating system is running exclusively, with virtualization the host and the guests are running simultaneously. You can even move files and data between them seamlessly.

There are two popular VMMs—VMware and VirtualBox. VMware is a commercial product from a company of the same name. They offer a free version called VMware Player that runs on both Windows and Linux hosts.

VirtualBox is an open source package sponsored by Oracle (formerly Sun Microsystems). It too is available for both Windows and Linux hosts, but also supports Mac OS X and Solaris.

The two packages are fairly similar in their installation and operation. After installing the software (see Resources section for download pages), you create one or more guest machines allocating resources to them, such as disk and RAM. A “wizard” steps you through the process of creating a new machine. A disk in the guest machine is represented by a very large file in the host. Then you install an operating system on the guest, in much the same way you would install it natively.

I happen to use VirtualBox.

# Installing VirtualBox

Installing VirtualBox is much like installing any Windows software. You download and run the installation executable. The default configuration is fine. You’ll be prompted if you want to install the Extension Pack. Yes, you do.

The next step then is to create a virtual “guest” machine and install Linux on it. Start the VirtualBox Manager and click the New icon in the upper left. Give the machine a name. VirtualBox will often infer the type and version from the name. Be sure they’re correct. Allocate RAM. I have 8 GB in my laptop, and allocate 2 GB to guest machines. I found that allocating more than 2 GB to the guest caused Windows to slow down.

Create a virtual hard disk. Leave the default disk file type, VirtualBox disk image (.vdi). I use dynamically allocated storage for the disk file. Your choice. By default, the disk file