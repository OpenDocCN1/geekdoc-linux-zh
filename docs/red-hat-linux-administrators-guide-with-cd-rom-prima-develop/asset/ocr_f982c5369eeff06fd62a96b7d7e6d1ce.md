setup. In most cases, this should force the system to print any text file. Be sure also to restart the lpd daemon so that it rereads the /etc/printcap file. If both options—testing new filters and printing to the port—fail, check the hardware.

I remember installing a very early version of Red Hat on a machine given to me. No matter what I tried I could not configure the machine to print. Then, I checked the internal cabling and discovered that whoever had built the box had plugged the cable in backwards. This is an unlikely scenario in today's machines, but possible nonetheless in older systems.

# ## Restarting the lpd Daemon

The lpd daemon runs the entire printer system. Like other daemon processes, lpd sits in the background checking its port, awaiting print requests. The Linux system must run the print daemon before any sort of printing occurs. During the Red Hat Linux installation process, you can set up the daemon to start automatically. Or, if you choose to set it up later upon boot, you can define it using the /usr/sbin/ntsysv command. This utility selects which options should be started upon startup. You can manually restart the lpd daemon, much like you do under the PrintTool command. Changing the lpd status via the command line gives you more control over the stop and restart options.

The following text is a sample command to restart the Linux printer daemon (lpd). As is the case after modifying any configuration files, you should either send a HUP signal to the PID or stop and restart the daemon.

```
# /etc/rc.d/init.d/lpd restart
Shutting down lpd:
[			OK		]
Starting lpd:
[			OK		]
```

# ## Printing Directly to the Port

To print files without using any additional GUIs, you can use the command line. To do so, you must first have root permissions and then use the cat (*concatenate*) command. The cat command prints out to the standard input. Be aware that accomplishing this as root is not recommended unless it is not a public queue. In other words, it is fine to forcibly send files to the printer as root provided you are the only person on your machine and no one else is using the printer. However, using the lpr command instead is the recommended method of sending files directly to the printer. In nearly all instances one uses lpr. If this does