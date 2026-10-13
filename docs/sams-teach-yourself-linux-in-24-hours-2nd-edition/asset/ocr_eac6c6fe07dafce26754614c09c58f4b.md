Not using X? Don't worry—you can play music CDs with Sariel Har-Peled's cdp command, found under the /usr/bin directory. This command is a text mode program and is started from the command line of your console, like this:

```
# cdp
```

When cdp starts, you see a list of the tracks on your CD. Turn on the NumLock key of your keyboard to control how to play your CD. Table 20.1 lists the controls for playing CDs from your keyboard's keypad.

TABLE 20.1 THE cdp COMMAND KEYPAD CONTROLS

| Action | Keypad Key |
|---|---|
| Soft exit (music continues) | 0 |
| Help | . |
| Back 15 seconds | 1 |
| Hard abort (eject CD) | 2 |
| Forward 15 seconds | 3 |
| Previous track | 4 |
| Replay CD | 5 |
| Next track | 6 |
| Stop | 7 |
| Toggle pause/resume | 8 |
| Play | 9 |

The cdp command has a number of command-line options. A symbolic link, called cdplay, can be used to play music without cdp's interactive screen. Tell cdplay to start playing music at a certain track with the play option, followed by a track number, like this:

```
# cdplay play 3
```

This command line starts the cdp program, and your music CD starts playing from the third track.

# Games for the Console

If you don't use X11, you also can have fun at the console because you can find an assortment of nearly 60 classic games you can play. Look under the /usr/games directory.