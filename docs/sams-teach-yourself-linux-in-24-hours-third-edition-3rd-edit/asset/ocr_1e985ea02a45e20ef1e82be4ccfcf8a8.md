# 2. How can you find out which serial port the kernel found the modem on?

Read the kernel boot message log file with the dmesg command. In Linux, modem devices are usually called ttyS0, ttyS1, ttyS2, and ttyS3. These devices correlate to the COM1 and COM2 names in the MS-DOS world. Some Linux distributions name these serial ports cua0 and cua1.

# 3. When configuring your modem, which connection speed should you select?

You want to select the highest connection speed possible. For a 56K or V.90 modem, you can select a connection speed as high as 115200. Those with a 28.8 or 33.6 modem should select a speed of 57600.

# 4. What files do you need to configure a PPP dialup connection using a shell script?

There are three shell scripts that belong in the /etc/ppp directory: ppp-on, ppp-dialup, and ppp-off. The only file in this group that you need to edit is ppp-on. You also need a program called chat to execute the interaction between the modem and the ISP. The chat program is usually found in /usr/sbin/chat. Another file that you will need to edit is /etc/resolv.conf. This file contains the DNS addresses used by your ISP.

# Exercises

1. Look for other ways to create a dialup connection to your ISP. You might also want to look for some tools to help you monitor the connection and control the connection while you are on a search. You may want to start at metalab.unc.edu/pub/Linux/system/serial//INDEX.html.

2. After you have created the ppp-on script to connect to your ISP and you are satisfied that it works, you can move a copy of the file (or create a symbolic link to the file) to either the /usr/bin or the /usr/sbin directory. By doing this, every user on the system (not just the superuser) can connect to the Internet by just typing ppp-on at the command line. You'll also want to move a copy of the ppp-off script so that users can turn off the Internet connection.