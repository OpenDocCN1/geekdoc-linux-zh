
## Graphics Conversion Commands

Linux provides many different graphics conversion commands. The following is a short list of some of the major commands and families of commands you will find with nearly every distribution.

| Command | Description |
| :--- | :--- |
| **ImageMagick** | Includes the `display`, `import`, `animate`, `montage`, `convert`, `mogrify`, `identify`, and `combine` commands. See the `ImageMagick` manual page or individual manual pages for these commands. The `display` command is a capable, graphical image editor for use during X sessions. |
| **pbm** | A family of 39 portable bitmap file format commands (see the `pbm` manual page for details). |
| **pnm** | A family of 28 portable anymap file format commands (see the `pnm` manual page for details). |
| **pgm** | A family of 19 portable graymap file format commands (see the `pgm` manual page for details). |
| **pbm** | A family of 36 portable bitmap file format commands (see the `pbm` manual page for details). |
| **ppm** | A family of 44 portable pixmap file format commands (see the `ppm` manual page for details). |
| **xcv** | An interactive graphical X client that may also be used from the command line to translate, convert, and edit graphic images. |
| **ee** | The Electric Eyes graphical X client (like `xcv`) that can be used to transform images. |

Many of these commands may be used in shell scripts, or command-line pipes. By combining input and output streams of data, you use many of these commands as building blocks for larger editing applications.

## Audio Mixers and Players

Sound is an integral part of conducting business and doing work on a personal computer. Though many Mac OS users may turn off the Speech Manager, sound is often important during a Linux X session. Your X window manager provides visual as well as audio feedback in response to system events. This lets you know when applications quit, windows open, or buttons are clicked.

Many Linux users enjoy listening to music while working. Whether its playing an audio CD or listening to an .mp3 audio stream over the network, music can help make work easier. You will find numerous audio clients included with your Linux distribution and soon you will develop one or two favorites for each type of task.

These tasks can include using audio CD players, controlling sound with mixers, recording sound, creating .mp3 files, and listening to .mp3 files. Obviously, Linux must be configured to use your computer’s sound hardware. For many Macintosh PowerPC models, this is accomplished by loading the dmasound.o kernel module. Other models, such as the Apple G4 Cube (which uses USB audio), will use the audio.o module.

### Using Mixers

Audio mixers are used to adjust the volume, balance, treble, and bass of your computer’s sound system. Linux provides audio mixers that can be used from the text-only console, and graphical interface mixer clients that must be used during an X session. For example, the aumix client may be used at the console or in a terminal window. Start the client, like this:

```
$ aumix
```

The screen will clear, and you will see a display as shown in Figure 13.10.

When launched this way, the mixer is interactive. Use the Up and Down cursor keys to navigate through the sound controls, and use the Left and Right cursor keys to adjust the sound. Tap a letter, as indicated by the menu of commands, to save or quit the client. You can also use `amix` from the command line to adjust sound, like this:

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

![](img/1ea833f5a3e3c1547e3dd2891f52804a_331_0.png)
Figure 13.10 The aumix command may be used interactively or as a command-line mixer with or without X.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_332_0.png)
**Figure 13.11** *Use the `kmix` client during your KDE X sessions to control your system's audio levels.*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_333_0.png)
Figure 13.12 The gmix client is used for audio control during GNOME sessions.

After you press Enter, you will see the mixer appear in a window as shown in Figure 13.12.

### Playing Audio

Linux provides a number of sound players, or commands you can use to play a sound file. One of the most popular of the command-line utilities is the sox command. Its symbolic link, the play command, can be used to play a .wav file, like this:

```
$ play /usr/share/sounds/test.wav
```

You will also find many different sound files installed on your system. Look under the /usr/share/sounds directory. SuSE PPC Linux users will also find four directories of sounds in different formats that may be played or converted for use during X sessions (KDE, GNOME, and other X window managers can use sounds for various system events).

Every Linux distribution includes several audio CD players. These players vary in capabilities and purpose. For example, the Window Maker window manager includes a tiny CD player applet named wmcddplay that can dock in Window Maker's desktop wharf. Many audio CD players, such as KDE’s kscd and GNOME players, have advanced features such as automatic retrieval of artist and title and track information from remote database servers (if run during an active Internet connection).

KDE’s kscd client (shown in Figure 13.13) is a network-aware audio CD player and features a configuration dialog box you can use to choose a specific Internet music database. Start this client from KDE’s desktop panel or the command line of an X terminal window, like this:

```
$ kscd &
```

After you press Enter, insert an audio CD. If you have an active Internet connection and your audio CD is recognized by the default remote database (most likely freedb.freedb.org), the information about your CD will be retrieved, displayed by the player, and saved on your system.

GNOME’s audio CD player, gcdc, like KDE’s player, will also search remote Internet databases for your CD’s artist, title, and track information. This client (shown in Figure 13.14) may be started from the desktop panel or the command line of an X terminal, like this:

```
$ gcdc &
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_334_0.png)
Figure 13.13 The kscd client will not only play CDs, but also search the Internet for track and title information about your CD.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_334_1.png)
Figure 13.14 GNOME’s gcdc client also searches the Internet for track and title information about your CD.

## Problems Playing Audio CDs on Your PowerPC?

Playing audio CDs generally poses less of a problem on Intel-based PC hardware. However, PowerPC Linux users with slot-loading CD-ROM drives (such as the Apple G4 Cube and Titanium PowerBook) may experience problems playing audio CDs. One solution is to follow the initial directions outlined below in “Playing DVDs” to load the ide-scsi.o kernel module and create /dev/sr0 (along with the symbolic link /dev/cdrom). You can then insert an audio CD and play selected tracks with the cdda2wav command, which strips selected audio tracks directly from a CD, converts the track to .wav audio file format, and plays the stream all in one step!

For example, the following script can be typed in a text file with the name myplaycd, like this:

```
cdda2wav -t $1 -D /dev/cdrom -M -e -q -x -d0 "-I cooked_isoct 1 &"
```

Save the file, then use chmod +x myplaycd to make the file executable. You can then insert an audio CD, and play selected tracks, such as track 2-6, like this: myplaycd "2\*". For an explanation of cdda2wav's command-line options, see its manual page.

## Using the xmms Client

The .mp3 audio format reigns as the leading compressed digital audio format for Linux and many Internet users. All Linux distributions include .mp3 or MPEG audio players for the command-line, such as the mpg123 command. Use this command to play one or more audio files, like this:

```
$ mpg123 *.mp3
```

The most widely used graphical interface player is the xmms client, shown in Figure 13.15. This client may be launched from your window manager’s multimedia menu or the command line of an X terminal, like this:

```
$ xmms &
```

This player can provide an easy way to play selected albums, tracks, or collected playlists of tracks from a variety of audio CDs. Many Linux users within a local network use this client to play music that resides on remote servers, with the remote filesystem mounted locally.
