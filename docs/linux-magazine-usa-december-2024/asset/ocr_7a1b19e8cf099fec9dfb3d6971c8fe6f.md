![](bbox=[0.065, 0.085, 0.92, 0.42])

Figure 5: The homepage (left) contains instructions on how to log in to the local ownCloud service.

from there to the ownCloud login (2), the top folder in the shared filesystem (3), and the picture folder (4).

Note, I’ve only been dealing with the unencrypted HTTP protocol. For HTTPS, see the “What About HTTPS?” box.

and in the [Resolve] section of its configuration file /etc/systemd/resolved.conf I set

```
# Use dnsmasq
DNS=127.0.1.1:5353
```

and then start the service with

```
systemctl start systemd-resolved
```

This will send all requests to a DNS server running on port 5353 on this machine – you’ll see why in a second. Perhaps confusingly, you will be using two different instances of dnsmasq for two different tasks:

# ## Creating the Hotspot

So far, I have not turned the Raspberry Pi Zero into a WiFi access point. Listing 5 shows the necessary commands which, again, you need to run with root privileges. First use the Network Manager command-line tool (ncl) to create an “open” (password-less) network (lines 1–3). Then make it auto-start at boot time (line 4). I also add the command

```
ncll con up lodge
```

to the /etc/rc.local script, just before (not after!) the last line (exit 0). These steps enable the WiFi chip, open a hotspot with SSID lodge and give your Pi an additional IP address of 10.42.0.1. Being offline means requires an unusual configuration for DNS. I use systemd-resolved for very little here: On my machine, it exists simply to connect DNS lookup requests to a different service running on the Rasp Pi. I first install systemd’s DNS resolver via

```
apt install systemd-resolved
```

![](bbox=[0.365, 0.56, 0.92, 0.9])

Figure 6: The lodge access point appears (left). It is recognized as a captive portal allowing the user to sign in (right).