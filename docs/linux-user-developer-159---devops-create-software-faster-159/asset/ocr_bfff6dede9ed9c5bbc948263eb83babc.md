# Tutorial

![](bbox=[0.06, 0.11, 0.94, 0.5])

Above The infrared receiver on your robot will look something like this

# Robot variation

+   - You can use a bunch of different robots with this tutorial, such as the Makeblock that's pictured or the WowWee Roboquad that our author used. Pay attention to the event key setup in your code – different robots will have different native functions.
+   - The Roboquad, for example, has a ‘Dance’ command that you can see about halfway down the code listing on the opposite page.

# 07 Make the lirc.conf file: part 3

The second part of the program asks you to enter the names of the keys for each of the signals it has recorded. Follow each of the on-screen prompts, typing a suitable name for each of the remote buttons/ keys. For example, type ‘KEY_UP’ and then press the corresponding up key on the remote. You will then be prompted to type in the name of the next key – for example, ‘KEY_BACK’, in which case you would press the back key on the remote, and so on. Keep repeating this process until you have entered names for each of the recorded keys.

# 08 Rename the remote

Once saved, locate the new lirc.conf file in the /home/pi folder. By default, the name of the remote on line 14 will probably be named as /home/pi/lirc.conf. Change this: under the heading ‘begin remote’, find the ‘name’ label and rename /home/pi/lirc.conf to something more appropriate, such as ‘Robot’. Doing this helps ensure that it is an easier process to refer to it in the program whenever you call a movement instruction or key name.

# 09 Transfer the lircd.conf file

Now your lirc.conf file is ready to transfer to the /etc/lirc folder; this is the folder that holds the hardware and lirc files. The simplest method is to open your new lirc.conf, which is saved into the /pi/home folder, and then copy and paste over the code that you have just created. However, this will overwrite any old configuration file setup that you have. To save a previous file, see the next step. In the LX Terminal, type:

```
sudo nano /etc/lirc/lircd.conf
```

# 10 Transfer file without overwriting

If you have set up a lircd.conf file, or want to use a new one but keep the old one, create a new configuration file. This is saved in the /home/pi folder and can be copied over to /etc/lirc. Make a backup of the original lircd.conf file by creating a copy of it, then save it as lircd_original.conf. In the LX Terminal, type:

```
sudo cp /etc/init.d/lirc_start
sudo mv /etc/lirc/lircd.conf /etc/lirc/lircd_original.conf
```

Then copy over your new configuration file:

```
sudo cp ~/lircd.conf /etc/lirc/lircd.conf
```

Your original configuration file will now be saved as lircd_original.conf.

# 11 Start to take control

Now your robot has a configuration file, you can use your remote control. Restart the LIRC with sudo /etc/init.d/lirc_restart. Now test that the lirc file is working by listing all the registered KEYS stored in the file: irsend LIST Robot '*'. This will list all the KEYS that are recorded in the lircd.conf file.

It’s time to control your device. This uses the irecord application that comes with LIRC to send the commands. The commands are very simple: irecord SEND_ONCE Remote_Name Remote_Button. For example, to make the robot walk forward, just type this into the LX Terminal: irecord SEND_ONCE Robot KEY_UP. This will send the ‘forward’ infrared signal and your robot will then walk forward.