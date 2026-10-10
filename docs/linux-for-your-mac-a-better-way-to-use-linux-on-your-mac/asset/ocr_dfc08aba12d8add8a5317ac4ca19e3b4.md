![](bbox=[0.16, 0.05, 0.32, 0.2])

Figure 13.12 The gmix client is used for audio control during GNOME sessions.

After you press Enter, you will see the mixer appear in a window as shown in Figure 13.12.

# ### Playing Audio

Linux provides a number of sound players, or commands you can use to play a sound file. One of the most popular of the command-line utilities is the sox command. Its symbolic link, the play command, can be used to play a .wav file, like this:

```
$ play /usr/share/sounds/test.wav
```

You will also find many different sound files installed on your system. Look under the /usr/share/sounds directory. SuSE PPC Linux users will also find four directories of sounds in different formats that may be played or converted for use during X sessions (KDE, GNOME, and other X window managers can use sounds for various system events).

Every Linux distribution includes several audio CD players. These players vary in capabilities and purpose. For example, the Window Maker window manager includes a tiny CD player applet named wmcddplay that can dock in Window Maker's desktop wharf. Many never audio CD players, such as KDE’s kscd and GNOME players, have advanced features such as automatic retrieval of artist and title and track information from remote database servers (if run during an active Internet connection).

KDE’s kscd client (shown in Figure 13.13) is a network-aware audio CD player and features a configuration dialog box you can use to choose a specific Internet music database. Start this client from KDE’s desktop panel or the command line of an X terminal window, like this:

```
$ kscd &
```

After you press Enter, insert an audio CD. If you have an active Internet connection and your audio CD is recognized by the default remote database (most likely