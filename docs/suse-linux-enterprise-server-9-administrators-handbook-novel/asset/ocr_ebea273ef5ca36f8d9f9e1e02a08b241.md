When you have the basic components on hand, you need to do a little planning: The following are some topics you should consider before installing SLES 9:

+   - **The role of the system**—The role of your system determines what software packages (thus, what amount of RAM and disk space) it may require. For instance, if the server is to be a dedicated Domain Name System (DNS) server, there is no need to put a 120GB hard disk in it unless you expect a huge DNS database. Furthermore, a dedicated DNS server would not require a GUI desktop because you can generally perform all necessary configurations using the text-based YaST (Yet another Setup Tool) or using a simpler text editor like vi. You should make a list of network services that your server will be offering and then install only the required packages, their dependencies, and nothing more.

# TIP

We strongly recommend against installing any GUI desktop on production servers. The extra overhead takes away all the necessary CPU cycles and RAM from important network services.

# NOTE

Software packages can be easily added and removed after the server is up and running. However, experience has taught us that, more often than not, after a package is installed, it is rarely removed, either due to laziness or lack of time. Furthermore, any installed software can be a source for security vulnerability. You will learn later in this book that one of the best ways to secure a system is to run the minimum amount of services required, which means installing only what you need for that rogue services may be started without your knowledge.

+   - **Hard disk partitioning scheme**—For a production server, all the available hard disk space should be devoted to Linux. However, you may want a test server to dual-boot or multi-boot with a number of different operating systems. Even if all the hard disk space is used for Linux, you still need to decide how to “break up” the disk space for the various filesystems, such as root (/), /home, and so on. For example, a standard SLES 9 install takes up about 1.5GB of disk space. This means you should allocate perhaps 2GB to the root filesystem to allow room for expansion. A rule of thumb is, if you have 4GB or less of total disk space, create one partition of swap (typically twice the physical RAM size) and