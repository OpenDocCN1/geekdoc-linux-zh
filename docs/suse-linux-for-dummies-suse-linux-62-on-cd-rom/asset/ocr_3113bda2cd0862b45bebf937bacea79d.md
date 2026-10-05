# Chapter 6: Solving Problems with the X Window System Installation 107

have to manually select some configuration settings for your hardware. As with all X configuration tools, SaX creates a configuration file that the X server uses so it knows how to communicate with your mouse, keyboard, monitor, and the video card on your system.

As Linus becomes more sophisticated in the methods that it uses to probe hardware, and as hardware becomes more sophisticated in the information that it can return to the operating system, fewer questions will need to be asked. For now, though, we have SaX.

To run SaX, follow these steps:

+   1.  Log in as root and type the following:

```
sax
```

SaX should start and immediately open the mouse configuration screen, as shown in Figure 6-3. If SaX does not start, it may not be able to determine which X server to use for your card, or your card may not work with the VGA16 server. If the latter is the case, and you know which X server supports your card, you need to specify that X server when you start SaX.

For example, if you want SaX to use the SVGA X server, type the following:

```
sax -s svga
```

![](bbox=[0.188, 0.56, 0.633, 0.818])

Figure 6-3:
The SaX mouse configuration screen.

+   2.  Select the appropriate device and protocol for your mouse.

Because SaX is aware of the mouse configurations that you selected during the installation, it will use them. If your mouse was correctly configured during the installation, it should be working now. If it is not, then