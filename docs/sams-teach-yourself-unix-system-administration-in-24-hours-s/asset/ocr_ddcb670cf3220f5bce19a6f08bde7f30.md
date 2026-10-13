```
<!DOCTYPE kpartgui>
<kpartgui name="artscontrol" version="3">
<MenuBar>
<Menu name="view"&amp;View/text>
<Action name="view_fft_scope"/>
<Action name="view_audio_manager"/>
<Action name="view_arts_statusview"/>
<Action name="view_midi_manager"/>
<Action name="view_media_types"/>
<Action name="view_freverb"/>
<Action name="old_volume_display"/>
</Menu>
</MenuBar>
</kpartgui>
```

Notice the very useful shell shortcut !$, which matches the last word of the previous command.

Well, we haven't found any documentation, but we can glean a few snippets of information from this. First off, the arts application is some sort of synthesizer player or interface system (notice arts MIDI manager view.rc: MIDI is musical interface digital instrument, and it's how synthesizers talk to each other). Secondly, notice the rc file contents indicate that it's a kpartgui, which indicates that it's part of the GUI to KDE. Most likely, then, artsd is a background daemon that helps the arts synthesizer work properly.

+   4. Because all the arts* applications in /usr/bin seem to be part of this program, another sneaky trick is to use the helpful strings command to search for any sort of URL that might be listed in any of the programs:

```
# cd /usr/bin
# strings arts* | grep -i http:
http://www.arts-project.org/
```

Gotcha! A quick visit to that Web site reveals that sure enough, arts is an analog real-time synthesizer. And now we know.

There are a number of different ways that you can try to isolate and identify different programs running in a ps output. It's good practice learning the various sysadmin tools, so try doing a bit of your own detective work, and see if you can identify some of the more cryptic daemons running on your own Unix system.