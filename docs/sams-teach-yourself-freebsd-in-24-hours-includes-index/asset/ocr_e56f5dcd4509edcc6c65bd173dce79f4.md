FIGURE 21.1
The XMMS MP3 player. Windows users who have used Winamp in the past will not have any problem getting used to XMMS.

![](bbox=[0.35, 0.17, 0.48, 0.38])

# CD Player

KDE also comes with a CD player. The CD player supports the CDDB system, which means that it can automatically download album and track information from the Internet. Figure 21.2 shows the KDE CD player.

FIGURE 21.2
The KDE CD player.

![](bbox=[0.35, 0.54, 0.6, 0.62])

# Mixers

FreeBSD comes with a mixer that can be accessed from the command line. To simply display the current mixer settings, just type mixer at the command prompt, and press Enter. Here is some sample output from the mixer command:

```
Mixer vol   is currently set to 90:90
Mixer bass  is currently set to 75:75
Mixer treble is currently set to 75:75
Mixer synth is currently set to 75:75
Mixer pcm   is currently set to 75:75
Mixer speaker is currently set to 75:75
Mixer line  is currently set to 75:75
Mixer mic   is currently set to 32:32
Mixer cd    is currently set to 75:75
Mixer mix   is currently set to 0:0
Mixer igain is currently set to 75:75
Mixer ogain is currently set to 75:75
```

To change one of the settings, type mixer, followed by the name of the setting that you want to change, followed by a number from 1 to 100. For example, the command

```
mixer vol 50
```