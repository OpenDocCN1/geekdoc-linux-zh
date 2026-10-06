# 396 Part III ♦ Choosing and Installing a Linux Distribution

26. Configure system services. Install your system services — system logger, cron service, hotplug, and reisers service — and set the domain name. Then turn on each of these services, as follows:

```
# emerge syslog-ng
# rc-update add syslog-ng default
# emerge vixie-cron
# rc-update add vixie-cron default
# emerge hotplug
# rc-update add hotplug default
# emerge reiserfsprogs
# rc-update add domainname default
```

27. Add special driver support. There may be particular kernel modules required by your computer at this point. For example, if you have a special Ethernet adapter or a special type of video card, use the emerge to install kernel modules now. You may not need any of them. Here are a few examples:

```
# emerge nvidia-kernel
# emerge nforce-audio
# emerge e100
# emerge e1000
# emerge emiu10k
# emerge ati-drivers
```

These command lines are used only if you have special hardware associated with the kernel drivers. respectively, these commands load drivers for accelerated Nvidia video cards, audio for Nvidia Nforce-boards. Intel e100 Fast Ethernet cards, Intel e1000 Gigabit Ethernet cards, Sound Blast/Audiochemy for 2.4 kernel, and ATI Radeon+/FireGL graphics acceleration cards.

28. Add user and information. Add a password for the root user, a regular account name of your choosing (chris in this example), a machine name, and a domain. If you like, you can also edit the /etc/hosts and /etc/rc.conf files to add IP addresses or change the basic startup script.

```
# passwd
# useradd chris -G users,wheel,audio -s /bin/bash
# echo myname > /etc/hostname
# echo mydomain.com > /etc/dnsdomainname
# nano -w /etc/hosts
# nano -w /etc/rc.conf
```

29. Set up networking. Edit the net file, and then run rc-update to add the eth0 interface as the default (Uncomment the line interface eth0="dhcp" to have the network use DHCP to start automatically.)

```
# nano -w /etc/config.d/net
# rc-update add net.eth0 default
```