Each mode exists in its own directory, numbered sequentially, from `$MINBASE/etc/cosmic/0`. This holds all the files necessary to control that mode. It includes the following files:

+   name: A text file with the mode name. This is read aloud when you cycle to the mode.
+   
+   status: A script that writes the status report for this mode to STDOUT. In the case of a multimedia mode, it would be the currently playing song, for example. This is read out at the end of each mode status report. If no file exists, the mode name is simply reread.
+   
+   c1, c2, c3, c4, c5, c6, c7, c8: These eight files are the scripts that are executed when any of the eight corresponding commands buttons are pressed. By running scripts in this way, you can change the system without reprogramming the `x10.conf` file or restarting the heyu daemon.

All of the main work is done in those eight c1–c8 scripts. There are three sample subsystems in Minerva: media control for the CD player, a set of status reports, and a set of timers. This latter mode uses the wireless controller to begin timing a set period, such as five minutes. Once the time is up, the voice announces its completion, with several timers able to be run concurrently.

> **Tip**  The output from all c1–c8 scripts should be written to STDOUT. In this way, you can debug Cosmic configurations much more quickly (and easily) by changing the code in Cosmic to read `REPORT=/bin/echo`.

# To Yaks

Although Cosmic has many benefits, it wasn’t as expansive as some people wanted. So Yaks was born. As an acronym it stands for “Yet Another Kontrol System,” and is a method for processing arbitrary messages (from X10 device) into Linux-bound commands. There are a series of scripts, held in `/usr/local/minerva/etc/x10/scripts/` which are called when a button is pressed from a specified controller. Each controller lives in its own subdirectory, and each button has a subdirectory from that. So, for example, button 8 on the control panel for the shower unit would be in the directory,

```
/usr/local/minerva/etc/x10/scripts/Shower/8
```

bECAUSE the X10 addressing protocol isn’t as user-friendly as this, you must also configure Yaks to map the X10 messages (such as D9) into their equivalents here. This information is stored in a code-based configuration script at `/usr/local/minerva/etc/x10/controls` which looks like this:

```
```shell
$c = $config->addController(new YaksController("Keyfob", "c", 1, 8));
$c = $config->addController(new YaksController("Shower", "d", 8, 8));
```
```

> **Note**  This configuration looks like code because it is! This file is loaded as part of the yaks program, which creates the `$config` object, and declares the YaksController class. Using code as data is a cheat, but allows for more flexibility in the configuration.

From this you can see that the Keyfob occupies house code “C” and 8 unit ids of 1 through 8, while the shower is working on house code “D”, with 8 units numbered 8 to 16. All that is then necessary is to ensure every house code and unit is set-up in `/etc/x10.conf` to trigger the yaks program.