To keep your system clock synchronized:

+   1. Install the NTP daemon:

```
```
sudo apt install ntp
```
```

+   2. Start and enable the service:

```
```
sudo systemctl start ntp
sudo systemctl enable ntp
```
```

+   3. Check synchronization status:

```
```
ntpq -p
```
```

# IPv6 Configuration

To enable or disable IPv6:

+   1. Edit `/etc/sysctl.conf`:

```
```
# To disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
```
```