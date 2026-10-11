# Tutorial

Find the line starting “net.ipv4_ip_forward=1” and remove the “#” at the start. Now reboot the Pi.

# 10 Setup IPv4 Forwarding

For the next step, you need to run each of these commands individually:

```
```
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```
``` sudo iptables -A FORWARD -i tun0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT```
```

Next, run

```
```sudo nano /etc/rc.local```

Paste the following right above the line reading “exit 0”:
```

```
```
iptables-restore < /etc/iptables.ipv4.nat
/usr/sbin/hostapd /etc/hostapd/hostapd.conf
```
```

# 11 Test Access Point

Run the commands

```
```sudo update-rc.d hostapd enable``` 

and
```

```
```sudo update-rc.d dnsmasq enable```

Reboot the Pi. You'll need a second device at this stage to see if you can access the Wireless AP. Search for it in your network menu and enter the password you created earlier on. If you can't remember this, run
```

```
```sudo nano /etc/hostapd/hostapd.conf```

on the Pi to view it again. Once connected visit www.whatsmyipaddress.com to check you're behind the VPN.
```

# 12 Fix DNS Leaks

Certain VPN providers use their own DNS servers. Other VPN Providers are less cautious. Visit https://www.dnsleaktest.com/ and click Extended Test to check you're safe. If any of the DNS servers match your regular ISP, your connection is not fully secure.

```
To resolve this, edit your VPN configuration file e.g. ```sudo nano /etc/openvpn/vpn2.conf```

and add these lines immediately above “ca”:
```

```
```script-security 2
up /etc/openvpn/update-resolv-conf
down /etc/openvpn/update-resolv-conf```
```

Save and exit, then restart your Pi. Check the DNS leak website once again. If this fails to resolve the issue, try using another VPN provider.

```
```
sudo iptables -A INPUT -i tun0 -m conntrack --state RELATED,ESTABLISHED -j ACCEPT
```
```sudo iptables -A INPUT -i tun0 -j DROP```
```

```
```sudo sh -c “iptables-save > /etc/iptables.ipv4.nat”```

Make sure to save your changes so that they'll apply on reboot:
```

```
```sudo sh -c “iptables-save > /etc/iptables.ipv4.nat”```

```

# 13 Block unsolicited connections

As your Pi is sitting between your computer and the internet, it can potentially be accessed by other devices. Prevent unsolicited incoming connections from other devices with the following commands:

# 14 Route all traffic through OpenVPN

When you boot the Pi initially, certain applications may try to connect directly to the internet, which can undermine your anonymity.

To channel all network traffic through the VPN, you need to edit your configuration file in /etc/openvpn, for instance by running

```
```sudo nano /etc/openvpn/vpn2.conf```

Make sure the line “redirect-gateway” reads “redirect-gateway def1”. DNS queries will also be routed through the VPN also so make sure your provider supports this.
```

# 15 Set up Firewall

Although you may have previously configured iptables to prevent unsolicited incoming connections, to be on the safe side, consider installing ufw (Uncomplicated Firewall) with

```
```sudo apt-get install ufw```

Run
```

```
```sudo ufw enable```
```

```
to fire it up, then open the default OpenVPN port 1194 with ```sudo ufw allow 1194```
```

You may also want to enable Port 22 to allow connecting via SSH. Remember that this doesn't change which ports are open and closed on the router.