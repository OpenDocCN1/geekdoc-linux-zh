![](bbox=[0.1, 0.1, 0.9, 0.32])

# A new world

Getting your Raspberry Pi into the desktop isn’t the only thing you can do on the command line, though. There’s a whole world of functionality built into the command line; in fact, most of the graphical programs you’re using are just executing these commands in such a way. You don’t have to leave the comfort of the desktop environment to perform these commands either, as all Raspberry Pi operating systems will come with an application known as a Terminal emulator.

This creates a window where a command can be written in the same way that we launched the desktop, and use the exact same commands (Fig. 1). On Raspbian, look for the app LX Terminal in the Accessories section of the menu and click on it. If you’ve had to use startx to get into the desktop, then we can now fix that before continuing. In the terminal, enter:

```
$ raspi-config
```

Here’s the initial setup screen (Fig 2). From here you can enable the desktop on boot (Fig 3), and even update the firmware and add support for the official Raspberry Pi camera module. This allows you to modify Raspbian without having to reinstall again.

You won’t be using those two commands very often, though, so is there practical use for delving into the command line? Very much so. For starters, Raspbian doesn’t have an official package manager. This is a program that allows you to browse the available software for the operating system, similar to the Pi Store.

However, there’s other software available to Raspbian that you can’t get through the store. You also can’t specifically update the Pi software either, and all of this can be fixed using the command line.

![](bbox=[0.64, 0.36, 0.9, 0.44])

![](bbox=[0.64, 0.77, 0.9, 0.92])