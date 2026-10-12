
## Running X Window Applications

Setting up and configuring the X Window System to your liking is the hard part. By comparison, using X to run applications is relatively easy. If you have used Microsoft Windows operating systems, you already know the most basic ways of running an application from a graphical desktop. X, however, provides a much more flexible environment for running native Linux applications.

**CROSS-REFERENCE:** See Chapter 4 for information on setting up an X desktop.

## Starting applications from a menu

To run applications on your own desktop, most X window managers provide a menu, similar to the Microsoft Start menu, to display and select X applications. Applications are usually organized in categories, typically under the Programs submenu selection. Open the Programs menu, select the category, and then select the application to run. Figure 5-1 shows an example of the GNOME Main Menu and the Programs submenu.

![](img/1744bde8c889adfab3fc911e1687fecf_214_0.png)

## Starting applications from a Run Program window

Not all installed applications appear on the menus provided with your window manager. For running other applications, some window managers provide a window, similar to the GNOME Run Program window, that lets you type in the name of the program you want to run.

To access the Run Program window:

1. Open the GNOME Main Menu.
2. Click Run. The Run Program window displays a list of programs you can select from.
3. Click the program you want and then click Run.

If the application you want isn’t on the list, you can click Advanced. Then you can either type the command you want to run (along with any options) and click Run, or you can click Browse to browse through your directories to select a program to run. If you are running a program that needs to run in a Terminal window, such as the vi command, click the Run in Terminal button before running the command. Figure 5-2 is an example of the Run Program window.

![](img/1744bde8c889adfab3fc911e1687fecf_215_0.png)

## Starting applications from a Terminal window

I often prefer to run an X application, at least for the first time, from a Terminal window. There are several reasons why I prefer a Terminal window to selecting an application from a menu or Run Program window:

- If there is a problem with the application, you get to see error messages. Applications usually just fail silently if an application that is started from a menu or Run Program window fails.
- Applications selected from menus are run with set options. If you want to change those options, you have to change the configuration file that set up the menu and make the changes there.
- If you want to try out a few different options with an application, a Terminal window is an easy way to start it, stop it, and change its options.

When you have found an application and figured out the options that you like, you can add it to a menu or a panel (if your window manager supports those features). In that way, you can run a program exactly as you want, instead of the way it is given to you on a menu.

> **TIP**: To add an application so that it appears in your GNOME desktop Panel, open the GNOME menu and choose Panel → Add to Panel → Launcher. Fill in the fields needed to identify the application. In the Command field, type in the command name and the options that you like. Click the icon box to select an icon to represent the command. Click OK when you are done, and the application appears on the launcher.

Here is a procedure to run X applications from a Terminal window.

1. Open a Terminal window from your desktop (look for a Terminal icon on your Panel or a Terminal selection on a menu.)
2. Type:
   ```bash
   $ echo $DISPLAY
   ```
   The result should be something similar to the following:
   ```
   :0
   ```
   This indicates that the Terminal window will, by default, direct any X application you run from this window to display 0 on your system. (If you don't see a value when you type that command, type `export DISPLAY=:0` to set the display value.)
3. Type the following command:
   ```bash
   $ xmms &
   ```
   The `xmms` program should appear on your desktop, ready to work with. You should note the following:
   - The `xmms` command runs in the background of the Terminal window (`&`). This means that you can continue to use the Terminal window while `xmms` is running. Because it is a child process of the Terminal window, `xmms` will close if you close the Terminal window.
   - I encountered no errors running `xmms` on this occasion. With other applications, however, text sometimes appeared in the Terminal window after the command was run. The text may say that the command can't find certain information or that certain fonts or colors cannot be displayed. That information would have been lost if the command were run from a menu.
4. If you want to know what options are available, type:
   ```bash
   $ xmms --help
   ```
5. Try it with a few options. For example, if you want to begin by playing a file and you have a WAV audio file named `file.wav`, you could type:
   ```bash
   $ xmms file.wav
   ```
6. When you are ready to close the window, you can either do so from the `xmms` window (right-click on the `xmms` window and select *Exit*) or you can kill the process in the *Terminal* window. Type *jobs* to see the job number of the process. If it was job number 2, for example, you would type *kill %2* to kill the *xmms* program.

**CROSS-REFERENCE:** Refer to Chapter 4 for information on X resources and options that are available to most X commands.

You should try running a few other X commands. Many X commands are stored in /usr/X11R6/bin. A few of these commands are described in the following sections.

## Using X Window utilities

A common set of X utilities comes with most versions of the X Window System. The *Terminal* window (*xterm* command) is a useful X Window utility because it enables you to run other commands and utilities. To get a feel for using X utilities, try several, such as a simple text editor (*xedit*), a calculator (*xcalc*), and some clock programs (*xclock*, *wmclock*, and *xdalclock*).

## Using a Terminal window

The UNIX system, on which Red Hat Linux is based, began as a completely text-based system. There were no colors or graphics. There was no mouse. Everything had to be done by typing letters, numbers, and special keys (for example, function keys, Ctrl, Alt, and so on) from a keyboard. The shell command interpreter (usually just referred to as the *shell*) interpreted the keystrokes.

> **CROSS-REFERENCE:** See Chapter 3 for a description of the shell command interpreter.

If you are accessing Red Hat Linux from the X Window System, the *Terminal* window provides your text-based interface to Linux. As you use Red Hat Linux, you will find that there are many times when you want to use a *Terminal* window. Moving up and down the file system can be quicker in a *Terminal* window than in a file manager. Some useful utilities don't have graphical equivalents. And, as I stated earlier, there are even reasons for starting X applications from a *Terminal* window.

Every window manager provides a menu selection for one or more ways of opening a *Terminal* window. As an alternative, there are several different commands available with Red Hat Linux that can be used to start a *Terminal* window, like the following:

- *xterm* — This is the most common command used to open a *Terminal* window. Most other *Terminal* windows are based on this command.
- *rxvt* — A reduced-size *Terminal* window, which is designed to run more efficiently.
- *gnome-terminal* — A *Terminal* window available with the GNOME window manager.

If you are using the GNOME desktop environment, which is the default, several features make it easier for you to customize the GNOME Terminal window (the gnome-terminal command launches this window). This window has a menu bar that offers File, Settings, and Help buttons. Figure 5-3 shows a GNOME Terminal window.

![](img/1744bde8c889adfab3fc911e1687fecf_218_0.png)

Figure 5-3: An added menu bar helps customize the GNOME Terminal window.

With the GNOME Terminal window, you can change the Terminal window attributes by selecting Settings → Preferences instead of messing around with command-line options or X resources. From the window that appears, you can change the following Terminal window preferences:

- Font
- Bold text
- Blinking cursor
- Menu bar (hidden or not)
- Terminal bell (silent or not)
- Erase key (DEL or backspace)
- Background image
- Color (foreground and background)
- Scrolling (scrollbar position and number of scrollback lines)

If you get really stuck, you can click Help to view the GNOME Terminal User’s Guide.

## Using a text editor

One of the most intimidating tasks in Linux is learning to use a text editor. The most popular editors are vi and emacs. People who use one of these editors typically claim that their editor is the most powerful and easy to use. The truth is that both take some time to learn.

> **CROSS-REFERENCE:** See Chapter 3 for a description of how to use the vi editor.
