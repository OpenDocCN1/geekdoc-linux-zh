But there are other times when you need other features beyond those outlined in the previous section or presented in Project 8-2 at the end of the chapter. Some of these, such as setting up a network installation server and preparing multisk file systems are left to later chapters. This section describes one advanced feature: using Red Hat's Kickstart tool.

**Kickstart** is a method of automating installation selections so that you can reinstall a system, or install multiple identical systems, without entering all the information discussed in Project 8-2. Instead, the installation program relies on a configuration file that contains all of the settings to complete the installation.

The basic process for using Kickstart is as follows:

+   1. Create a **kickstart configuration file** using the graphical Kickstart Configuration utility or else use the kickstart configuration file created when you installed Linux (this is the safer choice when first using Kickstart).
+   2. Copy the kickstart configuration file onto a removable disk under the name ks.cfg.
+   3. Insert the Fedora CD and boot the Linux installation program on the system where you want to use the kickstart configuration file to control the installation.
+   4. At the first screen, instead of just pressing Enter to start the installation program, enter the text linux ks=floppy and press Enter.
+   5. The kickstart configuration file is read and used to control all aspects of the installation that are defined in that file. Assuming the configuration file is complete, the system restarts when the installation is complete, without any intervention on your part.

# Reviewing the Kickstart Configuration File

When you complete an installation in Project 8-2, a kickstart configuration file is created based on the choices you made during that process. The file is /root/anaconda-ks.cfg. You can follow the steps just given and use that file to immediately experiment with Kickstart, but it's a good idea to review the contents of the file first. Project 8-4 uses this file as the basis of a Kickstart installation.

The contents of the file for one system are shown here for reference. Note that this file is different from the file on your system because each system uses different partitions, has different hardware, and requires different software packages be installed. You can use any text editor to view the kickstart configuration file on your system.

Although you may not have installed Linux yourself yet, someone installed your system. If you have root access, you can use any text editor to view the existing kickstart configuration file. Try entering this command in a graphical terminal window:gedit /root/anaconda-ks.cfg. You should see something similar to the following: