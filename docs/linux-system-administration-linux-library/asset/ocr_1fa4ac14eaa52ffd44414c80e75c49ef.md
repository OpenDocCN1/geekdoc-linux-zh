# Initialization and Startup Scripts 159

+   pop-3: on
auth: on
charger: off
charger-udp: off
daytime: off
daytime-udp: off
echo: off
echo-udp: off
time: off
time-udp: off

You can also use Linuxconf to configure services to run. Use the Control Panel ➤ Control Service Activity option on the Control tab. You'll see a list of services. Click one, and you'll be able to set the levels in which the service is active, as shown in Figure 5.5. Linuxconf offers many additional capabilities, so it is worth the time spent learning how it works.

# Tracking Startup Problems

If your system won't start up, the cause could be any of number of things. One common problem is that something is wrong with the LILO installation. Troubleshooting LILO startup problems is tricky for newcomers to Linux because the error messages are cryptic. They do have clear meanings, which Table 5.1 demystifies.

# LI Only

The most common of the LILO errors is the LI message, which means that the secondboot loader has loaded but could not be started. Sometimes this is the result of a disagreement between the BIOS and LILO about the disk parameters. If the number of cylinders, heads, and sectors are not agreed upon, you will see this error. Using the hard drive append line that was described in the lilo.conf section, specify the correct parameters for the drive. If the drive is in BIOS LBA mode, use the linear option in the /etc/lilo.conf.

At other times this is the result of a BIOS limitation, which prevents the /boot partition from booting if it is not contained within the first 1024 cylinders of the disk. As of LILO version 21.4.2, this limitation has been overcome on systems where the BIOS supports EDD BIOS extensions.