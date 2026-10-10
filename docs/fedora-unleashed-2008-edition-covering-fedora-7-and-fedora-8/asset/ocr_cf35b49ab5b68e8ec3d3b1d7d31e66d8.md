you can change its appearance by using the PS1 variable like this:

```
$ PS1='$STYPE r001z .>'
```

After you press Enter, you see the following:

```
linux-gnu r001z .>
```

> **NOTE** See the bash man page for other variables you can use for prompt settings.

# # Using the Text Editors

Linux distributions include a number of applications known as *text editors* that you can use to create text files or edit system configuration files. Text editors are similar to word processing programs, but generally have fewer features, work only with text files, and might or might not support spell checking or formatting. The text editors range in features and ease of use, but are found on nearly every Linux distribution. The number of editors installed on your system depends on what software packages you've installed on the system.

Some of the console-based text editors are as follows:

+   - **emacs**—The comprehensive GNU emacs editing environment, which is much more than an editor; see the section \"Working with emacs\" later in this chapter
+   - **joe**—Joe's Own Editor, a text editor, which can be used to emulate other editors
+   - **nano**—A simple text editor similar to the pico text editor included with the pine email program
+   - **vim**—An improved, compatible version of the vi text editor (which we call vi in the rest of this chapter because it has a symbolic link named vi and a symbolically linked manual page)

Note that not all text editors described here are *screen oriented*. Some of the text editors for the X Window System, which provide a graphical interface, such as menu bars, buttons, scrollbars and so on, are the following:

+   - **gedit**—A GUI text editor for GNOME
+   - **kate**—A simple KDE text editor
+   - **kedit**—Another simple KDE text editor

A good reason to learn how to use a text-based editor, such as vi, is that system maintenance and recovery operations generally never take place during X Window sessions