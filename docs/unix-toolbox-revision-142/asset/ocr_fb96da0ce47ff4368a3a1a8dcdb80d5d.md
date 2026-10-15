# gateB is on Linux

```
gateA# ssh -w5:5 root@gateB
gateB# ifconfig tun5 10.0.0.1 netmask 255.255.255.252  # Executed on the gateB shell
gateB# route add -net 192.168.51.0 netmask 255.255.255.0 dev tun5
gateB# echo 1 > /proc/sys/net/ipv4/ip_forward      # Only needed if not default gw
gateB# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

# gateB is on FreeBSD

```
gateA# ssh -w5:5 root@gateB      # Creates the tun5 devices
gateB# ifconfig tun5 10.0.0.1 10.0.0.2   # Executed on the gateB shell
gateB# route add 192.168.51.0/24 10.0.0.1,2
gateB# sysctl net.inet.ip.forwarding=1   # Only needed if not default gw
gateB# natd -s -m -u -dynamic -n fxp0    # see NAT (page 17)
gateB# sysctl net.inet.ip.fw.enable=1
```

# Configure gateA

Commands executed on gateA:

# gateA is on Linux

```
gateA# ifconfig tun5 10.0.0.2 netmask 255.255.255.252
gateA# route add -net 192.168.16.0 netmask 255.255.255.0 dev tun5
gateA# echo 1 > /proc/sys/net/ipv4/ip_forward
gateA# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

# gateA is on FreeBSD

```
gateA# ifconfig tun5 10.0.0.2 10.0.0.1
gateA# route add 192.168.16.0/24 10.0.0.1,2
gateA# sysctl net.inet.ip.forwarding=1
gateA# natd -s -m -u -dynamic -n fxp0      # see NAT (page 17)
gateA# sysctl net.inet.ip.fw.enable=1
```

The two private networks are now transparently connected via the SSH VPN. The IP forward and NAT settings are only necessary if the gates are not the default gateways. In this case the clients would not know where to forward the response, and nat must be activated.

# 7 RSYNC

Rsync can almost completely replace cp and scp, furthermore interrupted transfers are efficiently restarted. A trailing slash (and the absence thereof) has different meanings, the man page is good... Here some examples:
Copy the directories with full content:

```
# rsync -a /home/colin/ /backup/colin/      # "archive" mode. e.g keep the same
# rsync -a /var/ /var_bak
# rsync -aR --delete --during /home/user/ /backup/   # use relative (see below)
```

Same as before but over the network and with compression. Rsync uses SSH for the transport per default and will use the ssh key if they are set. Use "..." as with SCP. A typical remote copy:

```
# rsync -axSzrv /home/user/ user@server:/backup/user/   # Copy to remote
# rsync -a 'user@server:My\ Documents' 'My\ Documents'   # Quote AND escape spaces for the remote sh
```

Exclude any directory tmp within /home/user/ and keep the relative folders hierarchy, that is the remote directory will have the structure /backup/home/user/. This is typically used for backups.

```
# rsync -aZR --exclude=tmp/ /home/user/ user@server:/backup/
```

# Use port 20022 for the ssh connection:

```
# rsync -az -e 'ssh -p 20022' /home/colin/ user@server:/backup/colin/
```

Using the rsync daemon (used with ":") is much faster, but not encrypted over ssh. The location of /backup is defined by the configuration in /etc/rsyncd.conf. The variable RSYNC_PASSWORD can be set to avoid the need to enter the password manually.