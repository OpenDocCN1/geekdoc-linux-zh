# Chapter 8 KDE Desktop Environment

To specify the Sawfish window manager, work as root to change the preceding line to kwrapper ksmyserver --restore --windowmanager sawfish || \

When you start KDE, it automatically starts the programs in the global autostart directory (SKEDIR/share/autostart, where the value of SKEDIR defaults to /usr when the variable is not set) and then the ones in your Autostart directory (SKEDIR-HOME/Autostart). Although KDE can use its session management capability (page 185) to restart KDE-compliant and running programs when you close KDE and bring them up again when you restart KDE, you must place non-compliant programs in your Autostart directory to have them restart automatically. Drag and copy or link noncompliant programs you want to start automatically into the Autostart directory.

# Autostart

# Reporting a Bug

Select K menu: Extras⇒Bug Report Tool to open the Bug Buddy window which facilitates sending a bug report to the KDE group. Follow the instructions in the window to submit a bug report.

# Sound

Sound is controlled by K menu: Control Center⇒Sound. By default KDE runs the aRT (analog real-time synthesizer, www.arts-project.org) sound server in the background. Without a sound server, a program that needs to play a sound asks the system for control of the sound device (the soundcard) before continuing. The aRT provides above the sound device a layer that allows programs to output sound without waiting for the device to become available. The aRT mixes sounds. If you are playing music (with, for example, noatum, a media player for KDE) and another application plays a sound, aRTs this sound alongside the music without interrupting it.

The aRT server is a professional soundserver; it provides the advanced features required by professional music composition software. Because GNU/Linux was not designed with professional (real-time) multimedia in mind, you have to choose between (1) highest-quality sound that uses many system resources and CPU cycles and (2) lower-quality sound for casual listening that uses fewer resources and CPU cycles. For improved performance, when you select K menu: Control Center⇒Sound⇒Run soundserver with realtime priority, you may want to investigate the Linux kernel low-latency patch (people.redhat.com/mingo/lowlatency-patches).