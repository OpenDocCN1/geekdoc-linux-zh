If the desktop works fine when you type **startx**, you might want to change to a graphical login, so the GUI starts automatically every time. See the “What Happens During Desktop Startup” sidebar for information on booting to a GUI. If X crashes, see /var/log/Xorg.0.log for clues about what went wrong.

If your GUI is so distorted you can’t even see to correct it, switch to a virtual terminal to correct the problem. For example, hold the Ctrl and Alt keys, and press F2. You will see a plain text login prompt. Log in as root user and type **init 3** to make the garbled GUI login screen go away. As an alternative, press Ctrl+Alt+Backspace to close the X session. Then you can try tuning your video card as described in the following section.

> TIP: Switching virtual terminals is a great way to get out of a GUI that is broken or stuck and run the commands you need to fix a problem. You can use any function key from F1 through F8 with Ctrl+Alt to switch terminals. The GUI itself is probably on the F7 virtual terminal. Linux experts use virtual terminals during Fedora or RHEL installation to debug a problem or during startup to view text startup messages.

# ## Tuning your video card and monitor

If your GUI is starting up but needs some tuning (to get better resolution, more colors, or to fix flickering), you can use the Display Settings window to fix your desktop. For the current Fedora and RHEL versions, the Display Settings window was enhanced so that you can use it from a command with no GUI running. The next sections describe how to run the Display Settings window, and then how to review the resulting xorg.conf file to understand your settings.

# ### Running the Display Settings window

The Fedora Project recently replaced the Xconfigurator tool with a new Display Settings window (*system-config-display* command). This window lets you set the most basic functions relating to your display, monitor, and video card. The Display Settings window is easy-to-use and no longer requires a running X desktop to use it.

To open the Display Settings window from the Desktop menu, click System Settings → Display. To open that window from a text prompt (even with no GUI running), type *system-config-display* (as root).

From the Settings tab of the Display Settings window, you can try different resolutions (screen width and height in pixels) and color depth (from 256 colors to millions of color). Click the Hardware tab to try to configure your monitor and video card. Click the Dual head tab if you have a video card that supports two monitors that you can use side-by-side with Fedora or RHEL. Click OK to save your changes.

Here are a few tips for using the Display Settings window:

+   - If you know your monitor type, but it is not being detected, click the Hardware tab and then click Configure. You can select the monitor from a list of monitors (by