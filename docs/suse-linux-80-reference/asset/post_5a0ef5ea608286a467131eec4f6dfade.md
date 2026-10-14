
## Loading Sound Fonts (SB Live! and AWE)

The package uses the `sfload` command for loading sound fonts in Soundblaster AWE and Live! cards. The relevant sound font files can be found on your sound card’s driver CD. The ALSA start-up script can automatically load the required sound fonts for the WaveTable synthesis, if the appropriate files pertaining to the Creative Driver CD have been installed with YaST2. Currently, the script only works for one sound card. However, ALSA can easily manage up to eight sound cards. Then load the sound fonts with the command `sfload -D n /usr/share/sfbank/creative/8MBGM.SF2`. `{n}` stands for the number of the sound card. This number does not necessarily correspond to the order in which the cards were configured. Find the number in YaST2 under ‘Hardware’.

If your driver CD is not available, you can also load already installed sound fonts in `/usr/share/sounds/sf2`. The sound font `Vintage_Dreams_Waves_v2.sf2` by Ian Wilson contains 128 analog synthesizer sounds and 8 drum sets. It is compatible with both SB AWE and SB Live! cards. The ROM sound font `gun1-rom.sf2` by Samuel Collins is only compatible with SB AWE cards. It provides an extended general MIDI bank for these cards. Review the copyright files and documentation in `/usr/share/doc/packages/snd_sf2`. More sound fonts can be found on the Internet. See `http://www.hammersound.net`.

> **Tip**
> 
> ALSA currently only supports a maximum sound font size of 32 MB.

## vkeybd — Virtual MIDI Keyboard

If you do not have an external MIDI keyboard connected to your sound card, use the virtual keyboard vkeybd. The internal port numbers listed previously via `pmidi -l` are especially of importance here. The application is started at the command line by entering `vkeybd --addr 73:0`. The port address might differ on your system. Specify the first WaveTable port in the list. If an external sound generator is connected, you can specify the external MIDI port here.

vkeybd recognizes a series of additional options. Increase the number of octaves to five, for example, with `vkeybd --addr 73:0 --octave 5`. Obtain a summary of the command line options with `vkeybd --help` or in the man page for vkeybd (`man vkeybd`).

![](img/a4b6c994843f3fbd688003f4cabfa48f_195_0.png)

*Figure 8.5: vkeybd — Complete Virtual MIDI Keyboard*

The instrument names in the preset list are configurable by specifying a preset file using the `--preset` option. The instrument names of a sound font file can be extracted from it with the `sftovkb` command:

```
earth:~# sf2 /usr/share/sounds/sf2
earth:/usr/share/sounds/sf2 # sftovkb Vintage_Dreams_Waves_v2.sf2 \
        ~/vintage.vkb
```

This command saves the names to a file your home directory called vintage.vkb. The vkeybd interface can be configured under ‘View’.

## Setting Up Connections Between MIDI Ports

ALSA provides a sophisticated infrastructure for the connection of several MIDI ports. Sound cards and MIDI applications (provided that they support the ALSA sequencer structure) have one or more MIDI ports for communicating with each other. These ports can either be connected with the KDE application kaconnect or with aconnect. After it starts, kaconnect shows the readable and writable MIDI ports available on your system and existing connections. To see a demonstration of this, start two MIDI applications with vkeybd and aseqview. Specify the port address after the application name. The first application is assigned the port number 128:0, for example, and the second, 129:0. A list of the application ports can also be obtained in kaconnect.

![](img/a4b6c994843f3fbd688003f4cabfa48f_196_0.png)

*Figure 8.6: Connecting MIDI Ports with kaconnect*

The connection between the application port and the WaveTable (or external MIDI port) can now be configured manually. To do this, select the corresponding ports then click ‘connect’. If you prefer using the command line tool aconnect instead, enter something like `aconnect 128:0 73:0`. This sets up a (unidirectional) connection between port 128:0 as sender and 73:0 as receiver.

You can now set up a connection between the MIDI port of the keyboard and the MIDI port of the ALSA sequencer viewer. If you alter keyboard settings, such as panning or the pitch wheel (which must first be enabled under ‘View’), these changes will be immediately reflected in qseqview.

View a list of ports available for receiving and sending and their connection status by entering `aconnect --i` or `aconnect --o`. The connection set up with aconnect can be terminated by specifying the option `--d`, as in `aconnect --d 128:0 129:0`.

To terminate all connections, enter `aconnect --x`. A list of further command line options in aconnect can be viewed in the man page for aconnect (`man aconnect`).

> **Tip**
> 
> For experts: aseqnet allows you to set up MIDI connections beyond your own machine over the network. Maybe you want to play a piano duet with an old friend in Germany.

## kmid — The KDE MIDI Player

series kde2, package kdemultimedia

![](img/a4b6c994843f3fbd688003f4cabfa48f_197_0.png)

*Figure 8.7: Main Window and Channel View in kmid*

In the KDE start menu, find ‘Multimedia’ → ‘Midi/Karaoke Player’. A few demo files for this format are located in the /opt/kde2/share/apps/kmid directory in .kar format. These files also contain the lyrics, which are scrolled and highlighted in sync with the playback.

MIDI files can be found on the Internet. One suggested address is http://www.midi.net. A comprehensive MIDI archive of classical music is located at http://www.classicalarchives.com.

The detailed online help of kmid can be opened with (F1). In this application, the MIDI ports must be correctly established with ‘Settings’ → ‘MIDI Settings’. Especially worth mentioning is the channel view you can select by clicking the keyboard button in the tool list. You may have to drag the window slightly to the right to be able to see this item. The MIDI events are displayed graphically on several keyboards in the channel view — whereby you may also have to adjust the size of the window. The instruments can be changed here as well.

There is, however, a potential catch with this application. If kmid is launched by clicking on a MIDI file in the KDE file manager Konqueror, the MIDI settings specified in the KDE Control Center will apply. The configuration specified in the application itself only applies if you start the application separately.

## Playing MIDI Files Without a WaveTable Card

series snd, package timidity

Not every sound card has a WaveTable synthesizer for playing back MIDI files according to the loaded sound font (or instrument patch). If this is your situation, the software WaveTable synthesizer timidity++ is designed to meet your needs.

### Configuring timidity++

timidity++ is configured in the configuration file /usr/share/timidity/timidity.cfg. Specific documentation is available for its configuration, which can be viewed by entering man timidity.cfg. Refer to the documentation in /usr/share/doc/packages/timidity.

Compatible instrument patches can be obtained at http://www.stardate.bc.ca/eawpatches/html/default.htm. Load the file eawpats11_full.rar from there. This file is 22 MB in size, but it is well worth it. It contains a complete GM/GS/XG instrument set. To use the patches with timidity, you must proceed as follows.

Switch to root. Create a directory /usr/share/timidity/eawpats, copy eawpats11_full.rar to that location, then change to that directory. The command unrar x eawpats11_full.rar unpacks the archive. The timidity.cfg in the /usr/share/timidity/ directory must now be modified. This file only needs to contain the following two lines.

```text
dir /usr/share/timidity/eawpats
source timidity.cfg
```

*File 14: timidity.cfg*

Caution: eawpats11_full.rar contains another timidity.cfg, which will show up in the eawpats directory after it is decompressed. This file is included by the source command in the timidity.cfg above. Only four lines in this file are of importance:
