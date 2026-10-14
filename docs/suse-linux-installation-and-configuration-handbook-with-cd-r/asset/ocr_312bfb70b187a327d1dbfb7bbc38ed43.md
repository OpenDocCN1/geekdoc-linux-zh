# Troubleshooting ALSA

ALSA is easy to troubleshoot. To correctly troubleshoot ALSA, you should use the source package and compile it using ./configure --with-debug=detect. Install the drivers and issue the following command in a terminal or another console:

```
#tail -s /var/log/messages
```

Continue the installation process and watch for the tail window/console. Check what type of errors you get and try to fix them.

ALSA cannot work if you have sound support built in the kernel. If you cannot load the ALSA modules, check your kernel configuration.

ALSA also cannot work if OSS is already loaded. Only one of them can be loaded at a time for the same card.

# Enlightenment Sound Daemon (ESD)

Enlightenment Sound Daemon (ESD) is not a sound card driver by itself. As the name indicates, ESD is a normal daemon. Why you need ESD is another story. As you might have noticed, the sound card supports only one wav file at a time. One amazing thing about Windows games is the ability to hear more than one voice at a time. This, in fact, is the gift of DirectX to Windows. Linux programmers don't like missing out on great features like this. So, they came up with ESD. ESD sits on top of the sound drivers and controls what's going in. Thus, for programs that use the ESD API, two programs can output sound (wav) at the same time.

Without getting in to technical details, ESD waits for programs that require sound output. It handles the streams sent to it and manages to mix them in one stream and output them to the sound card. In very simple terms, this is how ESD does it.

Remember though that you will only be able to play sounds through programs that were written to support ESD. The other programs written for OSS and ALSA, won't be able to work until ESD is terminated. When ESD is running, only ESD programs will play.

ESD is essential for Enlightenment if you want to hear sound. Sound in Enlightenment will not work if ESD is not running.

The following are some programs that use ESD:

+   - Enlightenment
+   - X Multimedia System (xmms), which has an ESD plug-in
+   - mpg123
+   - E-music
+   - ALSA player