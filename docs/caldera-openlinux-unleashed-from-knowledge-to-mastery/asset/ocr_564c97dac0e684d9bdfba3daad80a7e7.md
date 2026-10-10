Note that each application defines its own window (or widget) hierarchy and class names. Although applications built with the same widget toolkit (a library for building graphical interfaces) are likely to have consistent class names for their windows, X itself does not impose a standard for window class names. (Remember, it provides mechanism, not policy.)

Use the *x* program to set resources. The easiest way to set resources is to create a file (usually called `.Xresources` in your home directory) specifying the resources you wish to set. The file looks something like this:

```
```
! A comment line -- begins with exclamation mark.
Xterm*background: white
Ghostview*arguments: -DNOPLATFONTS
Xterm*font: 10x20
```
```

You simply list the resources followed by a colon and the value. You can continue long lines with the backslash character (`\\`).

Remember that you need to read the manual page for each application to discover which resources it uses or expects.

After you've created the resource file, load it into the X server with this command:

```
```bash
$ x*merge $HOME/.Xresources
```
```

This adds the resources specified in the file to the X resource database. *x* has a number of options:

+   * `x* -query` Queries the X resource database and prints the results to standard output.
+   * `x* -merge` *fileName* Merges resources from a file into the database.
+   * `x* -load` *fileName* Replaces the resources in the database with the resources in the file.

*x* has a number of more advanced (and less used) options for processing resource files; see *x(1)* for more details.

# # Configuring XFree86

Historically, configuring the X server has been one of the most difficult tasks under Linux. However, modern XFree86 servers support a wide range of video cards, and the PCI bus makes identifying hardware easier. Most likely, when you installed Caldera OpenLinux, the installation program correctly configured the X server. If it didn't, or if you wish to reconfigure the X server for some reason (adding a new video card, perhaps), this section will explains how to do it.