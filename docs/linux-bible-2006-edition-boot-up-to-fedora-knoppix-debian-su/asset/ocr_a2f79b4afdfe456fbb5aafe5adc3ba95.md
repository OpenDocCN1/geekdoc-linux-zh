# Chapter 2 ♦ Running Commands from the Shell

# # Exploring Other Text Editors

Dozens of text editors are available for use with Linux. Here are a few that might be in your Linux distribution, which you can try out if you find vi to be too taxing.

| Text Editor | Description |
|---|---|n| nano | A popular, streamlined text editor that is used with many bootable Linuxes and other limited-space Linux environments. For example, nano is often available to edit text files during a Linux install process. |
| gedit | The GNOME text editor that runs in the GUI. |
| jed | This screen-oriented editor was made for programmers. Using colors, jed can highlight code you create so you can easily read the code and spot errors. Use the Alt key to manipulate your text. |
| joe | The joe editor is similar to many PC editors. Use control and arrows to move around. Press Ctrl+C to exit with no save or Ctrl+X to save and exit. |
| kate | A nice-looking editor that comes in the kdebase package. It has lots of bells and whistles, such as highlighting for different types of programming languages and controls for managing word wrap |
| kedit | A GUI-based text editor that comes with the KDE desktop |
| mcedit | With mcedit, function keys help you get around, save, copy, move, and delete text. Like jed and joe, mcedit is screen-oriented |
| nedit | An excellent programmer's editor. You need to install the optional nedit package to get this editor. |

If you use ssh to log in to other Linux computers on your network, you can use any editor to edit files. A GUI-based editor will pop up on your screen. When no GUI is available, you will need a text editor that runs in the shell, such as vi, jed, or joe.

The vi editor is difficult to learn at first, but once you know it, you never have to use a mouse or a function key—you can edit and move around quickly and efficiently within files just by using the keyboard.

# ## Starting with vi

Most often, you start vi to open a particular file. For example, to open a file called /tmp/test, type the following command:

```
$ vi /tmp/test
```