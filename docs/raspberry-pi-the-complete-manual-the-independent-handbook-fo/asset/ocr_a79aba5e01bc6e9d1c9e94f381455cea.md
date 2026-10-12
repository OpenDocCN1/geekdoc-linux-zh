# Set up your Pi Zero

Raspbian user interface from the previous step. Insert the SD card into your Linux machine and work out what the device is called

```
dmesg | tail -n 3
[326516.612994] mmc0: new high speed SDHC card at address 0001
[326516.613437] mmcblk0: mmc0:0001 SD08G 7.35 GiB
So the device is /dev/mmcblk0 - now we need to work out which partition number the root partition is (this will be different on a Raspbian image; we are using a NOOBS image here).
```

```
sudo parted /dev/mmcblk0 print
This will give you a list of the partitions.
The largest partition will be the root partition. In this case it’s partition 7, so the root filesystem is at /dev/ mmcblk0p7. To mount the SD card and edit the wpa_supplicant.conf file do the following
```

```
cd /mnt
sudo mkdir pi
sudo mount /dev/mmcblk0p7 pi/

cd pi/
sudo nano etc/fapassuplicant/ wpa_supplicant.conf
Then fill in your Wi-Fi details:
```

```
network={
ssid="your_wifi_network"
psk="your_wifi_password"
key_mgmt=WPA-PSK
}
Then finally
```

```
cd -
sudo umount pi/
## Remotely access your Pi
```

10 You can use nmap to scan your local network to find a Raspberry Pi. You need to know the address range of your local network (common networks are 192.168.1.0/24, and 192.168.3.0/24). You can find it with the ip addr command: nmap -p22 -sV 192.168.157/24 will scan for a list of devices with SSH open. Example output:

```
nmap scan report for 192.168.157.29
Host is up (0.070s latency).
PORT STATE SERVICE VERSION
22/tcp open ssh (Protocol 2.0)
Then you can SSH in with
```

```
ssh pi@192.168.157.29
The password is 'raspberry.' If you are using the Pi headless, you’ll want to disable the user interface that is started on boot by default:
```

```
sudo systemctl set-default multi-user.target
## Setup a VNC server
11 VNC stands for Virtual Network Computing. Using VNC you can access the Raspbian desktop over the network (meaning you only need power and Ethernet/Wi-Fi connected). There is no audio support, but for any other tasks (including the use of pygame) VNC should provide an acceptable level of performance. You can install a VNC server with the following commands
```

```
sudo apt-get install tightvncserver
There are several free VNC clients available so a search engine will help you find a suitable one. To start a VNC session on your Pi, log in over SSH and then run tightvncserver. You will be prompted to enter a password the first time you run it. You can specify a screen resolution with the -geometry option; for example, `-geometry 1024x768`. You can kill an existing VNC session with `tightvncserver -kill 1`, where `1` is the session number. To connect to that session on a Linux machine, you could use the command `vncviewer 192.168.157.29`, substituting for the IP address of your Raspberry Pi
```

# Getting started

![](bbox=[0.45, 0.1, 0.7, 0.25])

> “The minimum that you need connected for a NOOBS install is a monitor and a keyboard”