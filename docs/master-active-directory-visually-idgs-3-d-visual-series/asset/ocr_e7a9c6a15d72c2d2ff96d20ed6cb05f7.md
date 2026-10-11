# CHAPTER **2**

TCP/IP BASICS

# ## TCP/IP UTILITIES

TCP/IP contains a number of command line utilities that help you gain information about the TCP/IP configuration of your computer and troubleshoot connectivity problems. The following sections tell you about the three most common utilities.

TCP/IP is functioning properly. If you cannot contact a remote computer, ping is a good way to determine if the computer is “down” or if some other communication problem exists.

# **Ping**

You can use Ping to test connectivity with both your computer and remote computers. Ping enables you to perform a test using a computer’s IP address, NetBIOS name, or DNS name. You can perform a *loopback* test on your own computer to make sure your TCP/IP software is initializing properly. This test checks your computer to make certain TCP/IP is operational. To perform a loopback test, simply type **ping 127.0.0.1** at the

![](bbox=[0.05, 0.53, 0.5, 0.75])

# **Netstat**

Netstat provides TCP/IP statistics and current connection information. This utility is useful to get a close look at your current connections and find out about potential problems. Netstat comes with a number of switches you can use to refine the information returned to you. Simply type **neistat ? at the command line to learn more.**

![](bbox=[0.51, 0.47, 0.96, 0.75])

command line and press Enter. To test a remote computer, type **ping**(IP address, NetBIOS name, or DNS name) **at the command line and press Enter. The ping test to a remote computer checks it to make certain**