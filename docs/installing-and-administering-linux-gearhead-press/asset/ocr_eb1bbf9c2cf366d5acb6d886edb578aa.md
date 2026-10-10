will require for your installation. We will explain default behavior and our rationale for choosing specific options. It is our intention that you will be able to make informed decisions when performing your own installation.

# Step 1. Boot Message

If you were to walk away from this first screen without selecting anything here, the installation program would proceed to boot the system on its own and would default to the GUI installation mode. We are specifically going to demonstrate the *text* mode installation (in other words, the `type: text <Enter> option in the screen facsimile shown in Figure 2.2).

**Install or upgrade . . . graphical mode.** This option is the default and will launch a GUI install panel. Be aware that this choice has a high video failure rate because it does not interpret all video cards and monitors correctly. If you choose this option and it fails, we recommend that you immediately reboot and use the text option.

**Install or upgrade . . . text mode.** This option is provided for practical reasons to facilitate the installation of the majority of systems with no graphical support. Remember, though, that not all systems that are destined to be servers will have graphical support. If that is what your system is to be, you might have to select this option.

```
Welcome to Red Hat Linux 7.1!!

o To install or upgrade Red Hat Linux in graphical mode, press the <ENTER> key.
o To install or upgrade Red Hat Linux in text mode, type text <ENTER>.
o To enable low resolution mode, type: lowres <ENTER>.
    Press <F2> for more information about low resolution mode.
o To disable framebuffer mode, type: nofb <ENTER>.
    Press <F3> for more information about disabling framebuffer mode.
o To enable expert mode, type: expert <ENTER>.
    Press <F3> for more information about expert mode.
o To enable rescue mode, type: linux rescue <ENTER>.
    Press <F5> for more information about rescue mode.
o If you have a driver disk, type: linsrc <ENTER>.
    Use the function keys listed below for more information.

[F1=Main] [F2=General] [F3=Expert] [F4=Kernel] [F5=Rescue]
```

![](bbox=[0.11, 0.92, 0.38, 0.94])