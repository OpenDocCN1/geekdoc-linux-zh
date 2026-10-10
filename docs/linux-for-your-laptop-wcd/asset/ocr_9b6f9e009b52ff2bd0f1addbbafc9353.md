![](bbox=[0.08, 0.07, 0.47, 0.3])

*Figure 6.5* *The XFree86Setup client is a graphical setup program for configuring X11 for your notebook.*

# ## Starting XFree86Setup

Until the advent of XFree86 4.0 (see the later section “Installing XFree86 4.0”), XFree86’s X11 distribution included a graphical setup program named **XFree86Setup**. If you have a current Linux distribution, you can try running this program, which requires that the X server named **X**Free86_VGA16 be available under the */usr/X11R6/bin* directory. From the command line, type **XFree86Setup** and press Enter. Your display should clear, and you should then see the dialog box shown in Figure 6.6.

Follow the prompts, using either the mouse or the keyboard, to make selections that match your notebook’s hardware. For example, to start the configuration of your pointer (mouse), press **Alt+m**.

# ## Using Xconfigurator

If **XFree86Setup** will not run, and you’re using Red Hat Linux, you can try Red Hat’s **Xconfigurator** client. This command does not require you to start X11, but you should have the appropriate X server (if you’re not using XFree86 4.0) for your notebook installed in the */usr/X11R6/bin* directory. From the console’s command line, type **Xconfigurator** and press Enter. Your display will clear, and you’ll see the dialog box shown in Figure 6.7.

**Xconfigurator** will either use an existing XFree86Config file (such as **XFree86Setup**) or can be used to create a new one from scratch.