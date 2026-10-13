a network, or setting up security. In Chapter 17, I introduce the YaST Control Center and the various sysadmin tasks you can perform through the control center.

If you are at a text console, you can still use YaST — through its command line. For example, to install an RPM from a command-line, type **/sbin/yast -i** followed by the name of an RPM package.

![](bbox=[0.12, 0.252, 0.207, 0.322])

YaST used to be proprietary software, but in 2004, Novell released YaST under the GNU General Public License (GPL) — the same open source license that governs Linux itself.

# Detects All Hardware
(Well, Nearly All!)

One of the best things about SUSE Linux is that it detects nearly all hardware during installation and setup. For all detected hardware, SUSE Linux loads any drivers needed to access the hardware and takes care of any configuration steps such as adding entries in the `/etc/fstab` configuration file and creating subdirectories in the `/media` directory where a storage device could be mounted. The excellent hardware detection means that you can usually install SUSE Linux on most PCs without any trouble.

If you add hardware after you install SUSE Linux, you can connect the hardware to the PC, power it on, and then run the appropriate hardware configuration module from the YaST Control Center (see Chapter 17 for more on the YaST Control Center).

# Smooth and Easy Installation

SUSE Linux installation is neither oversimplified nor unnecessarily complex — it’s just right. With its hardware detection capabilities and the YaST GUI tool, an average user can easily handle the SUSE Linux installation. The installer makes easy even a potentially complex step such as resizing the Windows partition on the hard drive to make room for SUSE Linux. All you have to do is indicate the size of the Windows partition, and the installer takes care of shrinking the size of the partition.

Instead of guiding the user through a set sequence of installation screens, the installer presents all the options in a single screen. Then all you need to change are the items that need changing such as the time zone and maybe the software selection between the KDE or GNOME desktop. The installer handles all other configurations after installing the minimal system and rebooting. All in all, SUSE Linux installation is smooth and easy.