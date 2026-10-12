In the latest Red Hat release, the variable FORWARD_IPV4 has been moved to the /etc/sysctl.conf file. Here several modular options are defined that affect networking. You can still leave the variable defined in /etc/sysconfig/network, but the system will automatically add the variable to the /etc/sysctl.conf file as well.

Here is what a sample entry looks like. Notice that the forward variable is defined although commented out. It is enabled only on the last line.

```
```
# Disables packet forwarding
# net.ipv4.ip_forward = 0
# Enables packet forwarding
# net.ipv4.ip_forward = 1

# Enables source route verification
net.ipv4.conf.all.rp_filter = 1
# Disables automatic defragmentation (needed for masquerading, LVS)
net.ipv4.ip_always_defrag = 0
# Disables the magic-sysrq key
kernel.sysrq = 0
# added by initscripts install on Thu Oct 19 13:46:24 MDT 2000
net.ipv4.ip_forward = 1
```
```

Once you have confirmed that the server is set up correctly, you can start configuring your client box at home or elsewhere. If you are using a Linux box, consult the previous “Setting Up the Dial-Up Server” section. If another machine on your network is using Microsoft Windows, use the provided Dial-Up Networking Tool. Enter in the numbers for the phone number from which your Linux modem is connected. If you are using a valid IP address for your system, be sure to provide the IP addresses of the DNS servers hosting your IP address.

# NOTE

If you experience any problems, check the following files. Look at /var/log/messages.log.1 and /var/log/maillog.log.2 to see what kind of errors are being generated. If that file doesn’t provide enough information, consult the messages in /var/log/messages. Otherwise look through all the files in /var/log.

Turn on the Debug option under the Linux dial-up connection and watch how your modem connects to the other remote modem. I noticed my own machine not sending the correct password for the user I was connecting as and was able to rectify the situation quickly.