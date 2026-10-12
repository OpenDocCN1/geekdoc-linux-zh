# Projects

# Build an always-on torrent box

# What you’ll need...

+   *   A portable hard drive
+   *   **Raspbian**
+       www.raspberrypi.org/downloads
+   *   **PC with a desktop environment with Deluge**
+       www.deluge-torrent.org

# Build an always-
on torrent box

Get the latest distros, packages and test builds faster with a low-power, mini torrent box

Torrenting your open source software has a number of advantages – it can be faster, alleviates bandwidth and allows you to share back with the community. Distros, packages and more are available via torrents, and the Raspberry Pi makes for a great tiny, low-wattage, always-on torrent box to better manage your files.

![](bbox=[0.05, 0.48, 0.48, 0.8])

# Install Raspbian

+   1.  Raspbian works just fine for our torrent box. Install the image on an SD card and go through the basic setup process, making sure to enable SSH in the advanced options and to disable the desktop.

# Remote access

+   2.  Type ifconfig into your Pi’s command line to find the IP address. At this point you can unplug the monitor and set it up remotely, but either way you can now access the Pi by typing:

```
```bash
$ ssh [user]@[IP address]
```
```

...and entering your password to log in.

![](bbox=[0.58, 0.87, 0.93, 0.95])

> “The Raspberry Pi makes for a great tiny, low-wattage, always-on torrent box to better manage your files”