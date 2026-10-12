# Make Host Specific Customizations to the Installed Image

Once the operating system image has been installed, a minimal amount of customization is required to make the system functional. This customization includes setting the proper network settings, specifically the IP address and the hostname. This can be accomplished easily using a script or by logging into the system and editing the files by hand. The amount of customization required depends on several factors, including the complexity of your network, whether or not you use dynamic IP address assignment, and other factors. How you customize is left to you.

# Install Boot Loader

The final step for installing a system that will not be running the X Windows system is to install the boot loader. This is simply a matter of running lilo against the lilo.conf file that is part of the installed operating system image. Assuming that you have the installed image mounted as /mnt, this can easily be accomplished by issuing the following command:

```
/mnt/sbin/lilo -r /mnt -v -v
```

Once this is done, you are ready to reboot you newly installed system. Depending on the degree of automation you add to this process, you can make the installation of a new system a simple matter of booting from floppies, getting on the network, and issuing a script from the host containing your operating system template. I have used this method for some time with great success. The time to install a system once booted from floppies is under five minutes.

The homegrown approach described here is just one method. If you are not inclined to use it, there are alternatives including one from Red Hat, known as a kickstart.

# Using Kickstart Files and RPM

If the previously described method of installation sounds like a lot of work, that's because it is. An alternative approach to installing multiple systems with minimal fuss is to use the kickstart capabilities provided by Red Hat. The kickstart method is accomplished by creating a file that specifies the answers to the questions asked by the installation program. This file can be copied to the boot floppy or can be made available on the network and the name is dependent on which of these two options you choose. Details on using the kickstart method are found in the installation guide that is included with your Red Hat Linux software. With kickstart files, you can eliminate the bulk of the interaction required by the install program and predefine a set of packages to be installed on a system. This method