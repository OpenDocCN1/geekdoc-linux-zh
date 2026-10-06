
# Full code listing

photo, ensure that your Pi's clock is set correctly before you start your program.

```python
import time
import os
import picamera
import subprocess
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)
# Setup the PIR
PIR = 7
GPIO.setup(PIR, GPIO.IN)
# Setup the LEDPAROL
GPIO.output(10, GPIO.OUT)

global file_name = # number of photo
global file_name = # name of photo
File_Number = 1

def detect_self(): # takes a photo of the beast
global File_Number
global current_time
time_of_photo = time.asctime(time.localtime(time.time()))
GPIO.output(10, GPIO.HIGH)
with picamera as camera:
    camera.start_record()
    time.sleep(5)
    camera.capture("Nature" + str(File_Number) + ".jpg")
    file_name = "Nature" + str(File_Number) + ".jpg"
    File_Number = File_Number + 1
GPIO.output(10, GPIO.LOW) # Turn off LEDPAROL
```

time_of_photo = time.asctime(time.localtime(time.time()))

## 12 Add the time to the picture
Recording the time a picture is taken is relevant if you are watching and waiting for wildlife to trigger the camera, and you can see the time value. A better solution is to add a "time stamp" to the picture. This means when you view the image you see the time. The line of code added is camera.annotate = "time".

## 13 Recap
Before you finish, a quick recap on the features and setup: the PIR module is attached to the Pi in the dark. This requires an infrared light source, which is provided by the LEDPAROL. A PIR attached is used to sense changes in heat, which turns the LED and triggers the camera to capture a picture. The current time is recorded for future reference. The caption on the pages showing views for the LEDPAROL and PIR are

## 14 Taking a video
If you would prefer to take a video when the PIR is triggered, you could adapt the program to record video of wildlife that might visit your garden. For example, you could change the code to record video using the camera.start_recording("/home/desktop/video.avi"). If you want to record for say, 20 seconds, use time.sleep(20) before stopping the recording with camera.stop_recording("/home/desktop/video.avi").

```python
camera.start_preview()
camera.start_recording('/home/desktop/video.h264')
time.sleep(5)
camera.stop_recording()
```

## 15 Automatically start your project
The project you have built can run without a monitor or screen, meaning that you can want the program to start. To do this, set the program to start automatically when the power supply is plugged in. You will have to add a line to your script, for example, in the /home/name/Night_Box.py file. Double-check if you'd use /home/name/Night_Box.py to get the correct path by the Terminal and command.

```bash
sudo nano /home/name/of_your_script.py
```

If correct, this will display the contents of your Python code. The next step is to create a job by modifying the 'cron'. To do this, use crontab -e (which will run the task for all users). Scroll to the top of the window and add the following line to:

```bash
@reboot python /home/name/of_your_program.py &
```
The @ at the end will run code in the background and ensure your Raspberry Pi will boot up as normal. Save the file by hitting Ctrl+X followed by Y, and then reboot.

## 16 Deploy the Box
To deploy the setup effectively you will want to create a box or holder for the PIR, LEDPAROL. This will protect the equipment from getting damaged if it rains or blows. You may want to create a 3D-printed structure for the components. In the previous step you used a scheduled cron to start the program automatically when the Raspberry Pi is booted. Choose a suitable location and set up your box. Start the program and check back the next day to see what visits your garden present!

![](img/a54b3b473771472dd2321dd1014be1_66_0.png)

# Tutorial

# Build an iBeacon with a Bluetooth dongle

# Get grips with Apple's iBeacon technology using your Raspberry Pi as a DIY PiBeacon

The 2002 movie Minority Report, based on Philip K Dick novel, is set in a dystopian future, where dreams before they happen and adverts are targeted individuals based on their identity and habits. It was seen as one of many futuristic elements, but fast-forward to 2015, and that is advertising here.

### 01 Prepare your Pi
To set Raspberry Pi up as a PiBeacon, begin with a fresh, updated version of Raspberry OS, perhaps using upgrade commands. Follow the instructions on the update and ensure that Raspberry is fully up to date. When done, you can proceed to install the libraries required for the PiBeacon project.

With Bluetooth Beacon, Apple uses Bluetooth and an iPhone 4 or later in proximity to trigger an app. Google, meanwhile, has its own version, and Raspberry developers investigate this technology with the addition of a low-cost Bluetooth Low Energy (BLE) USB module, available at bit. It will take a little bit of time to download and install. Once the libraries are installed, however, you'll be able to set up Bluetooth.

![](img/a54b3b473771472dd2321dd1014be1_67_0.png)

### 02 Set up Pi with Bluetooth
You've got a Bluetooth dongle already, but before connecting, ensure that it is the correct type (see Bluetooth devices on the right). Using a standard Bluetooth dongle for this project will result in a lot of wasted time and frustration.

### What you'll need
- Bluetooth Low Energy device
- Android/iOS device
- Android/iOS beacon app
- BlueZ

Above Beacons can trigger a number of actions on your smartphone as you close to them.

![](img/a54b3b473771472dd2321dd1014be1_67_1.png)

### 03 Build BlueZ
Extract the archive and configure the system. The node `sudo make` will take some time to complete, and when done, input `sudo make install`. If the Raspberry Pi is unresponsive, just wait.

# Bluetooth
Bluetooth Low Energy (BLE) device is the key to success with this project. Old USB Bluetooth dongles that you might have will work. For best results, check the order from the version repository.

Once it is done, you'll need to restart your Pi with `sudo reboot`. Wait for the power light to go on, and then connect the Bluetooth over-USB dongle:

### 04 Configure for Broadcast
Once you're happy with the device, create a new directory for BlueZ (the Linux stack), switch to that directory and download BlueZ: With the BLE connected and the restarted, enter `hcfig` in the command line to configure the Bluetooth module. It will usually be listed as being "DOWN". To resolve this, input the command. Ever, stay aware of the commands you're inputting. If the line ends with *noscan*, change it to *up* to allow the device to scan simultaneously. With this, the device entered, enter `hcfig` once more. The device status will be "RUNNING".

```bash
sudo mkdir bluez
cd bluez
sudo wget ..kernel.org/pub/linux/bluetooth/bluez-5.11.tar.xz
```
Our PiBeacon relies on Bluetooth technology, so you'll need a dongle.

### 05 Input UUID
The PiBeacon is now ready. All you need to do is advertise to other (configured) devices. This simply allows the phone to attend to the PiBeacon. However the unique UUID will be broken up into pairs. Any like portions of the string (everything after *cm*) are intended to be changed. For instance, manufacturer-specific data is displayed in this case 00, which is Apple's ID. The UUID shown here is for your own Pi, but it is intended for a particular application - specifically.

```bash
sudo unxz bluez-5.11.tar.xz
sudo xvf bluez-5.11.tar.xz
cd bluez-5.11/
sudo ./configure --disable-system
sudo make install
```

Additionally, check the version repository to review the UUID (alternatively named versionUUID).

```bash
sudo hcfig hci0
sudo hcfig devv 3
sudo hcfig hcichan
```

```bash
sudo hcfig -uuid 0E 01 1A 4F 4C 02 15 02 0E 09 34 7F 73 F5 04 C4 A2F 17 01 07 13 6A 2F 17 01 07 09 01 00 00 00 00 00 00 00 08
```

Here's how to use a unique identifier that can be broken down into meaningful changes

| iBeacon prefix. Manufacturer | TX Power |
|---|---|---|
| data begins after FF | | Minor |

0E 02 01 1A 4F 4C 02 15 02 0E 09 34 7F 73 F5 04 C4 A2F 17

www.linuxuser.com | 69
