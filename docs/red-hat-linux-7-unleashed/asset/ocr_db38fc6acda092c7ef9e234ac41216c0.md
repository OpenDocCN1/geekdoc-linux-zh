A forms-based interface is often more comfortable, but X11 is sometimes impractical— for example, while doing remote administration over a slow telnet connection or in a Linux machine for blind users. For these situations, we have the ncurses-based menuconf.ig. Both the X11 and the ncurses configuration tools offer the same options in the same order, and they have roughly the same capability to navigate backward and forward through the configuration options.

# Note

The X and ncurses configuration commands also have the same propensity to allow wildly conflicting kernel options with nary a whisper of dissent... some- time early in 2.5, this will all change with the adoption of Eric Raymond's CML2 Configuration Management Language (see the section “CML2: The Next- Generation Configuration Tool”).

To start the configuration, simply go to the /usr/src/linux directory and enter one of the configuration commands. If you choose either of the ncurses or X11 methods, you will see a brief flurry of compiler activity while the user-interface programs compile, and then you will be greeted by an overview screen with all the categories of kernel options.

Those of you who recoil in horror at the thought of a command line can now rest easy. From this point on, those using the xconfig method will be in carpal-tunnel land (a.k.a. “mouse mode”) until the configuration is done.

# ## Selecting Configuration Options

Figure 27.2 shows the initial screen as seen in the xconfig display for the 2.4 kernel. 2.2.x kernels are very similar, but with fewer options and minor cosmetic differences. In all of the configuration methods, most kernel options can be set to be included, included as a module, or left out of the compile. On the xconfig and menuconf.ig screens, there are options to include or exclude complete sections of configuration; disabling these will gray out any dependent options (the dumb-terminal config option will silently skip these sections).

This guide cannot attempt to describe every one of the 1,302 individual options in the Linux kernel; this chapter will only cover the major groups, focus on options of interest to specific applications, and explain some of the implications and configuration options for common Intel-based modules.