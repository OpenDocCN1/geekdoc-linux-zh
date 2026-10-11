The answer he was given is:

\> Grab the mii-tool and check the duplex settings on the NIC. My guess is that it is a link issue, not an application layer problem. Also run ifconfig and verify that the framing error, collisions, and so on, look normal for ethernet.

# 43.11  Corrupt tdb Files

Our Samba PDC server has been hosting three TB of data to our 500+ users [Windows NT/XP] for the last three years using Samba without a problem. Today all shares went very slow. Also, the main smbd kept spawning new processes, so we had 1600+ running SMDB’s (normally we average 250). It crashed the SUN E3500 cluster twice. After a lot of searching, I decided to **rm /var/locks/\*.tdb**. Happy again.

*Question: Is there any method of keeping the \*.tdb files in top condition. or how can I detect early corruption?*

*Answer: Yes, run* **tdbbbackup** *each time after stopping nmbd and before starting nmbd.*

*Question: What I also would like to mention is that the service latency seems a lot lower than before the locks cleanup. Any ideas on keeping it top notch?*

*Answer: Yes. Same answer as for previous question!*

# 43.12  Samba Performance is Very Slow

A site reported experiencing very baffing symptons with MYOB Premier opening and accessing its data files. Some operations on the file would take between 40 and 45 seconds. It turned out that the printer monitor program running on the Windows clients was causing the problems. From the logs, we saw activity coming through with pauses of about 1 second. Stopping the monitor software resulted in the networks access at normal (quick) speed. Restarting the program caused the speed to slow down again. The printer was a Canon LBP-810 and the relevant task was something like CAPON (not sure on spelling). The monitor software displayed a “printing now” dialog on the client during printing.

We discovered this by starting with a clean install of Windows and trying the application at every step of the installation of other software process (we had to do this many times). Moral of the story: Check everything (other software included)!