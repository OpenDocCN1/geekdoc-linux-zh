Adding new TV channels requires the addition of disparate settings, since the TV configuration for the guide and control is unified into a single set of arrays held in `$MINBASE/conf/tvconf.conf`.

```
```bash
#!/bin/bash

tuner=( a1 a1 d1 d1 a1 d1 a1 a1 d1 )
channel=( 55 0 0 65 0 0 59 0 )
names=( BBC1 BBC2 BBC3 BBC4 "Channel 4" "Film Four" Five ITV TMF )
stations=( bbc1 bbc2 bbc3 bbc4 ch4 film_four five itv tmf )
```
```

As you can see, this holds the tuning information for the TV card (the channel number and whether it uses the analog or digital tuners⁵), along with the station ID and its full, printable name. The only restriction on the station ID is that it must match the one being used to retrieve the TV guide data. In this case, this is discernible from the list at http://bleb.org/services/tv/data/listings/0.

These data arrays are supplemented by the web-only data for the station icons, held in `$MINBASE/media/images/tvguide`. The filename stubs must match the IDs given earlier and end in `.png` to be correctly read by the applet. Furthermore, since these icons must be available to the web server, it is necessary to ensure a symlink exists from a web-friendly directory (such as `warp/conf/tvguide/images`) back to the original folder. By default, this is created by the Minerva installer, so you needn’t worry.

The final media applets covered here support streaming video and come in a pair. The first is the VLC streaming applet that allows you to browse a series of predetermined folders (such as `/net/media/videos`) and select one for playback. This creates a media stream on the server and port specified in `$MINBASE/conf/videostream.conf`, which can then be read by a VLC client on any connected computer. The other half of the pair is a client applet that is able, by using a plug-in (available for Firefox when you install VLC), to stream the video clip into the browser window itself.

> **Note** The streaming generally occurs over the local network only. To make it accessible from the outside, you need to open a port on your firewall or router to redirect traffic on the VLC port (8080, by default) to the given machine.

# Lifestyle

These applets are generally for use in and around the house and include an X10 control panel for switching your appliances on and off in a visual manner, as shown in Figure 7-5.

⁵ Analogue TV transmissions are all but extinct in the United Kingdom, and other countries, so this functionality will soon follow suit.