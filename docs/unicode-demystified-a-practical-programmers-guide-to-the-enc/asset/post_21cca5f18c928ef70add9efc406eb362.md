
# KDE Control Center Personalization (Continued)

| Remove Schema | Removes the highlighted schema. |
| --- | --- |
| Background | Specifies an image to use as the background and the transparency of the Konole window. |
| Session | Specifies the names and properties of Konsole sessions that you can select when you click and hold the New button on the Konsole toolbar (page 278). You can add and re-move sessions as you please. |
| Write Daemon | Starts the daemon that allows you to write (page 84) under KDE on your machine. |
| Passwords | Controls how kdesu, the program that puts up the dialog box asking for the root password works. The first frame controls how the password you enter is entered: 1 star echoes one * for each character you enter, 3 stars echo *** for each character you, and no echo echoes nothing. Check Remember passwords to pass kdesu to remember and not ask you for the root password for the number of minutes you specify on the spinner. |

General specifies whether to display the End session dialog box to confirm a command to log out and whether the Save sessions for future logins in the same dialog box has a check mark in it. Refer to "Session Manager" on page 185 for more information on session management.

Default action after logout specifies what KDE should take after you log out.

Spell Checking sets aspell options for KDE applications.(The aspell utility is no longer used; the file with name is now a brief script that translates aspell command lines into aspell options.) Refer to /usr/share/doc/aspell-*/man/html/index.html for more information. Look for aspell to merge with pspell (see pspell.source-forge).

# Pilot/Handspring Tool

The Pilot/Handspring Tool section of the Control Center establishes a connection with your Pilot or Handspring PDA and allows you to work with the device.

# Power Control

The Power Control section of the Control Center (Table 8-19) controls battery operation and monitoring for battery-powered computers and energy conservation settings for the monitor.

# Chapter 8 KDE Desktop Environment

# KDE Control Center↔ Power Control

| Battery Monitor | For computers that run on batteries. Displays the Battery Monitor and specifies often to check (poll) the battery and icons to display in the Battery Monitor. |
| Energy | For Energy Star Compliant monitors. Specifies how long KDE puts the monitor in a Standby (minimum energy savings and a quick return to an active state), Suspend (large energy savings and a slow return to an active state), or Power Off (maximum energy savings and the slowest return to an active state). The time specifies when you start at the last use of the keyboard or mouse. KDE activates the monitor when you use the mouse or keyboard again; use a key that will not have any effect, such as the CONTROL key. |
| Laptop & Low Battery | Specifies what happens when the battery on a laptop runs down. |

# Sound

The Sound section of the Control Center (Table 8-20) controls various aspects of system sound including the system bell and system notifications.

# KDE Control Center↔ Sound

| Audio CD-Slave | Allows you to change settings for audio. Each of the tabs covers device, encoding, or information: CDDA (CD-ROM digital audio), Ogg Vorbis (a format for encoding files, similar to MP3 but free with smaller sizes and better fidelity, www.vorbis.com), MP3, and CDDB (CD-ROM database; lets you look up title and track information for CD-ROM; www.cddb.com). |
| Midi | Specifies the Midi device KDE uses. When you want to Midi, check the Midi box and specify the program to use. |
| Mixer | Configures basic options of the KDE mixer, kmix. You can save the current volumes as the defaults, restore the default volumes, and specify that KDE load the default volumes when you log in. Maximum number of probed mixers specifies the number of sound cards in the system. kmix stops looking after it finds many cards. Maximum number of devices per mixer specifies how many devices kmix should look for each soundcard. Increase this number if kmix does not find your devices. |
| Sound Server | Refer to “Sound” on page 346 for information. |
| General | |

# KDE Control Center ⇔ Sound (Continued)

| Start soundserver on startup | Starts the soundserver when KDE starts up. You may still hear system sounds when the soundserver is not running because a separate program is used as a fallback. KDE-based multimedia applications, such as, require the soundserver to be running. |
| Enable network transparency | For advanced users: Allows to send audio over the network and have it played on another computer. |
| Exchange security over X11 server | For advanced users: Enables a secure method of communication between soundservers. |
| Run soundserver with realtime priority | Refer to "Sound" on page 346. |
| Autosuspend if idle for n seconds | Allows non-enabled programs to use the sound device when idle. Also you may find that your system is more responsive if you allow to suspend when you are playing only system sounds. |
| Display messages using | Specifies how soundserver should communicate to you: for example, when it cannot find the soundcard there is usually no reason to change the default. |
| Message Display | Specifies which messages you want to see. |
| Sound I/O method | The soundserver can output audio using various methods depends on packages installed on your system. The usual method is by using OSS (Open Sound System), which is the standard GNU/Linux audio output system, and is automatically detected (Autodetect). Change this option only if you understand other output methods. |
| Enable full duplex operation | Enables simultaneous recording and playing of audio. Usually, kmix configures the card to allow only input or output but not both at the time. Some soundcards do not work properly with duplex enabled. |
| Use custom sound device | For advanced users: Passes the option to the GNU/Linux sound system. |

# KDE Control Center↔ Sound (Continued)

| Use custom sampling rate | Changes the sampling rate. The sampling rate is the amount of audio data passed to the soundcard during a period of time. Most soundcards work at a sampling rate of 44,100Hz (44,100 samples per second). Some soundcards work with a different sampling rate. |
| Other custom options | For advanced users: Refer to the project (www.audio-project.org) for information on options. |
| Sound quality | Most soundcards work with 16-bit audio (CD quality), some older soundcards can play only 8-bit audio (telephony quality). Autodetect usually picks the right quality. |
| Audio buffer size (response time) | Determines how quickly gets gets from a program to the sound. A larger buffer size (slider toward the right) is appropriate for casual listening and system sounds. |

**System Bell** By default KDE uses Notifications to alert you to important events. Notifications can be whatever you want: playing a sound, displaying a message box, and so on. Check System Bell instead of System notification to revert to the system beep method of notification. After you check this box, you can control the Volume, Pitch, and Duration of the system bell by using the sliders. See also "Bell" on page 328.

**System Notifications** Allows you to specify how and what you want to be notified when various events occur. Expand the tree menu to see the events. For each event, you can specify zero to four notification options: Log to file, Play sound, Show messagebox, and Standard error output. For the first two you specify a log file or sound file.

# System

Refer to “KDE Control Center: System Module” on page 988 in Chapter 17.

# Web Browsing

The Web Browsing section of the Control Center (Table 8-21) controls the use of cache, cookies, stylesheets, proxies, and the user agent and enhanced browsing over Konqueror-specific settings.

# KDE Control Center↔ Web Browsing

| Cache | Stores recently downloaded Web pages in memory for faster repeat access. This section defines cache (page 1459) policy and size. |
| Use Cache | Enables the rest of this tab. Causes the Konqueror Web browser to use cache |
