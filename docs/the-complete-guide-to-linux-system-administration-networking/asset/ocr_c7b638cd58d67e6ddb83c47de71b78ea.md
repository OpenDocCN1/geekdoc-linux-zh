5. Now try to log in to system2 from system1 using the ssh command.
$ ssh system2
Why doesn't this work as expected?

6. Try this command to log in:
$ ssh -l user2 system2

7. Assuming that you don't always want to enter the login name on the remote system (or that you work with several systems and can't keep track of multiple user names), review the man page for ssh to determine how you can set up the ~/.ssh/config file so that you don't have to include the -l user2 parameter when executing ssh. What line would you use in the config file?

8. Close all windows and log out.

# Project 7-2

For this project, you need a running Linux system with root access and Internet access. Beginning with Step 3, think about what the successful completion of each step indicates about your network. To complete the last few steps (as indicated) you need to have your instructor's permission, as these steps may create a heavy load on your network.

+   1. Log in to Linux using a regular user account.

+   2. If you are working in a graphical desktop, open a command-line window. Use the su - command to change to root access. (If you forget the hyphen, you will not have a complete root environment and will not be able to access the needed commands.)

+   3. Run the ifconfig command to view your networking devices. Check that you have both lo and eth0 devices configured. This indicates that you have networking activated and a working Ethernet card. On some systems, a different type of networking device may be shown, such as tr0 for a token ring card.

+   4. Use ping 127.0.0.1 to ping your loopback device. This indicates that networking is correctly configured. If ifconfig shows the lo interface, this step is virtually certain to succeed. Press Ctrl+c to exit the ping command.

+   5. Ping your own IP address, which you saw in the output of the ifconfig command in Step 3 (look at the eth0 interface). This indicates that your Ethernet card has a valid IP address.

+   6. If you are working in a classroom or computer lab, ask your neighbor for his or her IP address, then ping their host. This indicates that the cabling between systems is intact and that nothing is interfering with packets leaving your computer.

+   7. Using the -f option, for flood, ping your neighbor again. This option sends pings as fast as possible. Each period that is printed on your screen after you execute this command indicates one dropped packet (because the host being pinged cannot