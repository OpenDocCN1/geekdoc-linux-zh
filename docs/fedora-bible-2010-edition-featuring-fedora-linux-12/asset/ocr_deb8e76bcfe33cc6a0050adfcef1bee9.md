![](bbox=[0.13, 0.1, 0.87, 0.43])

Figure 25-1: Use Virtual Machine Manager to manage multiple guest systems from a Fedora desktop.

This chapter describes KVM technology and how you can use it to run virtualized operating systems within your Fedora system.

# ## Preparing for Virtualization

Before you start using KVM, you should understand the extra demands that are put on your system by running guest virtual machines. In particular, you should consider if your computer has enough resources to run virtual guests, check that all the packages you need are installed, and make sure that the necessary services are running.

# ## Checking computer resources for virtualization

When you run a guest virtual operating system, keep in mind that each instance might consume the same, or nearly the same, computing resources that the host system consumes. In other words, you must have enough processing power, disk space, and memory (RAM) available for all the guests you are running. Here are some things to check:

+   - **Memory** — Although some can run on less, most modern operating systems run best on at least 512M of RAM. So make sure that you have that much available for your host system, as well as for each guest you are running.

+   - **Storage** — You must check the disk space requirements for the operating systems you plan to install on your host computer (plus the applications you are installing with them). That storage area can come from a large raw file, a disk partition, logical volume, or one of several different storage file formats. Storage images such as qcow or qcow2 have the