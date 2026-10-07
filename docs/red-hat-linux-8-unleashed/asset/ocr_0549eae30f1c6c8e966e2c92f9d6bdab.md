# CHAPTER 27 Using Emulators and Other Cross-Platform Tools in Red Hat Linux

holdovers from the time when Win4Lin's predecessor application, Merge, ran 16-bit
Windows binaries and needed to access the advanced memory management features of
8086 Intel processors.

When launched, Win4Lin provides an MS Windows desktop in an X window running
 your Linux desktop. You can export Win4Lin to another computer just as you do
y X session. The single-user version of Win4Lin only supports one user at a time,
b server version of the product is available. An unsupported application named
apprapper.exe (available on the Netverse Web site) can be used to display a single
application running in Win4Lin rather than the entire desktop—useful if you want to
restrict a user's choice of applications for security reasons.

# Comparing Wine, Win4Lin, and VMware

So how do the Win4Lin and VMware emulators compare to the Wine program each other?
The benefits of Wine versus VMware are that it costs less and uses fewer resources. On
t other hand, Win4Lin cannot handle the range of operating systems that VMware can, and
hardware support is more limited.

Win4Lin has some benefits not found in Wine, as well. Win4Lin can run a wider range of applic-
 and is more stable than Wine, it is surprisingly faster and more stable than a native
Windows installation on the same hardware. Win4Lin does cost more than Wine, however, and
y you must also a licensed copy of Windows in order to use it.

Win4Lin is well suited for running a wide range of business-related applications like MS Office
(office-oriented as opposed to home- or multimedia-oriented DirectX/3D is not
supported) in an environment where stability is important and a licensed copy of Windows is
available.

# Mac OS Emulation

Apple has provided an operating system that has attracted millions of loyal followers and
for which a plethora of applications exist. For the emulator developers, emulating the
Apple Macintosh operating systems on Intel hardware is a challenge Apple soft-
is designed to be run on a non-Intel processor and on hardware that is unlike that
found on many Intel-based PCs. A significant hurdle is the necessity of possessing a
itimate version of the Apple ROM code. Red Hat does not provide any Apple emulators.

In this section, we'll look at the most popular and mature Apple emulators available and
see what they have to offer an Apple user. If you already have an Apple and have accumu-
lated software for it, these emulators can breathe new life and usability into them by allow-
ing to use all your applications on a single computer.

# EXECUTOR

ARDI's Executor is a commercial software emulator that runs legacy Mac OS applications
under Linux. A demonstration version can be downloaded for testing before purchase