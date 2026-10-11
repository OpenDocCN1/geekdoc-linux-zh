# **Figure 3–21 The Control Panel**

![](bbox=[0.14, 0.19, 0.5, 0.32])

To start the control-panel, start the X Window System as root with `startx` and type `control-panel` in an Xterm. You will need to be root to run the control-panel tools successfully. You can do this as well if you already have X running as a normal user. Just type `su -c control-panel` and then type the root password when prompted. If you plan to do other tasks as root, you could type `su` followed by the root password when prompted.

> **Please Note**
> 
> If you are not running X as root, you may need to give root access to your system’s X server. To do this, enter the following command on a *non-root* terminal window:

```
```xhost +localhost```
```

After starting the control panel, simply clicking on an icon starts up a tool. Please note that you are not prevented from starting two instances of any tool, but doing so is a very bad idea because you may try to edit the same files in two places and end up overwriting your own changes.