# ## Set up your Pi Zero

Rasbpian user interface from the previous step. Insert the SD card into your Linux machine and work out what the device is called.

```
```
dmesg | tail -n 3
[ 328516.612884] mmc8: new high speed SDHC card at address 6001.
[ 328516.614337] mmcblk0: mmc:0:6001 SD0BG 7.35 GiB
```

```

So the device is /dev/mmcblk0 – now we need to work out which partition number the root partition is (this will be different on a Raspbian image where we are using a NOOBs image here)

```
```
ls /dev/mmcblk0
sudo parted /dev/mmcblk0 print
```

```

This will give you a list of the partitions. The largest partition will be the root partition. In this case it’s partition 2, so the root filesystem is at /dev/mmcblk0p2. To mount the SD card and edit the wpa_supplicant.conf file do the following:

```
```
sudo mkdir /mnt
sudo mkdir /pi
sudo mount /dev/mmcblk2 /pi
cd /pi
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

```

Then fill in your WiFi details:


etwork={
ssid="your_wifi_network" 
psk="your_wifi_password" 
key_mgmt=WPA-PSK }

Then finally:

cd ..
sudo umount /pi

# ### Remotely access your Pi

1. You can use rmap to scan the local network to find a Raspberry Pi. You need to know the address range of your local network (common network ranges are 192.168.1/24, and 192.168.2/24). You can find it with the ip addr command. rmap -d22 -s/v 192.168.157/24 will scan for a list of devices with an SSH open.

```
```
Host 15.7
Port 0 (0.780s latency):
PORT STATE SERVICE VERSION
22/tcp open ssh (protocol 2.42)
```

```

Then you can SSH in with:

```
sudo ssh 192.168.157.29
The password is "raspberrypi" If you are using the Pi headless, you’ll have to disable the user interface that’s set in by the default:
```

```
sudo systemctl set-default multi-user.target
```


# ### Setup a VNC server

11. VNC stands for Virtual Network Computing. Using VNC you can access the Raspbian desktop over the network (meaning you only need power and Ethernet/WiFi.

> “The minimum that you need connected for a NOOBs install is a monitor and a keyboard”

![](bbox=[0.3, 0.1, 0.6, 0.25])

connected. There is no audio support, but for any other tasks (including the use of pygame) VNC should provide an acceptable level of performance. You can install a VNC server with the following commands.

```
sudo apt-get update
sudo apt-get install tightvncserver
```


There are several free VNC clients available so a search engine will help you find a suitable one. To start a VNC session on your Pi, log in over SSH and then run tightvncserver. You will be prompted to enter a password the first time you run it. You can specify a screen resolution with the -geometry option: for example, -geometry 1024x768. You can kill an existing VNC session with tightvncserver –kill n, where n is the session number. To connect to that session on a Linux machine, you could use the command vncviewer 192.168.157.29: n. Substituting for the IP address of your Raspbian Pi.

# ## Getting started