# Part II Using CentOS

+   1. Open permissions to your X server so that the remote application can use your display
+   2. Identify your X server display to the application when it starts up.

When you run an X client on your local system, your local display is often identified as :0, which represents the first display on the local system. To identify that display to a remote system, however, you must add your computer’s hostname. For example, if your computer were named whatever, your display name would be:

```
```
whatever:0
```
```

> **TIP** In most cases, the hostname is the TCP/IP name. For the computers on your local network, the name may be in your `/etc/hosts` file, or it may be determined using the Domain Name System (DNS) service. You could also use a full domain name, such as `www.example.com`. X does support other types of transport, although transports other than TCP/IP aren’t used much anymore.

You will probably use the display name in this form most of the time you run a remote X application. In certain cases, however, the information may be different. If your computer had multiple X displays (keyboard, mouse, and monitor), you may have numbers other than :0 (:1, :2, etc.). It is also possible for one keyboard and mouse to be controlling more than one monitor, in which case you could add a screen number to the address, like this:

```
```
whatever:0.1
```
```

This address identifies the second screen (.1) on the first display (:0). The first screen is identified as .0 (which is the default because most displays only have one screen). Unless you have multiple physical screens, however, you can skip the screen identifier.

There are two ways to identify your display name to a remote X application:

+   * **DISPLAY Shell Variable** — The `DISPLAY` shell variable can be set to the system name and number identifying your display. After this is done, the output from any X application run from that shell will appear on the display indicated. For example, to set the `DISPLAY` variable to the first display on `whatever`, type one of the following:

```
```
export DISPLAY=whatever:0
```
```

or

```
```
setenv DISPLAY whatever:0
```
```

The first example shows how you would set the `DISPLAY` variable on a `bash` or `ksh` shell. The second example works for a `csh` shell.

+   * **`-display` Option** — Another way to identify a remote display is to add the `-display` option to the command line when you run the X application. This overrides the `DISPLAY` variable. For example, to open an `xterm` window on a remote system so that it appears on the first display on `whatever`, type the following:

```
```
xterm -display whatever:0
```
```