> **TIP**: To add an application so that it appears in your GNOME desktop Panel, open the GNOME menu and choose Panel → Add to Panel → Launcher. Fill in the fields needed to identify the application. In the Command field, type in the command name and the options that you like. Click the icon box to select an icon to represent the command. Click OK when you are done, and the application appears on the launcher.

Here is a procedure to run X applications from a Terminal window.

+   1. Open a Terminal window from your desktop (look for a Terminal icon on your Panel or a Terminal selection on a menu.)
+   2. Type

```
`$ echo $DISPLAY`
```

The result should be something similar to the following:

```
`:0`
```

This indicates that the Terminal window will, by default, direct any X application you run from this window to display 0 on your system. (If you don't see a value when you type that command, type `export DISPLAY=:0` to set the display value.)

+   3. Type the following command:

```
`$ xmms &`
```

The `xmms` program should appear on your desktop, ready to work with. You should note the following:

+   - The `xmms` command runs in the background of the Terminal window (`&`). This means that you can continue to use the Terminal window while `xmms` is running. Because it is a child process of the Terminal window, `xmms` will close if you close the Terminal window.
+   
+   - I encountered no errors running `xmms` on this occasion. With other applications, however, text sometimes appeared in the Terminal window after the command was run. The text may say that the command can't find certain information or that certain fonts or colors cannot be displayed. That information would have been lost if the command were run from a menu.

+   4. If you want to know what options are available, type:

```
`$ xmms --help`
```

+   5. Try it with a few options. For example, if you want to begin by playing a file and you have a WAV audio file named `file.wav`, you could type:

```
`$ xmms file.wav`
```

> **CROSS-REFERENCE**: Refer to Chapter 4 for information on X resources and options that are available to most X commands.