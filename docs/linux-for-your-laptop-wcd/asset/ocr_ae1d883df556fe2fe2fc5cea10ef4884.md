![](bbox=[0.19, 0.08, 0.41, 0.12])

Figure 7.3 The *xhattery* client is a simple strip gauge for Linux notebook users.

+   * *xhattery*. Another X11 client that displays your notebook’s remaining battery life using a simple strip gauge and color (see Figure 7.3).

# ## Potential Networking and Communications Problems

Mobile Linux users need to be aware that some devices, especially PC cards, might not work very well if the notebook is put into suspend or hibernation and then resumed. Just as you should never eject a floppy disk until write operations have finished (when the drive light, if there is one, goes out), you should always wait until read or write operations have finished when using a flash memory card (which simulates an IDE drive) or a SCSI PC card interface for an external drive. Modem cards might also be susceptible to problems if they are ejected prematurely.

A much safer approach is to wait for current operations to finish and then eject the card and shut down Card Services before putting your notebook to sleep. You can do this in a variety of ways, including using a shell script.

# ## Using a Shell Script

Shell scripts are a handy way to quickly craft utilities for Linux. The following script, which you can name *dosleep*, should work with Red Hat and Mandrake Linux notebook systems. The script first uses the `cardctl` command to shut down and disable power for two PCMCIA sockets. (If you have only one, don’t use the second command.) The script then shuts down Card Services and networking (the script assumes you have a network card in one of your PC card slots). Finally, the `apm` command is used to put the notebook to sleep.

```
```python
#!/bin/sh

# stop Card Services (note: may not be safe for all cards!)

# stop networking, then put a notebook to sleep
/sbin/cardctl suspend 0
/sbin/cardctl suspend 1
/etc/rc.d/init.d/pcmcia stop
/etc/rc.d/init.d/network stop
/usr/bin/apm -s
```
```