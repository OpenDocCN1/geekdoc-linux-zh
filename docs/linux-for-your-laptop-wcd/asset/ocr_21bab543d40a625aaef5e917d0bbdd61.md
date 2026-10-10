If you need access to your LAN, and you don't mind paying for long distance (or if your cellular service provider has free long distance), you can configure your Linux system for dial-up access.

# ## Setting up for Dialing In

Setting up a Linux system for dial-in capabilities is very easy. You need a computer with a modem and a phone line to answer the phone. If you have two phone lines attached to the computer, after you log in you can dial out and connect to your ISP to send and receive software.

Edit your system's initialization table, /etc/inittab, and look for these lines:

```
```bash
# Run getty in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```
```

Each line represents a different Linux runlevel. When you use Linux without X11, you run Linux at runlevel 3. When you use X11 with Red Hat or Mandrake Linux (note that other distributions might use different runlevels), you use runlevel 5. One of the first lines in your /etc/inittab file shows the default runlevel; it might look something like this:

```
```bash
id:5:initdefault:
```
```

To have Linux answer the phone and allow you to log in, you need to use the `agetty` command instead of the `/sbin/mingetty` command to monitor runlevel 3. You also need to specify the serial port used by your modem. Change this line:

```
```bash
3:2345:respawn:/sbin/mingetty tty3
```
```

to this:

```
```bash
3:2345:respawn:/sbin/agetty -w -I "ATE0Q1&D2&C1S0=1\015" 115200 ttyS0 vt100
```
```

The `agetty` command automatically initializes your modem to answer the phone, using your modem's S0 register (set to answer after the first ring in this example). Note that the modem is attached to the computer's COM1 port.