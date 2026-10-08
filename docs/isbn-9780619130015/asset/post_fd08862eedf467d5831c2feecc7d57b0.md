
![](img/6d8286a85e2d8ad63e16f1801102da59_434_0.png)

Figure 11-1: Typical X Window screen

## X Window Clients and Servers

Although you can easily use the X Window system to run programs stored on your local computer, you can also run applications over a network. X Window uses a client/server model where a program can run on one computer but display its output on another. For example, suppose you have a network with two computers: system A and system B. The user on system A can invoke and run a program that resides on system B. Although the user of system A sees the program running in a window on his or her computer, it might actually be executing on system B. This interaction is transparent to the user of system A, who may not know the program is actually running on a different computer. Additionally, systems A and B can be different types of computers, each running a different variation of UNIX.

In X Window network terminology, the desktop system that the user runs a program from is called the **X server**. The system that hosts and executes the program is called the **X client**.

> Note: In normal network terminology, the server is the system that hosts a program, and the client is the system run by the user. In X Window jargon, the terms client and server mean the opposite. The terms are reversed because the X Window server (on the desktop) performs operations requested by the client (on the host system). For example, the client might request that the server display a window or ask the server to move a window to a different position on the screen.

## Window Managers

Like the UNIX operating system itself, the X Window system is layered and built from components. At the top layer is the **Window Manager**. The Window Manager controls how windows appear and how users control them. In many regards, the Window Manager is to the X Window system as the shell is to UNIX: each provides the user an interface to the underlying components.

Many Window Managers have been developed, and most of them are available for free. Linux supports over 50 different ones. Table 11-1 lists some common Window Managers currently in use.

| Window Manager | Description |
|---|---|
| AnotherLevel | Based on the fvwm Window Manager and commonly used with Red Hat Linux |
| CDE | Common Desktop Environment |
| Enlightenment | Popular Window Manager sometimes called E. Also commonly used with Red Hat Linux. |
| fvwm | Virtual Window Manager |
| fvwm95 | Version of fvwm with a Windows 95 look and feel |
| kwm | Windows manager used by KDE |
| olwm | Open Look Window Manager |
| mwm | Motif Window Manager |
| twm | Tab Window Manager or Tom's Window Manager |

Table 11-1: Common Window Managers

## Using GNOME

The **GNU Network Object Model Environment (GNOME)**, a product of the GNU project, is not a Window Manager, but a desktop environment that must be used along with a Window Manager. By default, Red Hat 6 installs the Enlightenment Window Manager with GNOME (pronounced “guh-nome”). All examples in this chapter use Enlightenment and GNOME.

> Note: The GNU project is an organization with the stated purpose of developing a free, UNIX-like, operating system named GNU. The Linux kernel is used in many GNU distributions. The project's Web site is www.gnu.org.

## Starting the X Window System

If your system does not start the X Window system automatically, you may invoke it by using the startx command.

> **To start the X Window System (if your system does not automatically start it):**
>
> - Type **startx** and press **Enter**.
>
> You see a display similar to Figure 11-2.

![](img/6d8286a85e2d8ad63e16f1801102da59_436_0.png)

**Figure 11-2:** Introductory X Window/GNOME screen

## Configuring Linux to Automatically Start the X Window System

If your system does not automatically start the X Window system, you may configure it to do so. This is accomplished by modifying a line in the file /etc/inittab.

> **To view the contents of /etc/inittab:**
>
> 1. Type **more /etc/inittab** and press **Enter**. Your screen looks similar to Figure 11-3.

![](img/6d8286a85e2d8ad63e16f1801102da59_437_0.png)

1. Look for the line that reads:
   `id:3:initdefault`
2. Type q to exit the more command.

The code shown above establishes the operating system’s default run level, or mode of operation, at 3. Run level 3 is full multi-user mode. By raising the run level to 5, the system starts in X11 mode, which automatically starts the X Window system.

Note: Configuring your system requires superuser privileges. You must be able to log on as root to complete the following exercise.

Caution: You should be very careful any time you log on as root. Because the root user has privileges to alter any part of the system configuration and delete any file, you could accidentally corrupt the operating system.

The next exercise is optional and assumes you have been given permission to log on as root. Root access is required to modify the inittab file as described in the exercise.

### To configure your system to start the X Window system automatically:

1. Log out of the system, and log back on as root.
2. Change your current working directory to /etc.
3. Make a back-up copy of the inittab file. Use a command such as `cp inittab inittab.safe`, and press Enter. You could restore the back-up copy if you accidentally corrupt the inittab file.
4. Open the inittab file in vi or Emacs.
5. Change the line:
   ```
   id:3:initdefault
   ```
   to
   ```
   id:5:initdefault
   ```
6. Save the file and exit the editor.
7. Force the init program to reread its configuration file (inittab) and switch into Run level 5 by typing `init q` and pressing Enter.
8. After a few moments, you see the X Window System graphical login screen. Log on with your normal user name and password.

Now that you know how to start the X Window system, you are ready to learn to navigate it and control its common components.

## Interacting with the X Window System

You interact with the X Window environment through its many components. Figure 11-4 shows the opening GNOME screen, with its major components labeled.

Here is a description of the components in Figure 11-4.

- **Icons**: There are a number of icons, or small images, on the screen. Each causes an action to take place when activated. You activate an icon by positioning the mouse pointer over it and clicking the left mouse button.
- **GNOME Panel**: This component is a strip that runs across the bottom of the screen, and includes a number of icons. Each icon invokes an applet when activated. An applet is a small application written specifically to be placed on the panel.
- **Windows**: Every program, application, or applet that runs under the X Window system runs in a window. Windows have many of their own components, which you will learn about in this chapter.
- **Desktop Area**: This is the background area that holds the windows and icons you are working with during your X Window session.

Now that you can identify the major components of the GNOME screen, you will learn to interact with each one.

![](img/6d8286a85e2d8ad63e16f1801102da59_439_0.png)

## Interacting with Windows

Windows have their own components, as shown in Figure 11-5.

Here is a description of the window components.

- **Border**: Each window is outlined with a border.
- **Title Bar**: At the top of the window border is a title bar. The title bar lists the name of the window or the application running in the window.
- **Window Options button**: Click this button to see a menu offering several useful window operations.
- **Iconify button**: Click this button to collapse the window into a small icon. The icon appears in a section of the panel known as the Pager. The program in the window is still running but is hidden from sight.
- **Minimize/Maximize button**: Click this button to alternately expand the window to fill the screen and reduce the window to its original size.
- **Close button**: Click this button to close the window and terminate the application running in it.
- **Scroll bar**: If a window contains more information than it can display, you see a scroll bar. The scroll bar lets you scroll through all the window's content.
