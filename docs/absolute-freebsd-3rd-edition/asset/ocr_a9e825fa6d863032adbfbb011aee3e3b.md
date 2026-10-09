norm instead of the exception.7 At the end of this file, you'll see a few entries like:

```
# Finger friendly shortcuts
uart0|con1:dv=/dev/cua0:br#9600:pa=none:
uart1|con2:dv=/dev/cua1:br#9600:pa=none:
--snip--
```

The uart entries are the standard Unix-type device names, while the con names were added for the convenience of people who grew up on x86 hardware.

Assume that you have two FreeBSD boxes wired back-to-back, with each one's serial port 1 null-modemed into serial port 2. Both machines are configured to use a serial console. You'll want to connect to your local serial port 2 to talk to the other system's serial console:

```
# tip uart1
connected
```

You're in!

To disconnect the serial console, press ENTER and then type the disconnect sequence “tilde-dot” at any time.

```
~.
```

You'll be gracefully disconnected. (This also works in the OpenSSH client.)

The tip(1) program uses the tilde (~) as a control character. Read the man page for a full list of things you can do with it.

# IPMI SOL Connections

You'll need a SOL client to connect to your IPMI serial port. The quickest way to test your configuration is probably with the SOL client applet included in your BMC. While that client has most of the disadvantages of the console applet, it's a good place to test. If the BMC SOL client doesn't work, check your SOL settings and FreeBSD configuration. Verify that the SOL client is set to use the same speed you set in the hardware and in FreeBSD. If it doesn't work but all your