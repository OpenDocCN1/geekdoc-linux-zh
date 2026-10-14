10. Create a link from the new device definition you created in each of the networking configuration directories where the network management scripts expect to find them. Enter these two commands while still working in the /etc/sysconfig/network-scripts directory:
ln ifcfg-eth0:1 ../networking/device/
ln ifcfg-eth0:1 ../networking/profiles/default

11. Restart networking by entering service network restart.

12. Run the ifconfig | less command. Notice that you now have a new, third interface: eth0:1.

13. Ping the IP address of your eth0 interface. Ping the IP address of your eth0:1 interface. You could now use these independent interfaces to set up two separate Web sites or FTP servers on the same computer.

14. Delete the three files you created, confirming the deletion if prompted (these commands assume you are still working in the /etc/sysconfig/network-scripts directory):
rm ifcfg-eth0:1
rm ../networking/device/ifcfg-eth0:1
rm ../networking/profiles/default/ifcfg-eth0:1

15. Restart networking again: service network restart

16. Run the ifconfig command to verify that you once again have only two networking devices: lo and eth0. Close all windows and log off.

# Project 12-3

In this project, you use the ping command to explore how the Linux resolver operates in conjunction with the configuration files you learned about in this chapter. To complete this project, you need Internet access and access to the root account on your Linux system. For each of the ping commands described in this project, you only need to let two or three response lines appear to verify that the command works, then press Ctrl+c to interrupt ping and continue with the next step.

+   1. Log in to Linux and open a command-line window.

+   2. Enter su - to change to root access.

+   3. Choose a site that allows you to ping it and execute the ping command to see that it is alive. We’ve used the University of Utah (one of the Internet’s foundational members) as an example:
+   ping www.utah.edu

+   4. As the ping packets are returned, note how the domain name and a corresponding IP address for the site are shown on each line. Write down the IP address.