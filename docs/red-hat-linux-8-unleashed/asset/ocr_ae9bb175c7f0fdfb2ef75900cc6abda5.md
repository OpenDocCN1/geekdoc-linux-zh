# FIGURE 4.5 The sndconfig command can be used to configure a new sound card.

NOTE\If your sound configuration works and you have installed multimedia support for Red Hat, you can rock out by listening to Brent Fox's Red Hat Linux Credits Theme song using the ogg123 sound player like this:

```
# ogg123 /usr/share/redhat-credits.ogg
```

See Chapter 26, "Multimedia Applications," for more information about enjoying music and video with Red Hat.

Red Hat also includes a graphical sound client used during an X session to configure sound. Start the `redhat-config-soundcard client by clicking your desktop panel System Soundcard Detection menu or item, or by using the command at a terminal window like so:

```
$ redhat-config-soundcard &
```

After you press Enter, you will be prompted for the root password. Enter the password and click OK. The `redhat-config-soundcard` will try to automatically detect and configure your soundcard. You'll then see a dialog you can use to test your soundcard settings, as shown in Figure 4.6. Click on the Play test sound button to listen to a sample sound.