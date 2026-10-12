# Chapter 14

# Configuring X Window

# Installing XFree86

When you install Red Hat Linux from the official CD-ROM, you get a chance to install and configure XFree86. If you haven't done that already, you can install XFree86 quite easily using the RPM packages on your CD-ROM. To install XFree86 from the RPMs directory of your CD-ROM, run the following command:

```
rpm -ivh XFree86*.rpm
```

This installs all the XFree86 packages from the CD-ROM.

# Configuring XFree86

Before you can configure XFree86 for your system, you need to know the following:

+   - What manufacturer and model of video card you have
+   - How much video memory you have
+   - What kind of chipset your video card uses
+   - The maximum resolution of your monitor
+   - The horizontal and vertical refresh rares, make, and model of your monitor