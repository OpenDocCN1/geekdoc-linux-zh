# # Setting Up SLIP

SLIP is used by some ISPs who don’t support PPP (a rarity these days). You may also find SLIP supported by some online services that don’t use the Internet, such as bank access programs and stock trading. In the past, SLIP was usually compiled into the Linux kernel, as was a modification of SLIP called CSLIP (Compressed SLIP). With Red Hat Linux, however, SLIP support is supplied as a loadable kernel module.

To use SLIP, you need to dedicate a port to it. This means that the port cannot be used by other applications. This is necessary because of the way SLIP handles ports, which causes conflicts if shared with other programs.

# ## Note

If you want SLIP installed in your kernel, you need to rebuild the kernel. See Chapter 27, “Configuring and Building Kernels,” for more information.

# # Configuring SLIP

The fastest way to configure SLIP is to use the slattach program. This requires the name of the port that SLIP will use (which has a modem attached for the connection, usually). The command that sets up slattach is as follows:

```
# slattach /dev/ttyS0 &
```

In this case, I’ve configured /dev/ttyS0 port (COM1) as the SLIP port. You can use any other port attached to your system. The ampersand at the end of the line puts the slattach program in the background so you can get your shell prompt back.

When you run slattach, the port is renamed to /dev/s10, which indicates it is the first SLIP device. It doesn’t matter what device name you used for the serial port; the first SLIP device is always called /dev/s10. This can lead to some confusion if you are using /dev/ttyS2, for example, which becomes /dev/s11. If more than one SLIP port is created, they are numbered increasingly as /dev/s11, /dev/s12, and so on. Linux usually supports up to eight SLIP lines, but it is unlikely you will need this many. To check if the SLIP device has been created, you can search the file named dev under the /proc/net directory using fgrep like this:

```
# fgrep s10 /proc/net/dev
s10:     0     0     0     0     0     0     0     0
...      
```