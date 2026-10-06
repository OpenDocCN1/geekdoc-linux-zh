# Chapter 2 + Running Commands from the Shell 31

In Linux systems, the $ and # prompts are preceded by your username, system-name, and current directory name. For example, a login prompt for the user named on a computer named /tmp as the current directory would appears as:

```
[jake@pine tmp]$
```

You can change the prompt to display any characters you like — you can use the current directory, the date, the local computer name, or any string of characters as your prompt, for example. To configure your prompt, see the “Setting Your Prompt” section later in this chapter.

Although there are a tremendous number of features available with the shell, it is easy to begin by typing a few commands. Try some of the commands shown in the remainder of this section to become familiar with your current shell environment.

In the examples that follow, the $ and # symbols indicate a prompt. The prompt is followed by the command that you type (and then you press Enter or Return, depending on your keyboard). The lines that follow the output resulting from the command.

# Using a Terminal Window

With the desktop GUI running, you can open a terminal emulator program (sometimes referred as a Terminal window) to start a shell. Most Linux distributions make it easy for you to get to a shell from the GUI. Here are two common ways to launch a Terminal from a Linux desktop:

+   **Right-click the desktop.** In the context menu that appears, for Shells, New Terminal, Terminal Window, Xterm, or some similar item and select it.
**Click on the panel menu.** Many Linux desktops include a panel at the bottom of the screen from which you can launch applications. For example, in Red Linux systems, you can select the Red icon, and choose System Tools > Terminal to open a terminal.

In all cases, you should be able to type a command as you would from a shell with no GUI. There are different terminal emulators available with Linux. One of the following is the default with your Linux system:

+   **xterm** — A common terminal emulator for the X Window System (In fact, I've never seen an X Window System for a major Linux distribution that didn't include xterm). Although it doesn't provide menus or any special features, it is available with most Linux distributions that support a GUI.
**gnome-terminal** — The default Terminal emulator that comes with GNOME. It consumes more system resources than xterm, and it has useful menus for cutting and pasting, opening new Terminal tabs or windows, and setting terminal profiles.