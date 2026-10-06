# KDE Control Center⇔ Sound (Continued)

| | |
|---||
| Start soundserver on KDE startup | Starts arts soundserver when KDE starts up. You may still be to hear system sounds when the arts soundserver is not running because a separate sound program is used as a fallback. KDE-based multimedia applications, such as noatun, require the arts to be running. |
| Enable network transparency | For advanced users: Allows arts to enable one computer to send audio over the network and have it played on another. |
| Exchange security and reference over the X11 server | For advanced users: Enables a secure method of communication between arts soundservers. |
| Run soundserver with realtime priority | Refer to "Sound" on page 346. |
| Autosuspend if idle for n seconds | Allows non-arts-enabled programs to use the sound device when arts is idle. Also, cause arts CPU time even if it not playing sounds, you may find that your system is more responsive if you allow arts to suspend itself when it is idle when you are using arts to play only system sounds. |
| Display messages using | Specifies how arts should communicate to you: for example, when it cannot find the soundcard. There is usually no reason to change the default. |
| Message Display | Specifies which messages you want to see. |
| Sound I/O method | The arts soundserver can output audio, using various methods. Methods are depends on packages which are installed on your system. The usual method is by using the OSS (Open Sound System), which is the standard GNU/Linux audio output system, and is automatically detected (Autodetect). Change this option only if you understand what other output methods are. |
| Enable full duplex operation | Enables simultaneous recording and playing of audio. Usually, arts configures a card to allow only input or output but not both at the same time. Some soundcards do not work properly with full duplex enabled. |
| Use custom sound device | For advanced users: Passes the option to the GNU/Linux sound system.