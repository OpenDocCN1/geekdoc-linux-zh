1. One instance runs as a regular daemon, controlled by `systemctl` and using the configuration file `/etc/dnsmasq.d/lodge.conf`. It will be doing DNS only.

2. Another instance is started by NetworkManager doing DHCP only. It does not read `/etc/dnsmasq.conf` or `/etc/dnsmasq.d/lodge.conf`; it starts on the fly from parameters in the `/etc/NetworkManager/system-connections/lodge.nmconnection` (Network Manager format) and `/etc/NetworkManager/dnsmasq-shared.d/lodge.conf` (dnsmasq format) files.

I also need to install the second `dnsmasq` service. Run:

```
```
apt install dnsmasq
```
```

Then create a new file `/etc/dnsmasq.d/lodge.conf` with the following two lines:

```
```
port=5353
address=/#/10.42.0.1
```
```

Now restart the `dnsmasq` service with

```
```
systemctl restart dnsmasq
```
```

you can also remove the `lodge.local` entry from `/etc/hosts` now. The `address=` line will make the DNS server return `10.42.0.1` (the Raspberry Pi’s WiFi IP address) as the answer to all DNS queries. Try it: Running `ping example.com` should return a reply that starts with:

```
```
64 bytes from lodge.local (10.42.0.1)
```
```

Finally, I will configure the instance of `dnsmasq` that I started by NetworkManager; it deals with DHCP and hands out IP addresses to clients that connect to my hotspot. Create a file `/etc/NetworkManager/dnsmasq-shared.d/lodge.conf` and add this line:

```
```
dhcp-option=119, "http://lodge.local".
```
```

This will inform some WiFi clients about the captive portal mode, and it follows RFC 8910 [7]. It tries to achieve the same goal as my redirect configuration of the Apache server. When this is all put in place, users should see the `lodge` access point and be able to connect to it (Figure 6).

# Conclusion

So there you have it: a user-friendly way for trading files via WiFi on low power (Figure 7). Sometimes convincing people to use a project is the hardest part. I am pleased to report that some extended family members have told me that they’re using it – quite probably for things I never imagined. Some were initially reticent since they didn’t know where the thing came from. In retrospect, I should have put my name on the homepage to inspire a bit of confidence.

If you’re interested in a more complex solution that also grants access to the Internet (where available), you can check out dedicated captive portal solutions, such as Nodogsplash [9] and openNDS [10], but they were not needed for this project. ■■■

# Info

+   [1] Raspberry Pi power supply documentation: https://github.com/raspberrypi/documentation/blob/develop/documentation/asclidoc/computers/raspberry-pi/power-supplies.adoc

+   [2] NextPi:
+   https://github.com/sky321/nextpi

+   [3] Raspberry Pi Imager:
+   https://www.raspberrypi.com/software/

+   [4] SURE: https://sury.org/

+   [5] Adding the SURY repo:
+   https://gist.github.com/janus57/
+   37b079a383dd0507149bd94d35053d1

+   [6] Captive portal: https://en.wikipedia.org/wiki/Captive_portal

+   [7] RFC 8910
+   https://www.rfc-editor.org/rfc/rfc8910

+   [8] Self-signed certificates:
+   https://peppe8o.com/self-signed-
+   certificate-https-in-raspberry-pi-with-
+   apache

+   [9] Nodogsplash: https://github.com/
+   nodogsplash/nodogsplash

+   [10] openNDS: https://github.com/
+   openNDS/openNDS

# Author

![](bbox=[0.84, 0.68, 0.95, 0.81])

**Dave McKellar** earned a Computer Science degree in the 1980s from the University of Waterloo, Canada. Since then, he’s worked as a programmer for a variety of companies with Windows and Linux. He enjoys canoeing near the remote cabin mentioned in this article.

![](bbox=[0.08, 0.4, 0.36, 0.81])

**Figure 7: The Raspberry Pi sits in a black case and is mounted to the rafter (circled). It is attached to a power supply.**