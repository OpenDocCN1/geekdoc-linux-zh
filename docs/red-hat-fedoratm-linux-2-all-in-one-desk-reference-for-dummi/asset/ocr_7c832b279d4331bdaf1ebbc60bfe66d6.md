# # Chapter 5: Managing Devices and Printers

# In This Chapter

+   - Understanding Linux devices
+   - Managing loadable driver modules
+   - Managing USB devices
+   - Managing print queues

Everything you use to work with your computer is a device. The key-
board and mouse you use to type and click with, the hard drive where
you store everything, and the printer where you get your hard copies —
these are all devices. And guess what? You have to manage them, but don't
worry: It's not as hard as it sounds. All you have to do is load the device
driver and (perhaps) configure the device a bit. This managing is easier to
do if you understand device drivers a bit and get some practice using the
tools Fedora Core includes to help you manage devices. In this chapter, I
provide a brief overview of device drivers and explain how to manage driver
modules. Because printers are a common type of device you have to manage,
I also show you how to manage print queues.

# ## Understanding Linux Devices

Linux treats all devices as files and uses a device just as it uses a file —
opens it, writes data to it, reads data from it, and closes it when done. This
ability to treat every device as a file comes through the use of device driv-
ers. *A device driver* is a special program that controls a particular type of
hardware. When the kernel writes data to the device, the device driver does
whatever is appropriate for that device. For example, when the kernel writes
data to the floppy drive, the floppy device driver puts that data onto the
physical medium of the floppy disk. On the other hand, if the kernel writes
data to the parallel port device, the parallel-port driver sends the data to
the printer connected to the parallel port.

Thus the device driver isolates the device-specific code from the rest of
the kernel and makes a device look like a file. Any application can access a
device by opening the file specific to that device. Figure 5-1 illustrates this
concept of a Linux device driver.