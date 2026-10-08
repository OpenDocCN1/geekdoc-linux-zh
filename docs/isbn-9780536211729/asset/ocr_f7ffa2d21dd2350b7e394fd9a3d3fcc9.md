ARPWatch shuts off, maybe due to the machine rebooting, the existing entries will be written to a file called `arp.dat` (the location of this file varies greatly; if you need to find it run `find / -name "arp.dat"`). If you need to reset ARPWatch’s monitoring database so that it will “pick up” all the hosts on the network again, run these commands from within the directory in which you locate ARPWatch:

```
rm arp.dat
touch arp.dat
```

A tip about using ARPWatch: Make sure that the ARPWatch data file, `arp.dat`, is monitored for unauthorized changes. If an attacker can alter this file and add his own entry manually, ARPWatch won’t alert you to the presence of the new host. Make sure that the `arp.dat` file is monitored by AIDE or through other similar means.

# ## 11.6 Summary

This chapter showed you some of the tools used in intrusion detection. The goal was to provide you with some hands-on experience based on the concepts introduced in previous chapters. You learned about network sniffers in this chapter and focused specifically on TCPDump. Some packets and attack types were viewed through the eyes of TCPDump as well.

Other tools were introduced and discussed in this chapter as well. These included Snort, which provides an excellent intrusion detection system. Finally, using ARPWatch to monitor for new and unexpected ARP entries on the network was also discussed.