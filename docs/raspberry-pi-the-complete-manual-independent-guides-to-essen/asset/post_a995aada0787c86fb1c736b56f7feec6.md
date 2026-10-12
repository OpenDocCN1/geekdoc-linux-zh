
## Projects

### Build an Onion Pi and browse privately

#### What you'll need...

- Raspi
  - http://raspberry-ai.org/downloads
- Compatible Wi-Fi adaptor
  - http://adafruit.com/products/814

### Build an Onion Pi and browse privately

> Turn your Raspberry Pi into a highly secure and very portable router to keep safe and anonymous...

Elsewhere in this book we've shown you how to turn your Raspberry Pi into the ultimate portable wireless router, requiring very little power and giving you a wireless network wherever there's the most basic of internet connections. What if it's not enough to know you can search the web, though? What if you want to be wholly secure as you do it? Then it's time to upgrade the router with Tor to protect your privacy on the internet.

This 'Onion Pi', as dubbed by Adafruit, combines Raspbian and Tor to create and secure a wireless access point using just a Raspberry Pi. This will keep you anonymous online - a handy feature in a time of privacy concerns all around the web.

When the Pi is not connected to the internet, it should still function as a wireless router.

#### Did you know...

There is much interest in internet security today due to the actions of some government agencies

#### It's all software

This isn't a hardware hack - a spare SD card can be used for Tor router, and other SD cards can be used for different functions without any problems

#### Safety first

Using our built more than a Raspberry Pi, you can route more of your systems through Tor-enabled access point, guaranteeing anonymity

#### Wi-Fi enabled

Connect everything over a wireless network - no need to directly connect to the Pi with a cable

#### Ethernet needed

Hook into the internet just about anywhere there's an internet connection - a relative's house, hotel rooms and more

![](img/59caadfa348382a5c408c25137901e27_115_0.png)

![](img/59caadfa348382a5c408c25137901e27_116_0.png)

![](img/59caadfa348382a5c408c25137901e27_116_1.png)

#### Install Raspbian

**01** Raspbian is the Raspberry Pi distro we'll be using for the Onion Pi. Download the zip file, extract the image and then apply it to an SD card using:

```
$ dd bs=4M if=Raspbian[version].img of=/dev/[SD card location]
```

You can also use NOOBS to install Raspbian if you wish.

#### Set up Raspbian

**02** Go through the initial Raspbian setup and make sure to turn on the SSH server, and to disable autologin to desktop – this is unnecessary and will only use extra power. You can also tell it to fill up the rest of the card if there's room for it.

#### Pi IP

**03** We'll be accessing your Raspberry Pi via SSH to set it up. To do this we need to know its IP address – you can find it by typing `ifconfig` into the command line. Make a note of it and turn off your Pi.

#### SSH connection

**04** Plug your USB wireless adapter into the Pi and turn it back on. On another computer connected to the same network, open a terminal or type into the command line:

```
$ ssh [user]@[IP address]
```

Then enter the password for your Raspbian Pi if it asks for it.

#### Install DHCP

**05** To make life easier for any system connecting to the Pi access point, we need to install a DHCP server on it. We do this with:

```
$ sudo apt-get install hostapd isc-dhcp-server
```

DHCP will automatically assign IP addresses to network-attached devices, meaning you won't need static IPs.

#### Set up DHCP

**06** Now we need to configure the DHCP server. Edit the configuration file with:

```
$ sudo nano /etc/dhcp/dhcp.conf
```

And start by putting a # in front of the two option domain-name entries, then remove the # in front of authoritative, server lines down.

![](img/59caadfa348382a5c408c25137901e27_116_2.png)

#### Server address

**07** At the end of the configuration file, add the following:

```
subnet 192.168.42.0 netmask 255.255.255.0 {
    range 192.168.42.10 192.168.42.55;
    option broadcast-address 192.168.42.255;
    default-lease-time 600;
    max-lease-time 7200;
    option domain-name "local";
    option domain-name-servers 8.8.8.8, 8.8.4.4;
}
```

Save and exit.

![](img/59caadfa348382a5c408c25137901e27_116_3.png)

#### DHCP server

**08** Edit the server configuration file so that it's set to work in conjunction with the wireless adapter:

```
$ sudo nano /etc/default/isc-dhcp-server
```

Scroll to INTERFACES= and change it to:

```
INTERFACES="wlan0"
```

#### Incoming Wi-Fi

**09** We need to set up the Wi-Fi adapter to be both static and accept incoming signals. First:

```
$ sudo nano /etc/network/interfaces
```

Put a # in front of iface wlan0 and following lines with wpa-roam, iface default and any other facing wlan0.

#### Static IP

**10** Now give the wireless interface a static IP – after the line allow-hotplug wlan0, enter the following:

```
iface wlan0 inet static
    address 192.168.42.1
    netmask 255.255.255.0
```

Save and exit, then set wlan0’s address with:

```
$ sudo ifconfig wlan0 192.168.42.1
```

![](img/59caadfa348382a5c408c25137901e27_117_0.png)

#### WLAN creation

**11** We need to create a new file that holds all the information for our wireless network. We are going to make it password protected so that only the people we want to can access it. To create the file, start with:

```
$ sudo nano /etc/hostapd/hostapd.conf
```

Once this is complete you can continue to the next step...

> “The Onion Pi combines Raspbian and Tor. This will keep you anonymous online. A handy feature in a time of privacy concerns all around the web”

#### WLAN configuration

**12** Assuming you’ve followed step 11 to open hostapd.conf: Write:

```
interface=wlan0
driver=rtl8192x
ssid=<access point name>
hw_mode=e
channel=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=<password>
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

#### Hostapd

**13** After saving and exiting, we need to edit hostapd to point it to this new file. Open it with:

```
$ sudo nano /etc/default/hostapd
```

And then find the line #DAEMON_CONF="". Remove the #, and change it to:

```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

#### Network addressing

**14** Setting up a NAT will allow multiple clients to connect. To do this, open a terminal window (if one isn’t already open) and type the following:

```
$ sudo nano /etc/sysctl.conf
```

And add to the bottom of the file:

```
net.ipv4.ip_forward=1
```

Save, exit, and then finish by running:

```
$ sudo sh -c 'echo 1 > /proc/sys/net/ipv4/ip_forward'
```

#### IP tables

**15** Run the following three commands to make sure the internet connection is forwarded correctly. Make sure you copy them carefully into the terminal.

```
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
```

#### Apply configuration

**16** So that this still continues to work even after the Raspberry Pi has been rebooted, Type:

```
$ sudo sh -c 'iptables-save > /etc/iptables.ipv4.nat'
```

Then add to the end of /etc/network/interfaces:

```
Up iptables-restore < /etc/iptables.ipv4.nat
```

#### Wi-Fi final

**17** Finally, set it up as a daemon so it runs at boot with the following commands:

```
sudo service hostapd start
sudo service isc-dhcp-server start
sudo update-rc.d hostapd enable
sudo update-rc.d isc-dhcp-server enable
```

And the wireless access point part will be finished.

#### Install Tor

**18** After a reboot, we now need to install Tor. Do this simply with:

```
$ sudo apt-get install tor
```

Once it’s installed, you need to edit the Tor config file with:

```
$ sudo nano /etc/tor/torrc
```

Follow the next step to add all the necessary information to it.

![](img/59caadfa348382a5c408c25137901e27_118_0.png)

#### Tor configure

**19** Put this below the FAQ comment:

```
Log notice file /var/log/tor/notices.log
VirtualAddrNetwork 10.192.0.0/10
AutomapHostsSuffixes .onion, .exit
AutomapHostsOnResolve 1
TransPort 9040
TransListenAddress 192.168.42.1
DNSPort 53
DNSListenAddress 192.168.42.1
```

#### Table flush

**20** Now we need to flush the current IP tables so that we can get the routing to go through.

```
$ sudo iptables -F
$ sudo iptables -t nat -F
```

If you want to keep SSH open to connect remotely, you’ll need to make an exception for that with:

```
$ sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp -dport 22 -j REDIRECT --to-port 22
```

#### Reroute

**21** Route all DNS traffic first, using the following commands:

```
$ sudo iptables -t nat -A PREROUTING -i wlan0 -p udp -dport 53 -j REDIRECT --to-port 53
```

And then route any TCP traffic with:

```
$ sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --syn -j REDIRECT --to-ports 9040
```

![](img/59caadfa348382a5c408c25137901e27_118_1.png)

#### Check and save

**22** You can check the table setup with the following terminal command. You’ll need to save it if it works so read on:

```
$ sudo iptables -t nat -L
```

If you’re happy with it, save it to the NAT file like before with:

```
$ sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
```

#### Logging

**23** We should create a log file. This is important in case you use these three commands.

```
$ sudo touch /var/log/tor/notices.log
$ sudo chown debian-tor /var/log/notices.log
$ sudo chmod 644 /var/log/tor/notices.log
```

You can also check it with:

```
$ ls -l /var/log/tor
```

#### Secure the router

**24** Finally, we can activate the Tor service so that we can start using the access point securely with:

```
$ sudo service tor start
```

You can check that it’s you with:

```
$ sudo service tor status
```
