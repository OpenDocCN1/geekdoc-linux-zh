will run a private script that switches off all the important lights and appliances in the house (remember that there is no “all units off” command), post something to your Twitter feed, and play a “Good night” sound effect:

```
```bash
#!/bin/bash

wavplayer default play ~steev/media/good-night-gorgeous.wav
tweet Good night all

/usr/local/bin/heyu turn studio_light off
/usr/local/bin/heyu turn kitchen_light off
/usr/local/bin/heyvu turn lounge_light off
shutdown -h now
```
```

Alternatively, it can detect a message sent by a sensor transmitter that goes to no device at all but is relayed to several others:

```
```text
SCRIPT pir_detect_msg on :: /usr/local/bin/heyu lights on
```
```

Instead of controlling X10 devices, you can also control the PC itself. This example intercepts the messages from a single switch to control the volume of the PC to which the CM11 is connected:

```
```text
SCRIPT E6 on :: /usr/local/minerva/bin/mixer default dec master 10
SCRIPT E6 off :: /usr/local/minerva/bin/mixer default inc master 10
```
```

These commands are run with the same user privileges as whoever issued the initial command:

```
```text
heyu engine
```
```

This ensures the commands and devices (such as /dev/dsp) are available to this user. It is possible to build complex scripts and interactions solely using X10 messages. In Chapter 7, I’ll discuss Cosmic.

# Programming the EEPROM

All of the functionality of the CM11’s EEPROM is available for programming through Heyu. You simply create a text file called /etc/heyu/x10.sched (there is a sample file in this directory also) with a suitable list of commands and type while the CM11U is connected:

```
```text
heyu upload
```
```

The process will convert this text file into a suitable binary image and upload it to the device through the existing serial cable. Because it is impossible to retrieve this data from the CM11, you will want to ensure that you keep a backup of the x10.sched file or the resultant image for later use:

```
```text
/etc/heyu/x10image
```
```

The full details of the x10.sched file format are available in the manual, including how to switch date formats to DMY from the default YMD. For now, I’ll include some fragments of my own schedule by way of an example:

```
```text
macro movies_on 0 dimb lounge 22; 0 on tv; 0 on stereo;
macro lounge_off 0 off lounge; 0 off lounge_table; 0 off tv; 0 off stereo;
timer ...wt...    01/01-12/31 21:00 00:02  movies_on lounge_off
trigger e1 on movies_on
```
```