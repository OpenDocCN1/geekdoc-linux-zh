![](bbox=[0.12, 0.1, 0.72, 0.33])

> Thanks to the miracle of NAT, packets can traverse the murky marshes of our internal network, negotiate all kinds of perils in the 192 plains and soar amongst the cloud birds of the wider internet.

the external interface of the gateway (eg the one connecting to your ISP-supplied router) as ext0, and the internal interface (the one connecting to the switch) as int0. So you'll have to make your own substitutions.

RFC1918 provides a few standard IPv4 addresses that can only be used for internal networks, eg 10.x.x.x, 172.16.x.x, 192.168.x.x, so let's go with the first format. We can be a bit more specific here, so let's stipulate that all our internal IPs are in the form of 10.0.1.x. This is usually written 10.0.1.0/24 ie a 24-bit netmask (255.255.255.0). We'll set up the gateway machine's Ethernet interface manually, with the static IP address 10.0.1.254. Depending on how your machine is set up, this might be achieved through Network Manager, the ifconfig or ip commands, making a netctl (Arch Linux) script, editing /etc/network/interfaces (Debian). Whatever you choose, it should be straightforward, and also not interfere with the gateway machine's existing internet connection.

We could do this for all the machines on our network, but it's easier to use the dnsmasq program, which provides a simple DHCP server to allocate addresses. This program will also be useful later since it will enable the gateway machine to masquerade as a DNS server (hence the program's name).

Installing dnsmasq will just be a matter of
$ sudo apt-get install dnsmasq
or whatever is your distribution's equivalent command is. This will install a heavily-commenteded /etc/dnsmasq.conf file which we shall tweak to our requirements. It's good practice to add the following lines right after their commented equivalents, so that options are sensibly grouped. We'll first set up our ersatz DNS server to listen to requests from our fledgling internal network. Add the following line to /etc/dnsmasq.conf:
listen-address=10.0.1.254

We'll also set up our DHCP server while we've got this file open. It's going to allocate addresses in the range 10.0.1.128 to 10.0.1.253, this way addresses with a lower final octet can be reserved for machines on the internal network which need static IPs. It's also possible to have DHCP assign specific addresses to specific machines based on their MAC address, using the dhcp-host option:
dhcp-range=10.0.1.128, 10.0.1.253, 12h

Now start the dnsmasq service with
$ sudo systemctl start dnsmasq
or if you're not running systemd:

# Quick tip

Basic forwarding, routing and masquerading can now be carried out via systemd's networking daemon, networkd. Is nothing sacred? We're taking bets on what its next trick will be. Our money's on Siri-stemd: "Siry, can I have my init scripts back, please?" No! – ED.

# Hotspots with hostapd

On Debian (and friends) sudo apt-get install hostapd will install, besides the hostapd program, a gzipped sample configuration file which you can peruse with:
$ zcat /usr/share/doc/hostapd/examples/hostapd.conf.gz | less

Other distros will install a similar file, probably in another place. This file is heavily commented and gives examples for setting up all manner of access points. We'll only need a few options to get our hotspot up and running, so rather than edit the example file, we'll start afresh. Hostapd needs to know where to find this file so edit /etc/default/hostapd and add the line:
DAEMON_CONF="/etc/hostapd/hostapd.conf"
This is a sane place to put the file and may already be the default on your distribution.

Before we proceed any further, make sure that you know the name of your wireless interface (you can check this with ifconfig). For this section we'll refer to the wireless network as wlan0 and the wired external network as eth0. A basic WPA2 password protected network is set up with the following /etc/hostapd/hostapd.conf file:
ssid=LXFwireless
wpa_passphrase=secret passphrase
interface=wlan0
auth_algs=3
channel=6
driver=nl80211
hw_mode=g
logger_stdout=-1
logger_stdout_level=2

max_num_sta=5
rsn_pairwise=CCMP
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP
The driver option might require some trial and error – most hardware will work with the nl80211 driver, but you might need something else here. Test your hostapd configuration using the following:
$ sudo hostapd -d /etc/hostapd/hostapd.conf
If you don't see any errors, then try and connect to your hotspot with your phone. It probably won't get anywhere since there's no DHCP service at this stage, but you should at least be able to authenticate. We'll get DHCP for free once we set up our network bridge.