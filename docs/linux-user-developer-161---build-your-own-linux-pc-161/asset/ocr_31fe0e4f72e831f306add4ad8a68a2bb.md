# Full code listing

photo, ensure that your Pi's clock is set correctly before you start your program.

```
import time
import os
import piccamera
import subprocess
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)
# Setup the PIR
PIR = 7
GPIO.setup(PIR, GPIO.IN)
# Setup the LISPAROL
GPIO.output(10, GPIO.OUT)

global file_name = ##number of photo
global file_name = ##name of photo
File_Number = 1

def detect_self():## takes a photo of the weeebastie
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
GPIO.output(10, GPIO.LOW) ##Turn off LISPAROL
```

time_of_photo = time.asctime(time.localtime(time.time()))

12 Add the time to the picture
Recording the time a picture is taken is relevant if you are watching and waiting for wildlife to trigger the camera, and you can see the time value. A better solution is to add a "time stamp" to the picture. This means when you view the image you see the time. The line of code added is camera.annotate = "time".

13 Recap
Before you finish, a quick recap on the features and setup: the PIR module is attached to the Pi in the dark. This requires an infrared light source, which is provided by the LISPAROL. A PIR attached is used to sense changes in heat, which turns the LED and triggers the camera to capture a picture. The current time is recorded for future reference. The caption on the pages showing views for the LISPAROL and PIR are

14 Taking a video
If you would prefer to take a video when the PIR is triggered, you could adapt the program to record video of wildlife that might visit your garden. For example, you could change the code to record video using the camera.start_recording("/home/desktop/video.avi"). If you want to record for say, 20 seconds, use time.sleep(20) before stopping the recording with camera.stop_recording("/home/desktop/video.avi").

```
camera.start_preview()
camera.start_recording('/home/desktop/video.h264')
time.sleep(5)
camera.stop_recording()
```

15 Automatically start your project
The project you have built can run without a monitor or screen, meaning that you can want the program to start. To do this, set the program to start automatically when the power supply is plugged in. You will have to add a line to your script, for example, in the /home/name/Night_Box.py file. Double-check if you'd use /home/name/Night_Box.py to get the correct path by the Terminal and command.

```
sudo nano /home/name/of_your_script.py
```

If correct, this will display the contents of your Python code. The next step is to create a job by modifying the 'cron'. To do this, use crontab -e (which will run the task for all users). Scroll to the top of the window and add the following line to:

```
@reboot python /home/name/of_your_program.py &
The @ at the end will run code in the background and ensure your Raspberry Pi will boot up as normal. Save the file by hitting Ctrl+X followed by Y, and then reboot.
```

16 Deploy the Box
To deploy the setup effectively you will want to create a box or holder for the PIR, LISPAROL. This will protect the equipment from getting damaged if it rains or blows. You may want to create a 3D-printed structure for the components. In the previous step you used a scheduled cron to start the program automatically when the Raspberry Pi is booted. Choose a suitable location and set up your box. Start the program and check back the next day to see what visits your garden present!

![](bbox=[0.62, 0.81, 0.64, 0.82])