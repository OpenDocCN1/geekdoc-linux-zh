> If you turn off this option, the Windows pointer remains visible wherever it was when you changed the input focus back to Linux. If you turn away from the screen and then turn back, you might get confused about which is the active mouse pointer until you actually start moving the mouse.

# Bring the Virtual Machine to Top

The option Bring the virtual machine to top is turned off by default. When on, it immediately brings the VMware window to the foreground whenever VMware is given the input focus. You might want to turn this on if you have a cluttered desktop and it might be difficult to move the VMware window to the top yourself.

However, if this option is on along with Capture input focus, it means that whenever your mouse pointer strays into the VMware window, it leaps to the foreground, which might be annoying, at best, when you are working on other projects in Linux.

> Keep experimenting with mix-and-match combinations of these cursor options until you have the settings that best fit the way you use VMware and your host PC.

# Allow Copy and Paste

By default, VMware Tools allows you to share a clipboard between Linux and your virtual machine, which, in theory, allows you to cut and paste seamlessly across applications, regardless of operating system. Some applications do not read the clipboard in the expected manner, and text cut and paste generally works better than graphical cut and paste. Test the shared clipboard performance before you start making drastic changes to documents.

You might want to turn off the option Allow copy and paste if you have security concerns on the host computer and you don’t want to encourage the flow of information across the boundary between the host OS and the virtual machine. Or you might simply want to keep the two clipboards separate because the projects you are working on in Linux and in the Windows virtual machine are different and need access to their own, private clipboards.