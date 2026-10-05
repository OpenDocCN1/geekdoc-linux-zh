# ## 8.3 Performing the migration

In this section, we discuss performing the migration.

# ### 8.3.1 Basic installation tasks

The first thing to do is complete a base installation from the distribution CDs. In the case of Red Hat Desktop, the CD set contains four CDs. Special packages for the desktop are available from the Red Hat Network. Third-party applications such as Acrobat Reader or Real Player and a set of high-quality trueetype fonts from AGFA.

During installation, we accepted the default selections for application packages defined by the installation program. On our target hardware, the Red Hat Anaconda installation program completed the base installation without any problems. Also, the Red Hat hardware probing library called kudu worked as expected. All hardware components were detected correctly. The modules for the integrated video and audio chipset loaded successfully. The network card driver was loaded, and the network was activated successfully at the end of the installation. The system successfully received a DHCP lease from the DHCP server in the ITSO network. Name resolution worked well, without any extra configuration steps.

# ## Setting up remote administrative access using VNC

Once the installation completed, we chose to immediately modify our client setup to provide remote terminal access to it from other workstations in the network using VNC. This way we could complete any additional administrative tasks to complete the install remotely.

To begin this process, we first checked that the SSH daemon was running and that every connection through VNC gets a complete desktop. One way to enable this for the root user is to modify the file $HOME/.vnc/startup, as shown in Example 8-1

> *Example 8-1 Enabling VNC connections*

```
#!/bin/sh
```

```
# Uncomment the following two lines for normal desktop:
unset SESSION_MANAGER
exec /etc/X11/xinit/xinitrc
....
```

Also, we had to enable Xdmcp in /etc/X11/gdm/gdm.conf and set up a session in /etc/sysconfig/vncservers.