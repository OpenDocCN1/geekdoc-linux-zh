save or quit the client. You can also use `amix` from the command line to adjust sound, like this:

```
$ amix -v +20
```

In this example, after you press Enter, the main volume sound will increase 20 percent. Using `amix` is a convenient way to include sound management in shell scripts or other programs.

> Is your PowerPC sound level too low or too high by default? Boot to Mac OS and check the sound level. In many cases, Linux will inherit sound settings established during a previous Mac OS session. In addition, some sound systems, such as the G4 Cube, will not respond to `amix` main volume settings. Use `amix -w +20` instead.

Christian Esken's `kmix` audio mixer client, included with KDE, features slider controls and split channels, along with graduated marks. Start this client (shown in Figure 13.11) from the desktop's panel or the command line of an X11 terminal window, like this:

```
$ kmix &
```

Note that your mixer may look different than the one shown in Figure 13.11, which is for an Apple G4 Cube (it provides audio via USB). The `kmix` client can also dock or embed itself in the KDE panel. To use the embedded client, click on its icon in the panel to access its features. GNOME users will turn to the `gmix` client, which provides slider controls and mute buttons. Start this GNOME client from the desktop's panel or the command line of an X11 terminal window, like this:

```
$ gmix &
```

![](bbox=[0.05, 0.74, 0.18, 0.91])

**Figure 13.11** *Use the `kmix` client during your KDE X sessions to control your system's audio levels.*