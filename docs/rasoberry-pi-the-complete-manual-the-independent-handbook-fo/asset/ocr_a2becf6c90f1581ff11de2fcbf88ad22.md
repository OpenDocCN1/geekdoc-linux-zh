# Projects

# Get alerts with the Raspberry Pi baby monitor

# Survey the bedroom

**01** Before you start installing and configuring your Pi, head to the baby’s bedroom and take a look around. Where will you be placing the Raspberry Pi? Is it within reach of a power source? Do you need to connect an Ethernet cable, or is the wireless signal strong enough? It’s vital at this stage to spend the necessary time planning the Pi’s position in relation to power sources and network connectivity.

# Enable the camera

**02** If you’re using the PiCam, this can be disabled by default. You can enable it in the raspi-config tool. This can be accessed in the GUI by opening Menu > Preferences > Raspberry Pi Configuration, where you should select the Interfaces tab and switch Camera to Enabled. Alternatively run sudo raspi-config and choose option 6, Enable. CameraFor USB webcams, use

```
sudo apt-get install fswebcam
```

And test with

```
fswebcam shot.png
```

# Test the camera

**03** You don’t want to set this project up to find that the camera doesn’t actually work. Whether you’re using a USB webcam or the PiCam, you’ll need to run a command to test the camera.

To confirm, use the GUI to browse to `/home/pi` and view the `image.jpg` file.

This is preferable to checking in the command line, as you can ensure the image is not corrupt.

# Install motion

**04** The motion capture software, motion, can be installed after an update and upgrade of the Raspberry OS.

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install motion
```

Older versions of motion will not start automatically, and display the “Not starting motion daemon” error message. To avoid this, you need to make sure you run the update and upgrade commands. If you’re using the PiCam module, you’ll also need a driver:

```
sudo apt-get install motion libcamera-client0.1 libcamera0.1
```

# Activate PiCam driver

**05** To activate the PiCam driver, you need to enter the following command:

```
sudo modprobe brcm2835-v4l2
```

This enables the PiCam to communicate with third party apps, such as motion. However, if you reboot, unless you add it to `/etc/rc.local`: Open the file in `/etc`

```
sudo nano /etc/rc.local
```

Find an empty line before exit “0” and enter

```
modprobe bcm2835-v4l2
```

Then CTLR-\* to exit, and Y to save.

# Auto-start motion

**06** Begin by opening the `motion` configuration file.

```
sudo nano /etc/default/motion
```

Here, we need to instruct the software to start each time the Raspberry Pi boots. Find the value ‘daemon off’, and change it to read

```
daemon on
```

Hit CTLR-\* to exit, tapping Y to confirm you wish to save the file, and Enter to continue. Next, confirm the motion daemon works on a reboot by restarting your Pi

```
sudo reboot
```

# Configure motion

**07** The next step is to configure the motion software. This means setting the frame-rate (how often an image is captured), image dimensions (bigger images will take up more resources, thereby slowing the monitor) and setting the video format! How you configure motion really depends on which model of Raspberry Pi you will be using for this project. First generation devices will