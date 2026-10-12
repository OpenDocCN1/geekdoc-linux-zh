# ## Verifying PPP

First, make certain that PPP is installed on your system. Most types of installation methods under Red Hat install PPP by default. This includes pppd or the PPP daemon, which controls PPP and runs in the background during your period of connectivity. To verify that the protocol is indeed installed, simply issue the RPM command as follows:

```
```
# rpm -q ppp
ppp-2.3.11-7
```
```

The exact version number may vary from release to release. If the program has not been installed, which in the most recent Red Hat version is unlikely, you may either choose the source or binary. You should use the RPM method for purposes of updating and keeping a uniform format throughout your system.

Again, installing the latest version is a simple matter of executing the rpm command as root along with the filename:

```
```
# rpm -ivh ppp*.rpm
```
```

You can install PPP using the source code, but doing so is not recommended. There are too many possible configurations and it is easy to foul up the settings and quickly become discouraged.

# ## Aliasing the Modem to Its Device

To avoid the headaches associated with device names under Linux, Red Hat recommends making a symbolic link from the true device name to a more identifiable designation. For example, under DOS, the modem normally connects to COM2 or COM4, while sometimes reserving COM1 for the mouse. The same is also valid under Linux, except that you connect the modem to /dev/ttyS0 through /dev/ttyS3 rather than COM2 or COM4. Remember that under Linux and UNIX, counting begins with zero. Thus, /dev/ttyS0 is saved for the mouse and /dev/ttyS1 can be allocated to the modem. A recommended method of identifying these files is to give the real device a more recognizable name. Creating a symbolic link is the preferred method:

```
```
# ln -s /dev/ttyS1 /dev/modem
```
```

This example creates a new filename, /dev/modem, that links to the real device. If you need to change modems later or edit the COM settings, you can replace this file with the correct settings.