
## 05 Test OpenVPN connection

Once the OpenVPN service is running, open a new tab in your Terminal or start a new SSH service and run the command `ifconfig` to list your network interfaces. Usually the VPN connection will appear as `tun0`.

![](img/6866071e033820549b214c239744aaa0_76_0.png)

You can check your apparent location with the command:

```
curl --interface tun0 freegeoip.net/json/
```

Next, make sure the OpenVPN service starts each time you log in. Then run

```
sudo nano /etc/default/openvpn
```

and remove the `#` at the start of the line reading "`#AUTOSTART=`all`".

## 06 Install prerequisites

Now we’ll install the necessary software to set up a Wireless AP. Do this by running

![](img/6866071e033820549b214c239744aaa0_76_1.png)

```
sudo apt-get install dnsmasq hostapd
```

Next, run

```
sudo nano /etc/dhcpd.conf
```

Add these lines to the very bottom of the file:

```
interface wlan0
static ip_address=172.24.1.1/24
```

Press Ctrl+X, Y then Return to save and exit.

![](img/6866071e033820549b214c239744aaa0_76_2.png)

## 07 Set static IP

Open your network interfaces configuration with

```
sudo nano /etc/network/interfaces
```

Change the line "`iface wlan0 inet static`" to "`iface wlan0 inet manual`". Press Return to start a new line, and then paste:

```
address  172.24.1.1
netmask   255.255.255.0
network   172.24.1.0
broadcast 172.24.1.255
```

Place a “#” at the start of the line beginning “wpa-conf”. Save and exit in the same way as before.

Restart the dhcpcd service with

```
sudo service dhcpcd restart
```

## 08 Configure AP

Run

```
sudo nano /etc/hostapd/hostapd.conf
```

![](img/6866071e033820549b214c239744aaa0_76_3.png)

and paste the following:

```
interface=wlan0
driver=nl80211
ssid=PiVPN
hw_mode=g
channel=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_passphrase=raspberry231
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

Feel free to change the name of the network from ‘PiVPN’ to one that is meaningful to you. Similarly change the password ‘raspberry231’ to something more secure.

Next run

```
sudo nano /etc/default/hostapd
```

Find the line starting `#DAEMON_CONF=`“`”` and change to DAEMON_CONF=`“`/etc/hostapd/hostapd.conf`”`. Note the “#” at the start of the line must be removed.

![](img/6866071e033820549b214c239744aaa0_76_4.png)

## 09 Configure dnsmasq

Move the old dnsmasq configuration file with

```
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```

then create a new one by running

```
sudo nano /etc/dnsmasq.conf
```

Paste in the following text:

```
interface=wlan0
listen-address=172.24.1.1
bind-interfaces
server=8.8.8.8
domain-needed
bogus-priv
dhcp-range=172.24.1.50,172.24.1.150,12h
```

Note we are using Google’s DNS server (8.8.8.8) for now; change this if you wish, then save and exit.

Run

```
sudo nano /etc/sysctl.conf
```

## Automatic Login

If you need a username and password for your VPN, you can save these so OpenVPN will connect automatically. First run

```
sudo nano auth.txt
```

On the first line put the username and on the second put your password. Save and exit. Next edit your OpenVPN config file e.g.

```
sudo nano /etc/openvpn/vpn2.conf
```

Scroll down to the line with the text "`auth-user-pass`", leave a space and enter the path auth. txt, for example:

```
auth-user-pass /home/pi/auth.txt
```

Save and exit once again.

Find the line starting “net.ipv4_ip_forward=1” and remove the “#” at the start. Now reboot the Pi.

## 10 Setup IPv4 Forwarding

For the next step, you need to run each of these commands individually:

```
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i tun0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

Next, run

```
sudo nano /etc/rc.local
```

Paste the following right above the line reading “exit 0”:

```
iptables-restore < /etc/iptables.ipv4.nat
/usr/sbin/hostapd /etc/hostapd/hostapd.conf
```

## 11 Test Access Point

Run the commands

```
sudo update-rc.d hostapd enable
sudo update-rc.d dnsmasq enable
```

Reboot the Pi. You'll need a second device at this stage to see if you can access the Wireless AP. Search for it in your network menu and enter the password you created earlier on. If you can't remember this, run

```
sudo nano /etc/hostapd/hostapd.conf
```

on the Pi to view it again. Once connected visit www.whatsmyipaddress.com to check you're behind the VPN.

## 12 Fix DNS Leaks

Certain VPN providers use their own DNS servers. Other VPN Providers are less cautious. Visit https://www.dnsleaktest.com/ and click Extended Test to check you're safe. If any of the DNS servers match your regular ISP, your connection is not fully secure.

To resolve this, edit your VPN configuration file e.g.

```
sudo nano /etc/openvpn/vpn2.conf
```

and add these lines immediately above “ca”:

```
script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf
```

Save and exit, then restart your Pi. Check the DNS leak website once again. If this fails to resolve the issue, try using another VPN provider.

Run the following commands to secure the connection:

```
sudo iptables -A INPUT -i tun0 -m conntrack --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -i tun0 -j DROP
```

Make sure to save your changes so that they'll apply on reboot:

```
sudo sh -c “iptables-save > /etc/iptables.ipv4.nat”
```

## 13 Block unsolicited connections

As your Pi is sitting between your computer and the internet, it can potentially be accessed by other devices. Prevent unsolicited incoming connections from other devices with the following commands.

## 14 Route all traffic through OpenVPN

When you boot the Pi initially, certain applications may try to connect directly to the internet, which can undermine your anonymity.

To channel all network traffic through the VPN, you need to edit your configuration file in /etc/openvpn, for instance by running

```
sudo nano /etc/openvpn/vpn2.conf
```

Make sure the line “redirect-gateway” reads “redirect-gateway def1”. DNS queries will also be routed through the VPN also so make sure your provider supports this.

## 15 Set up Firewall

Although you may have previously configured iptables to prevent unsolicited incoming connections, to be on the safe side, consider installing ufw (Uncomplicated Firewall) with

```
sudo apt-get install ufw
```

Run

```
sudo ufw enable
```

to fire it up, then open the default OpenVPN port 1194 with

```
sudo ufw allow 1194
```

You may also want to enable Port 22 to allow connecting via SSH. Remember that this doesn't change which ports are open and closed on the router.

![](img/6866071e033820549b214c239744aaa0_78_0.png)

The Electronic Frontier Foundation is the leading nonprofit organization defending civil liberties in the digital world. Founded in 1990, EFF champions user privacy, free expression, and innovation through impact litigation, policy analysis, grassroots activism, and technology development. We work to ensure that rights and freedoms are enhanced and protected as our use of technology grows.

## EFF.ORG

## ELECTRONIC FRONTIER FOUNDATION

Protecting Rights and Promoting Freedom on the Electronic Frontier

# Anaconda for the Pi

Python is the language of choice on the Raspberry Pi, and there are many packages available within the Raspbian repository. Berrycconda helps you move out beyond these modules.

![](img/6866071e033820549b214c239744aaa0_79_0.png)

Joey Bernard is a true renaisssance man, splitting his time between building furniture, helping researchers with scientific computing problems and writing Android apps.

## Why Python?

It’s the official language of the Raspberry Pi. Read the docs at python.org/doc.

Python has always been the language of choice for projects on the Raspberry Pi. There are several reasons for this, but we won’t dive into the history here. As a consequence of this decision, there are many Python modules available as packages within the Raspbian package repository. You can trust that these have been compiled to run on the ARM processor and that they have been tested and are therefore safe to use. But not all Python modules are available this way. For the missing modules, the intention is that you could use pip to install them yourself on your Raspberry Pi. While this works fine for some modules, you will eventually start running into those modules that require debugging to figure out why they aren’t working correctly on the ARM processor. The amount of work involved in debugging these types of issues really should be distributed across many people, and luckily it is. For Python coders, a very good distribution of Python modules is available as the Anaconda project. There is also a community part of the Anaconda project, called Berrycconda, which has been ported to the Raspberry Pi. The main website for the project is located at github.com/jihelmus/berrycconda. This article will cover the steps to getting it installed and ready to use on your Raspberry Pi so that we can go on and look at some of the functionality that becomes available to you for Python coding in future articles.

> “The main utility in Anaconda is the conda packaging system”

The very first step is to download and install the core of the Berrycconda system. On the download page, there are installation files for both armh6l (Raspberry Pi 1 or Zero) and armv7l (Raspberry Pi 2 or 3). There are also different versions of the installer for Python 2.X or Python 3.X. This covers all of the options that you might need for your particular project. The installer is actually a shell script, so all you need to do is to make the script executable, and then run it. For example, we can install the Python 3.x version on a Raspberry Pi 1 with the following commands:

```
wget https://github.com/jihelmus/berrycconda/releases/download/v1.0.0/Berrycconda-1.0.0-Linux-armv6l.sh
chmod +x Berrycconda-1.0.0-Linux-armv6l.sh
./Berrycconda-1.0.0-Linux-armv6l.sh
```

By default, this will install the base of an Anaconda environment into the directory berrycconda3 in your home directory. You can change this installation directory during installation in case you want to put it somewhere else. The installer also asks you whether you want to add the path to the binaries to your PATH environment variable. This is generally a good idea. Just remember to exit from the current shell and log back in so that the new path is picked up. Either that, or manually source the initialisation file to get it set.

The main utility within Anaconda is the conda packaging system. Conda provides a very fully featured package management system to handle Python modules and all of the various dependencies that may be required. There is a very good site of documentation available at the website conda.io/docs, covering all of the options and functionality available. The very first thing you will want to do is to keep your current system up to date. You can update individual packages with the command:

```
conda update package-name
```

This command will go out to the internet and figure out what new versions of the given package exist, and if it finds one, it will ask you whether you really want to perform the update. If you want to just see what will be done, you can use the command line option --dry-run to get a display of what commands would be run. If you just want to keep the entire system updated, you can use the following command to handle updating everything:

```
conda update --all
```

To install new packages, you need to first find out what has already been packaged and is available. Because this is a community effort, the selection will vary over time. So you should check before trying to install some packages. You can do that search with the command:

```
conda search some_text
```

This will do a regular expression search of package titles, looking for the given text, and return a list of any available. Sometimes, however, you may get a rather large list returned. If this happens, you can do a more refined search using the usual regex options used in many other UNIX utilities. If you already know the package name, you could use the -f option to force the search to only return exact matches to the text you give it. If the package in question is already installed on your Raspberry Pi, it will have an asterisk beside it for the version installed. When you are ready to install the package you were searching for, you can do so with the following command:

```
conda install ipython
```

This will, by default, install the latest version of the ipython package within the Berrycconda environment. It will also install any missing dependencies, as well as updating any out-of-date dependencies. While the online documentation is great, there are also help pages available within conda. If you want general help, you can get it with the help command. For help with some specific conda commands, you can use something like the following command:

```
conda install --help
```

This is handy for all of the details that
