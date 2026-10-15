called wattcp.cfg. You have to create it inside the c:\vfp directory by opening a new file in the DOS text editor. Type edit wattcp.cfg. A blank editor screen should appear.

# 5. Type the following four lines into the new file exactly as they appear. You will go back and fill in the blanks in the upcoming steps:

```
my_ip=
netmask=
nameserver=
gateway=
```

# 6. After my_ip=, enter an IP address appropriate to the type of virtual Ethernet connection (bridged or host-only). Unfortunately, if you use bridged networking and your LAN uses DHCP, you need to choose an address valid for your network, but unlikely to be assigned to any other computer. If you use host-only networking, the problem is not as severe. In fact, if you are sure you will never run more than one virtual machine at a time, you can simply steal the host-only IP address from a Windows or Linux virtual machine by looking up the information, writing it down, and transferring it to this configuration file.

# 7. After netmask=, enter the netmask for the network the virtual Ethernet card will address. For many bridged LANs, and nearly all host-only configurations, this is 255.255.255.0.

# 8. If you are on a bridged network, enter the address of your primary nameserver after the nameserver= blank. If you have more than one DNS available, create additional nameserver= lines. Unless you are running DNS service on the host PC, this setting is meaningless in a host-only environment.

# 9. If you are on a bridged network, enter the address of your Internet gateway in the gateway= line. For host-only networking, enter the IP address of your Linux PC's vmnet1 adapter. (Throughout the course of the book, I used 192.168.71.1 as an example.)

# 10. Save the file and exit the text editor. The fruit of your labors should resemble Figure 14.15, a sample completed wattcp.cfg file.

> A great many DOS Internet clients rely on the wattcp.cfg file, so once you create it, you can simply copy it into the program directory of other network clients and not worry about configuring them.

# 11. If you're not running the packet driver already, run it now.

# 12. Run the FTP program by typing ftp at the DOS prompt.