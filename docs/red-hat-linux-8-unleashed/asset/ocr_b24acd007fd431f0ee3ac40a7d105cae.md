# CHAPTER 4 Post-Installation Configuration

You can perform many post-installation tasks without rebooting or downtime. With proper planning, you can also create a server or workstation configuration that allows "hot-swapping" of system storage and other components, eliminating the need for downtime. In this chapter, you learn how to configure USB and Firewire (IEEE-1394) devices in addition to keyboards, modems, and notebook PCMCIA devices.

Information about your system's installed hardware is contained in a file under the Red Hat directory system. Aside from one two symbolic links, or shortcut-type files created under the /dev directory for the convenience of system utilities, nearly all these hardware settings are in text files under the /etc directory. The contents of these files are used by Red Hat's various software services to manage your system's hardware, save changes to your hardware, ensure settings are saved between reboots, and properly configure your system upon booting. A number of files are used by /rc.sysinit created when Red Hat starts. For example, some of these files include

+   - /etc/sysconfig/hwconf—Lists the currently configured system hardware (used by kudzu)
- /etc/sysconfig/apm—Lists system power-management settings (used by apmd daemon)
- /etc/sysconfig/clock—Contains time zone, and hardware clock settings (used by the hw command)
- /etc/sysconfig/harddisks—System hardware drive tuning parameters
- /etc/sysconfig/irda—Provides configuration data concerning Infrared Data Association (IrDA) hardware
- /etc/sysconfig/keyboard—Lists current keyboard mapping (and provides language settings)
- /etc/sysconfig/mouse—Details the current system pointing device (such as whether or not a PS2 or USB mouse is used)
- /etc/modules.conf—Defines device names, kernel hardware support modules to load, and any optional parameters (see Chapter 24, “Kernel and Module Management,") for more information about Linux modules
- /etc/pcmcia—A directory containing a Personal Memory Card International Association (PCMCIA) hardware database and device settings (the section “Managing PCMCIA" later in this chapter)

You'll find additional information about the files in /etc/sysconfig in the file named sysconfig.txt under the /usr/share/doc/inscripts-6.91 directory.

# CAUTION

Don't edit kudzu's text-file database of installed hardware; these files are updated dynamically by Red Hat's software. If you have trouble with a device, however, you can check the information in these files when troubleshooting to see if the device is properly recognized and its definition matches the actual hardware.