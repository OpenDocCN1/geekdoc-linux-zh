# **Reboot the System**

At this juncture, all you have to do is reboot the machine. When Linux boots again, the command-line login prompt does not appear. Instead, you are presented with the graphical `xlogin` widget.

# # Basic X Window Components

The concepts introduced in this section should be easily grasped, especially since almost all of us have used a graphical user interface (GUI) before. However, even though the discussion may seem almost trivial to some, the terms and concepts as defined here are worth remembering. They are common to all GUIs, and provide a foundation for understanding and comparison not only among X Window managers, but also between the X Window system and other GUIs.

# ## Display

Figure 14.2 illustrates what your X Window System *display* might look like when using one of the less-complex window managers. All window managers do not look like this one, however; some have more or fewer applications showing different backgrounds and so on, depending on the preferences of the system administrator or the person who installed X. Moreover, ordinary users will have some ability to add or delete applications or other information.

The basic components of the display are described next:

**Root window.** Also called the *desktop*, this area fills the entire screen. You can move your mouse to an open part of this area (that is, an area not covered by other windows or other displays) and then left-click to access the root menu, a menu that helps you start other windows or otherwise customize your environment. A sample root menu appears in the bottom-right corner of Figure 14.2. Note that we have chosen a generic name (`wimngr`) for the window manager. Now, if you right-click an open area of the root window, you automatically invoke the Programs menu, which is the same menu you would get if you accessed a root menu and then clicked `Programs` (because of space constraints, we did not show the