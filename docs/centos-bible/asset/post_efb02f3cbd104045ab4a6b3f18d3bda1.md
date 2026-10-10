
## Getting Started with the Desktop

![](img/2f265415ceec72538dd3c78ffca75c10_126_0.png)

## Trying Other GNOME Applications

The GNOME project stores and tracks bugs for a variety of Open Source projects that work well with GNOME desktops. Two such applications are the Tomboy desktop note-taking application and the GNOME Network Tools utility.

## Taking Notes with Tomboy

Tomboy ([www.beatniksoftware.com/tomboy](http://www.beatniksoftware.com/tomboy)) is an excellent tool for keeping track of lots of bits of information. Instead of putting little sticky notes all over your computer, Tomboy lets you put sticky notes *inside* your computer. Features in Tomboy enable you to link notes together, search your notes, and use fonts and colors to help information within your notes stand out.

Add the Tomboy Notes applet to your desktop panel as you would any GNOME applet (yum install tomboy, and then select “Tomboy Notes” from the Add to Panel window). Then click on the sticky notepad icon and select “Create New Note” to open a small window that's ready for you to start typing your note.

After you have created a sticky note with Tomboy, double-click on the title bar to be able to add a title, font, font color, and note color. You can add links to new notes (select some text and click on the **Link** button). You can go back and search for text in existing notes (click on the Search button). You can even see a table of contents of your notes (select the Tomboy applet icon, and then select “Table of Contents”).

### Getting Started

Recent new features in Tomboy allow you to add links to items outside of your notes, such as URLs and files. Those items are automatically detected and highlighted as you type them.

If Tomboy is not available on your system, type **yum install tomboy** to install it. Figure 3-14 shows an example of the Tomboy applet.

#### FIGURE 3-14

Tomboy lets you create virtual sticky notes to keep important information at your fingertips.

![](img/2f265415ceec72538dd3c78ffca75c10_127_0.png)

### Checking Your Network from GNOME

The GNOME Network Tools window (recently added to GNOME) brings together several tools you would normally run from the command line to monitor network resources from a graphical window on your GNOME desktop. To open the Network Tools window, select Network Tools ▸ System Tools ▸ Network Tools. Eight tabs on that window let you perform different operations on your network.

If the GNOME Network Tools window is not available on your system, type **yum install gnome-nettool** to install it.

The Devices tab displays information about each of your network interfaces. It makes it easy to find the names and addresses associated with each of your network interfaces (IP addresses, broadcast, netmask) as well as information on data transmissions and collisions.

On other tabs, you can run graphical versions of the **ping** command (to see if another computer can be reached on your network), **netstat** command (to see information about routes and network services), and **traceroute** command (to watch the network hops from your site to a remote host). You can do a port scan with Nmap (to check for open ports on a network interface), DNS lookup (to get information about a domain **name.system.server**, finger (to see who’s logged into a local or remote host computer), and whois (to get information about domain name registration).

Figure 3-15 shows an example of the GNOME Network Tools window.

#### FIGURE 3-15

The GNOME Network Tools window gives you convenient access to common network diagnostic and lookup commands.

![](img/2f265415ceec72538dd3c78ffca75c10_128_0.png)

### Exiting GNOME

When you are done with your work, you can either log out from your current session or shut down your computer completely.

To exit from GNOME, do the following:

- 1. Click on the System button from the panel.
- 2. Select Log Out from the menu. A pop-up window appears, asking if you want to log out.
- 3. Select OK from the pop-up menu. This will log you out and return you to either the graphical login screen or to your shell login prompt.
- 4. Select OK to finish exiting from GNOME.

If you are unable to get to the “Log Out” button (e.g., if your Panel crashed), there are two other exit methods. Try one of these two ways, depending on how you started the desktop:

- If you started the desktop by typing **startx** from your login shell, press [Ctrl]+[Alt]+[Backspace] to kill X and return to your login shell. Or you could type [Ctrl]+[Alt]+[F1] to return to where you first ran **startx**, and then press [Ctrl]+C to kill the desktop.
- If you started the desktop from a graphical login screen (and `[Ctrl]+[Alt]+[Backspace]` doesn’t work), first open a Terminal window (right-click on the desktop and then select “New Terminal”). In the Terminal window, type **ps x** to see a list of running processes. Look for a command named `gnome-session` and determine its number under the PID column. Then type **kill -9 PID**, where *PID* is replaced by the PID number. You should see the graphical login screen.

Although these are not the most graceful ways to exit the desktop, they work. You should be able to log in again and restart the desktop.

## Running 3D Accelerated Desktop Effects

The goal of the Accelerated Indirect GL X project (AIGLX) is to add three-dimensional (3D) effects to everyday desktop systems. It does this by implementing OpenGL (<http://opengl.org>) accelerated effects using the Mesa (<www.mesa3d.org>) Open Source OpenGL implementation.

Currently, AIGLX supports a limited set of video cards and implements only a few 3D effects. However, if you have one of those cards, AIGLX features in the current version of CentOS can give you some insights into the eye candy that is to come in later versions.

To use AIGLX, you must have one of the following supported video cards.

- **ATI Video Cards** — The ATI Radeon 7000 through X850 video cards are supported. Generations r100 through r400 are included.
- **Intel Video Cards** — The Intel 8110 and 8330 through i945 Intel video cards are supported.
- **3DFX Video Cards** — 3DFX Voodoo3 through Voodoo5 video cards should work, but have not been tested yet. (3DFX was bought out by NVIDIA a few years ago.)

Because direct rendering infrastructure (DRI) is required for AIGLX, cards that don’t support that feature cannot be used. Support for NVIDIA cards is under development. Although not yet officially supported, the nouveau Xorg driver is an experimental 3D Open Source driver for NVIDIA cards that comes with CentOS. Cards that are known *to work* with AIGLX include ATI Rage 128 and Mach 64, Matrox G200 through G550, and 3DFX Voodoo 1 and 2.

If you have a supported video card, the next trick in getting AIGLX to work in CentOS is to have the right software packages installed. If you have installed the GNOME desktop, you should already have all the packages you need. Those packages include compiz (for the Compiz Window Manager), glx-utils, gtk2-engines, mesa-libGL, mesa-libGLU, and xorg-x11-drv-ati or xorg-x11-drv-i810 (depending on which driver your video card needs).

If your video card was properly detected and configured, you *may* be able to simply turn on the Desktop Effects feature to see the effects that have been implemented so far. To turn on Desktop Effects from the GNOME desktop, select System ► Preferences ► Desktop Effects.

### Getting Started with the Desktop

When the Desktop Effects pop-up window appears, select “Enable Desktop Effects” From the KDE desktop, open the System Settings window, then select Desktop ► Desktop Effects. Then choose “Enable Desktop Effects.” Enabling this does the following:

- Stops the current Window Manager and starts the Compiz Window Manager.
- Enables the “Windows Wobble When Moved” effect. With this effect on, when you grab the title bar of the window to move it, the window will wobble as it moves. Menus and other items that open on the desktop also wobble.
- Enables the “Workspaces on a Cube” effect. Drag a window from the desktop to the right or the left and the desktop will rotate like a cube, with each of your desktop workspaces appearing as a side of that cube. Drop the window on the workspace where you want it to go. You can also click on the Workspace Switcher applet in the bottom panel to rotate the cube to display different workspaces.

The following are some interesting effects you can get with your 3D AIGLX desktop:

- **Spin Cube** — Hold [Ctrl]+[Alt] keys and press right and left arrow keys. The desktop cube spins to each successive workspace (forward or back).
- **Slowly Rotate Cube** — Hold the [Ctrl]+[Alt] keys, press and hold the left mouse button, and move the mouse around on the screen. The cube will move slowly with the mouse among the workspaces.
- **Tab through Windows** — Hold the [Alt] key and press the [Tab] key. You will see reduced versions of all your windows in a strip in the middle of your screen, with the current window highlighted in the middle. Still holding the [Alt] key, press [Tab] or [Shift]+[Tab] to move forward or backward through the windows. Release the keys when the one you want is highlighted.
- **Scale and Separate Windows** — If your desktop is cluttered, hold [Ctrl]+[Alt] and press the up arrow key. Windows will shrink down and separate on the desktop. Still holding [Ctrl]+[Alt], use your arrow keys to highlight the window you want, and release the keys to have that window come to the surface.
- **Scale and Separate Workspaces** — Hold [Ctrl]+[Alt] and press the down arrow key to see reduced images of the workspace shown on a strip. Still holding [Ctrl]+[Alt], use right and left arrow keys to move among the different workspaces. Release the keys when the workspace you want is highlighted.
- **Send Current Window to Next Workspace** — Hold [Ctrl]+[Shift]+[Alt] keys together and press the left and right arrow keys. The current window will move to the next workspace to the left or right, respectively.
- **Slide Windows Around** — Press and hold the left mouse button, and then press the left, right, up, or down arrow keys to slide the current window around on the screen.

If you get tired of wobblling windows and spinning cubes, turning off the AIGLX 3D effects and returning Metacity as the Window Manager can be done quite simply. Just select System ► Preferences ► Desktop Effects again, and toggle off the “Enable Desktop Effects” button to turn off the feature.
