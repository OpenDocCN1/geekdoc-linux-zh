
## Projects

Still handle low-resolution images comfortably for a real-time feed, you should probably use the Raspberry Pi 3.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_0.png)

### Edit the config file

08 To begin configuration, just open motion.conf:
```sudo nano /etc/motion/motion.conf```

Use the CTRL+AW shortcut to open search, find each of the following conditions, adding the values as specified:
```
daemon on
framerate 2
width 640
height 480
ffmpegvideo_codecs mpeg4
stream_localhost off
control_localhost off
```

If you're recording in a dark room, you can adjust the brightness and contrast. With the changes made, hit CTRL+W to exit, confirming with Y and Enter.

### Assign ownership to target directory

09 You may find that the camera stops streaming images after a short time. This is a permissions issue, one that causes a few images to appear on your screen before the whole thing comes to a stop. Overcome this with:
```sudo chown motion: /var/lib/motion```

You can also set a custom file path in motion.conf. Look for target_dir and change as appropriate. Remember to save the file and restart motion when you're done.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_1.png)

### Start and test your baby monitor

10 We now almost have a fully working baby monitor. At this stage, all that is left to get the baby monitor set up and running is to launch the motion:
```sudo service motion start```

You should be able to browse to the feed by entering the IP address of your Raspberry Pi in a mobile browser. This should typically be something like 192.168.0.10:8081

Check this on multiple devices on your home network to confirm that it works.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_2.png)

### Adjust motion detection

11 It's motion detection that will do the bulk of the work in a baby monitor setup. To alter the sensitivity, you need to adjust this for the environment you have set up in the baby monitor set up in, open:
```sudo nano /etc/motion/motion.conf```

And use CTRL+AW to search for "Motion Detection Settings".
Here you'll find various conditions with values that you can adjust, such as threshold and area_detect_value. These will require some patient tweaking for the best results.

### Make motion beep

12 To aid in tweaking the detection, you can enable a beep to sound when movement is captured. As a project this needs some calibration to get the best results, this is a useful feature. Again, this setting is found in motion.conf. Search for "quiet on" and change the setting to read:
```
quiet off
```

Remember to undo this when you're happy with the motion capture, as it may disturb the little one!

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_97_3.png)

### Adjust image quality

13 While you can alter dimensions of the images captured by the PiCam board, it's important to be careful with the figures you enter in motion.conf. For instance, a dimension of 133x342 pixels probably won't work. Dimensions need to be multiples of 4. For larger options, look at 1280x800 or 1920x1080.
Not only will larger images impact bandwidth, they'll make the resulting AVI file larger.

### Get alerts with the Raspberry Pi baby monitor

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_98_0.png)

```
tail -f /var/log/syslog
```
and
```
dmesg | tail
```

This will display any issues that the process is currently having, which is intended to (and hopefully will!) help you diagnose and resolve any problems.

Most issues will be driver-related, so keep this in mind with USB webcams. Press CTRL+Z to end.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_98_1.png)

### Check saved images

14. To confirm the quality of the images captured by the Raspberry Pi baby monitor, boot into the GUI (or install tightv server and remote connect) and browse to /var/lib/motion to see how they are turning out. This should give you the info you need to adjust the dimensions of the captured images.

### Troubleshoot camera connectivity

15. There’s no guarantee that motion will work straight away. If no images are found, or you can’t connect to the stream, run:

### Name your images

16. Images collected by the motion software can be configured with a specific naming convention, based on date and time.

You can find these listed under target_base_directory in motion.conf. For instance, you can specify a folder for new images, based on date:
```
target_base_directory ~/pic%Y%m%d%H%M%S-%t
```
Note the “%” — both directory and images will be named according to date, with images also labelled with the timestamp.

### Go beyond your home network

17. Wouldn’t it be great to monitor your child’s sleep from your favourite restaurant? You can do this by installing the No-IP software on your Raspberry Pi.

This software enables you to get around the fact that your ISP won’t give you a dedicated IP address without paying a hefty premium, by installing a client app that enables you to view the baby monitor outside your home network.

Head to www.noip.com and check their knowledge base for details.

## Build an always-on torrent box

### What you'll need...

- A portable hard drive
- Raspbian
  www.raspberrypi.org/downloads
- PC with a desktop environment with Deluge
  www.deluge-torrent.org

### Get the latest distros, packages and test builds faster with a low-power, mini torrent box

Torrenting your open source software has a number of advantages – it can be faster, alleviates bandwidth and allows you to share back with the community. Distros, packages and more are available via torrents, and the Raspberry Pi makes for a great tiny, low-wattage, always-on torrent box to better manage your files.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_99_0.png)

### Install Raspbian

01 Raspbian works just fine for our torrent box. Install the image on an SD card and go through the basic setup process, making sure to enable SSH in the advanced options and to disable the desktop.

### Remote access

02 Type `ifconfig` into your Pi's command line to find the IP address. At this point you can unplug the monitor and set it up remotely, but either way you can now access the Pi by typing:
```
ssh [user]@[IP address]
```
and entering your password to log in.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_99_1.png)

> "The Raspberry Pi makes for a great tiny, low-wattage, always-on torrent box to better manage your files"

### Mount hard drive

03 Unless you plan to reformat your portable drive, you'll need to install NTFS support onto your Pi. Type in:
```
sudo apt-get install ntfs-3g
```
Add the hard drive to /etc/fstab (open it with `sudo nano /etc/fstab`) by adding the line.

```
/dev/[hard drive address] [mount point] auto_nofail rw 0 0
```
Use `fdisk` to find the name of the instance, and mount `/dev/sdz` (for example, `/dev/sdz`) with mount point `/home/pi/torrents`.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_100_0.png)

### Install Deluge

04 We'll use Deluge for our torrents. Install it with:
```
sudo apt-get install deluge-console
```
Now start and then stop Deluge so it creates a config file we can edit with:
```
deluge
sudo pkill deluged
```
And finally, run the following to copy the config file in case we mess up:
```
cp ~/.config/deluge/auth --config/deluge/default
```

### Basic configuration

05 Edit the file with:
```
sudo nano ~/.config/deluge/auth
```
And add to the bottom:
```
[username]:[password]:10
```
to restrict access.
Now start it up with:
```
deluge-console
```

pi@raspberrypi: # Free-Web-Server-Guide:
```
sudo /etc/init.d/deluge-daemon start
```
[infox] /etc/default/deluge
sudo /etc/init/deluge-daemon.conf
```
echo 'sudo /etc/init.d/deluge-daemon start'
```

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_100_1.png)

### Remote connection

06 Now you're in the client, type the following three commands:
```
config -s allow_remote True
config allow_remote
exit
```
Start the Deluge daemon with:
```
sudo pkill deluged &
deluged
```
Now open the graphical client on your main PC.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_100_2.png)

### Remote interface

07 Go to Edit > Preferences and select Classic Mode and restart Deluge. Click Add on the Connection Manager, and enter the IP in Hostname. Click Connect to see any torrents you have downloading or uploading.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_100_3.png)

### Download location

08 Go to Edit again and then Preferences, and change to the Downloads tab if it's not on there already. Set the download location to the directory we mounted the hard drive to, and enable Auto add torrents; setting it to any destination you plan to dump torrents to the hard drive.

### Start on boot

09 An init script from Ubuntu can be used to have Deluge start on boot. Download it with:
```
sudo wget -O /etc/default/deluge-daemon https://bit.ly/1zNXKiz
```
Open /etc/default/deluge-daemon with nano and change the username to the one we set up earlier. Save it, then download the full init script and update with:
```
sudo wget -O /etc/init.d/deluge-daemon https://bit.ly/1s8d76s
sudo chmod 755 /etc/init.d/deluge-daemon
sudo update-rc.d deluge-daemon defaults
```
