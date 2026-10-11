
![](img/d6d2a4cd4a2f445e8c9e8079857e2469_67_0.png)

Figure 5: The homepage (left) contains instructions on how to log in to the local ownCloud service. from there to the ownCloud login (2), the top folder in the shared filesystem (3), and the picture folder (4).

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

## Creating the Hotspot

So far, I have not turned the Raspberry Pi Zero into a WiFi access point. Listing 5 shows the necessary commands which, again, you need to run with root privileges. First use the Network Manager command-line tool (ncl) to create an “open” (password-less) network (lines 1–3). Then make it auto-start at boot time (line 4). I also add the command

```
ncll con up lodge
```

to the /etc/rc.local script, just before (not after!) the last line (exit 0). These steps enable the WiFi chip, open a hotspot with SSID lodge and give your Pi an additional IP address of 10.42.0.1. Being offline means requires an unusual configuration for DNS. I use systemd-resolved for very little here: On my machine, it exists simply to connect DNS lookup requests to a different service running on the Rasp Pi. I first install systemd’s DNS resolver via

```
apt install systemd-resolved
```

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_67_1.png)

Figure 6: The lodge access point appears (left). It is recognized as a captive portal allowing the user to sign in (right).

1. One instance runs as a regular daemon, controlled by `systemctl` and using the configuration file `/etc/dnsmasq.d/lodge.conf`. It will be doing DNS only.

2. Another instance is started by NetworkManager doing DHCP only. It does not read `/etc/dnsmasq.conf` or `/etc/dnsmasq.d/lodge.conf`; it starts on the fly from parameters in the `/etc/NetworkManager/system-connections/lodge.nmconnection` (Network Manager format) and `/etc/NetworkManager/dnsmasq-shared.d/lodge.conf` (dnsmasq format) files.

I also need to install the second `dnsmasq` service. Run:

```
apt install dnsmasq
```

Then create a new file `/etc/dnsmasq.d/lodge.conf` with the following two lines:

```
port=5353
address=/#/10.42.0.1
```

Now restart the `dnsmasq` service with

```
systemctl restart dnsmasq
```

you can also remove the `lodge.local` entry from `/etc/hosts` now. The `address=` line will make the DNS server return `10.42.0.1` (the Raspberry Pi’s WiFi IP address) as the answer to all DNS queries. Try it: Running `ping example.com` should return a reply that starts with:

```
64 bytes from lodge.local (10.42.0.1)
```

Finally, I will configure the instance of `dnsmasq` that I started by NetworkManager; it deals with DHCP and hands out IP addresses to clients that connect to my hotspot. Create a file `/etc/NetworkManager/dnsmasq-shared.d/lodge.conf` and add this line:

```
dhcp-option=119, "http://lodge.local".
```

This will inform some WiFi clients about the captive portal mode, and it follows RFC 8910 [7]. It tries to achieve the same goal as my redirect configuration of the Apache server. When this is all put in place, users should see the `lodge` access point and be able to connect to it (Figure 6).

# Conclusion

So there you have it: a user-friendly way for trading files via WiFi on low power (Figure 7). Sometimes convincing people to use a project is the hardest part. I am pleased to report that some extended family members have told me that they’re using it – quite probably for things I never imagined. Some were initially reticent since they didn’t know where the thing came from. In retrospect, I should have put my name on the homepage to inspire a bit of confidence.

If you’re interested in a more complex solution that also grants access to the Internet (where available), you can check out dedicated captive portal solutions, such as Nodogsplash [9] and openNDS [10], but they were not needed for this project.

# Info

-   [1] Raspberry Pi power supply documentation: https://github.com/raspberrypi/documentation/blob/develop/documentation/asclidoc/computers/raspberry-pi/power-supplies.adoc

-   [2] NextPi:
    https://github.com/sky321/nextpi

-   [3] Raspberry Pi Imager:
    https://www.raspberrypi.com/software/

-   [4] SURE: https://sury.org/

-   [5] Adding the SURY repo:
    https://gist.github.com/janus57/
    37b079a383dd0507149bd94d35053d1

-   [6] Captive portal: https://en.wikipedia.org/wiki/Captive_portal

-   [7] RFC 8910
    https://www.rfc-editor.org/rfc/rfc8910

-   [8] Self-signed certificates:
    https://peppe8o.com/self-signed-certificate-https-in-raspberry-pi-with-apache

-   [9] Nodogsplash: https://github.com/nodogsplash/nodogsplash

-   [10] openNDS: https://github.com/openNDS/openNDS

# Author

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_68_0.png)

**Dave McKellar** earned a Computer Science degree in the 1980s from the University of Waterloo, Canada. Since then, he’s worked as a programmer for a variety of companies with Windows and Linux. He enjoys canoeing near the remote cabin mentioned in this article.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_68_1.png)

**Figure 7: The Raspberry Pi sits in a black case and is mounted to the rafter (circled). It is attached to a power supply.**

# MakerSpace-Online

# New Maker Content Every Week

At MakerSpace, we are all about technology you can use to build your own stuff. Our goal is to help you turn your ideas into reality with hands-on projects for makers.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_69_0.png)

Solar-Powered PI Face
Powering your PI face with solar may not solve the current energy crisis, but it will save you from charging or replacing batteries.
by Benford Benford

My idea to add face power to a Raspberry PI was started with a project in the design process, temperature measurements at a one-stop display were added to this project. I used an Adafruit 2.2" LCD by Benford.

Figure 1: A typical solar cell (left), battery (center), and a Raspberry Pi (right) set up with all components attached to the battery and solar cell.

The system runs off a mix of solar, recharges the power supply and life, and then holds back the deep sleep. Figure 2 shows the power flow for the battery 2600 mAh (which is used as a backup). Figure 2 shows a power budget that supports the system at full power. This diagram shows the maximum power draw from the battery, which is the Raspberry Pi's 5V supply. The system uses a small microcontroller to switch on/off the 5V supply from the battery, and to control the charge level of the battery. This is done by a simple circuit that uses the battery's charge level to control a transistor that switches on the charging circuit. The charging circuit is a simple charge pump circuit that uses the solar panel to charge the battery. The charge pump circuit is designed to be efficient, and to be able to charge the battery at a low current, which is important for a small solar panel. The charge pump circuit is also designed to be able to operate at a low voltage, which is important for a small solar panel.

Figure 2: A typical solar cell (left), battery (center), and a Raspberry Pi (right) set up with all components attached to the battery and solar cell.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_69_1.png)

# Fresh Content, Delivered

Subscribe now and join the MakerSpace community. You'll stay up-to-date when new content is published.

**Join Now!**

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_69_2.png)

https://makerspace-online.com

**So many geeks are gamers.** Many Linux users say their first experience with computers was playing those classic old computer games of the 1990s. And of course, many who were born much later still relish the raw simplicity of those old-school games from the DOS space. If retro-gaming is your thing, or if you are curious about what to do with those old gaming CDs and backup files that are taking up space in your attic, you’ll enjoy this month’s tutorial on legacy video game preservation. Also in this month’s Linux Voice, scale up your memorization skills with the Anki flashcard system.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_70_0.png)

# LINUX VOICE

**Doghouse – Stakeholders** 73
Jon "maddog" Hall
The stakeholder approach of open source broadens the pool of who can access, influence, and benefit from information technologies.

**Anki** 74
Marco Fioretti
Flashcards are a fast and effective way to memorize pertinent facts for your next exam. Anki takes this time-honored trick in a direction you never could have imagined in the days of those classic 3x5 cards.

**FOSSPicks** 82
Nate Drake
Nate explores some top FOSS tools, including the latest Gnome desktop, a slick 3D model viewer, LibreQuake, a neat currency converter, and much more.

**Tutorial – Legacy Video Games** 88
Rubén Lorente
People born in the late ‘80s and early ‘90s often have a sizeable collection of old video games gathering dust at home. Systems capable of executing these are, however, becoming scarce. This article explores the options for archiving old PC games and running them on modern systems.

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_70_1.png)
