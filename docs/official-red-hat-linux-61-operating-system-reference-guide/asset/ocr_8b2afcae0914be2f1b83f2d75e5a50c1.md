Next, we’ll discuss information on the files in /etc/sysconfig.

# 2.13.2 Sysconfig Information

The following information outlines the various files in /etc/sysconfig, their function, and their contents.

# Files in /etc/sysconfig

The following files are normally found in /etc/sysconfig:

+   • /etc/sysconfig/clock
+   • /etc/sysconfig/hwconf (this should be ignored for editing)
+   • /etc/sysconfig/mouse
+   • /etc/sysconfig/sendmail
+   • /etc/sysconfig/apmd
+   • /etc/sysconfig/init
+   • /etc/sysconfig/keyboard
+   • /etc/sysconfig/network
+   • /etc/sysconfig/pcmcia
+   • /etc/sysconfig/soundcard (which is written by sndconfig)

Let’s take a look at each one.

# /etc/sysconfig/clock

The /etc/sysconfig/clock file controls the interpretation of values read from the system clock. Earlier releases of Red Hat Linux used the following values (which are deprecated):

+   • CLOCKMODE=mode, where mode is one of the following:
+   – GMT -- indicates that the clock is set to UTC.
+   – ARC -- on Alpha only indicates the ARC console’s 42-year time offset is in effect.