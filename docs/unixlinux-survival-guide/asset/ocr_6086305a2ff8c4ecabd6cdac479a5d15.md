If you think we are exaggerating here, keep this in mind: backup is expensive, but losing your data for good is much more expensive. Being in a position to exchange a defective tape drive inside the jukebox with the external unit is just an added bonus. Even if the maintenance contract covers a replacement of the defective unit within 4 to 8 hours, would anyone risk losing the data over the availability of a piece of hardware in two to three years time?

# 4.2.4 Backup Using rcs

You can use the Revision Control System, part of most *NIX distributions, on the installation media, to check in important files. This is no real backup, but is a good way to give you some peace of mind.

There is more than one way to use rcs for the task at hand. Either you could create a directory to hold all configuration files put under revision control, modify the files in there, and copy them to their desired location after changing them, or you could create rcs directories in all places they are needed, for example, /etc.

Do as you prefer, but make sure all files get checked in after every change and write a descriptive log message. Everyone will be able to figure out who did what and the reason for the change. You can use rlog to display the revision history, create a living documentation in that respect. Listing 4.2 demonstrates the use of rcs with a configuration file.

# **LISTING 4.2**  Check In Hosts

```
root@unixhost> ci -l hosts
RCS/hosts,v  <--  hosts
new revision: 1.37; previous revision: 1.36
enter log message, terminated with single '.' or end of file:
>> added alias linuxhost for 192.168.0.2 (Erik)
>> .
done

root@unixhost> rlog hosts
...
----------------------------
revision 1.37  locked by: root;
date: 2004/08/27 04:35:36;  author: root;  state: Exp;  lines: +3 -1
added alias linuxhost for 192.168.0.2 (Erik)
----------------------------
...
```

If the change doesn’t work out the way it should have, you can get the former working version out of rcs with co -r revision <filename>. The newer version is still available from rcs, so you can find out what went wrong and rectify the configuration.