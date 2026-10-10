To get started with learning about NTP and xntpd, look under the /usr/doc/xntpd directory and use the text-only lynx Web browser like this:

```
$ lynx /usr/doc/xntpd*/index.html
```

Don't have access to a network? You can use a telephone to hear the latest time by calling the U.S. Naval Observatory's Master Clock Voice Announcer at (202) 762-1401 or (0202) 762-1069. You can also call long-distance (and not have to worry about satellite delays) by dialing 900-410-TIME; however, there is a charge of $.50 (U.S.) for the first minute and $.45 (U.S.) for each additional minute.

# ## Useful Clients

Mobile Linux users are enamored with clients that provide lots of information in small packages; they save screen real estate and reduce desktop clutter. KDE users know that the date and time are displayed by default in the lower-right corner of the desktop's panel. If you cannot see the date and time, your screen resolution is too small, and you should reconfigure the panel to its “tiny” setting (use the Configure menu item on the panel).

Linux also comes with many different clock and calendar clients. You can quickly craft your own pop-up current monthly calendar by combining the output of the text-based `cal` command with the `xmessage` X11 client like this:

```
$ cal | xmessage -geometry +1-0 -file - -title "Calendar"&
$ cal | xmessage -geometry +1+0 -file - -title "Calendar"&
$ cal | xmessage -geometry -1+0 -file - -title "Calendar"&
$ cal | xmessage -geometry -1-0 -file - -title "Calendar"&
```

These command lines produce a small monthly calendar in the lower-left, upper-left, upper-right, or lower-right corner of your desktop no matter what the screen resolution, as shown in Figure 16.4.

If you're traveling and you need to make sure you don't wake up someone halfway across the world, try KDE's `kworldwatch` client. This client may be launched from KDE's Utilities menu or from the command line of an X11 terminal like this:

```
$ kworldwatch &
```

After you press Enter, you'll see the window shown in Figure 16.5. It displays the local time, UTC time, time zone times, and a Mercator projection of the earth, showing the demarcation of sunrise and sunset.