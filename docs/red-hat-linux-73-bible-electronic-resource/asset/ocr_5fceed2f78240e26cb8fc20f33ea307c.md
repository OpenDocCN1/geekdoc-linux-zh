The following is a description of the basic information contained in the XF86Config file:

+   *   **Files section** — Sets the locations of the RGB (color) and fonts databases.

+   *   **Server flags section** — Allows you to disable abort and mode switching key sequences (usually you will leave this section alone).

+   *   **Keyboard section** — Sets keyboard settings, including the layout of the keyboard and how certain key sequences are mapped to the keyboard.

+   *   **Pointer section** — Selects the pointer you are using (typically a mouse linked to `/dev/mouse`). Also sets speed and button emulation, when appropriate.

+   *   **Monitor section** — Sets the type of monitor, along with its horizontal sync rate, vertical refresh rate, and settings needed to operate at different resolutions.

+   *   **Screen section** — Binds together the graphics board and monitor information to be referenced later by the ServerLayout section.

+   *   **Graphics device section** — Identifies your video card and, optionally, video RAM and clock information for the chipset.

+   *   **ServerLayout section** — Sets server definitions for different X servers (if necessary).

# ## Getting more information

If you tried configuring X and you still have a server that crashes or has a garbled display, your video card may either be unsupported or may require special configuration. Here are several locations you can check for further information:

+   *   **XFree86.org** (www.xfree86.org) — The latest information about the X servers that come with Red Hat Linux is available from the XFree86.org Web site. XFree86 is theeware version of X used with all major Linux distributions.

+   *   **Red Hat Support** (www.redhat.com/support) — Search the Red Hat support database for the model of your card. There may already be reports of problems (and hopefully fixes) related to your card.

+   *   **X documentation** — README files that are specific to different types of video cards are delivered with XFree86. Look in the XFree86 doc directory (`/usr/X11R6/lib/X11/doc`) for a README file specific to the type of video card (or more specifically, the video chipset) you are using. There is also a lot of good information on the XF86Config man page (type `man XF86Config`).

# ## Starting the X Desktop

There are several different ways you can start your desktop in Red Hat Linux. If Red Hat Linux starts up and you see a graphical login screen, you can just log in and your desktop environment should appear. If Red Hat Linux starts up to a simple text-based login prompt,