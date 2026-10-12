CD-ROM. To install XFree86 from the RPMS directory of your Red Hat Linux CD-ROM, run the following command:

```
rpm -ivh XFree86*.rpm
```

This installs all the XFree86 packages from the CD-ROM. Now continue with XFree86 configuration.

# Configuring X

Before you can configure XFree86 for your system, you need to know the following:

+   - How much video memory you have
+   - What kind of chipset your video card uses
+   - The maximum resolution your monitor supports
+   - Your monitor's make and model
+   - Your monitor's horizontal and vertical refresh rates

If you do not know the information for your video card, you can run the SuperProbe utility to determine it. SuperProbe is included with XFree86. You can run it with the following command:

```
/usr/X11R6/bin/SuperProbe
```

Following is a sample SuperProbe output:

```
WARNING - THIS SOFTWARE COULD HANG YOUR MACHINE.
READ THE SuperProbe.1 MANUAL PAGE BEFORE
RUNNING THIS PROGRAM.

INTERRUPT WITHIN FIVE SECONDS TO ABORT!

First video: Super-VGA
Chipset: S3 Trio64V+ (Port Probbed)
Memory: 2048 Kbytes
RAMDAC: Generic 8-bit pseudo-color DAC
(with 6-bit wide lookup tables (or in 6-bit mode))
```