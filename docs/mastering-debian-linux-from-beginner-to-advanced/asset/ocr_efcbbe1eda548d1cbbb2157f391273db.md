```
du -sh /home/*
```

+   3. iotop: Monitor I/O usage by processes (may need to be installed)

```
sudo apt install iotop
sudo iotop
```

+   4. smartctl: Check disk health (part of the smartmontools package)

```
sudo apt install smartmontools
sudo smartctl -a /dev/sda
```

# Configuring Network Settings

Proper network configuration is essential for connecting your Debian system to local networks and the internet. This section covers the basics of network configuration in Debian.

# Network Interfaces

Network interfaces are the connection points between your system and the network. Common types include:

+   1. Ethernet interfaces (e.g., eth0, enp0s3)
+   2. Wireless interfaces (e.g., wlan0, wlp2s0)
+   3. Loopback interface (lo)