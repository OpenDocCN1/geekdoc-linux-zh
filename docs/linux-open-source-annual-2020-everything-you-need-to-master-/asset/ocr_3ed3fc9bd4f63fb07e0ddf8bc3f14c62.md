![](bbox=[0.08, 0.11, 0.43, 0.26])

> Hardened veterans are likely to appreciate Ardour's improved bus design compared to earlier versions.

advanced options like track alignment and automation. However, to make further mixing adjustments like changing Pan, you'll need to open the mixer, the button for which is in the top-right corner.

Exporting audio is fairly straightforward in Audacity 5.x. From the main menu choose Session > Export > Export to Audio File(s). It's best to leave these options alone if you don't know what you're doing: with the defaults it should save your work as a snapshot of the entire session. A warning: *Ardour* crashed the first time we tried to export, so click Save first!

*Ardour* has been around for 14 years now and is synonymous with Linux audio – there is even a modified proprietary variant, *Harrison Mixbus*, for serious audiophiles who want a big name behind their software. Nevertheless, it has always suffered from something of an awkward interface. Now it seems the tables have turned, and rival projects will need to up their game.

![](bbox=[0.08, 0.55, 0.16, 0.59])

# Qtractor
http://qtractor.org

Although Qtractor has evolved into a fully fledged DAW, it was originally meant to be just a MIDI sequencer with some DAW features. Qtractor's strange evolution has resulted in an endearing hodgepodge of all the major editors, with bits

of Rosegarden, Ardour, old Pro Tools, and chunks of Cakewalk and Cubase for good measure. The last time we used Qtractor it was prone to crashing, but developer Rui Nuno Capela has put a lot of time into fixing bugs.

Unfortunately, starting a project involves running through a series of prompts that may be intimidating and somewhat confusing (much like the bad old days of Ardour!). However, once you're up and running, Qtractor has some killer editing features.

Rather than deleting chunks of audio, you can grab the edge of either end of a track and just drag it inwards. Rather brilliantly, you can also drag it back to 'uncrop' as it were, even past the start of recently pasted bits of audio. Interestingly, if you hold Ctrl when you click and drag a clip's border, Qtractor will generate more of the same audio based on what's snap before it. If you have your BPM set correctly the Snap feature can break down your music into perfect Bar-length chunks, which can be dragged around at will. And don't worry if your wave spills over the edge of what you've grabbed, as you can always 'uncrop' it.

If you're into MIDI, Qtractor has a similar piano roll editor to LMMAS: double-click on a piece of recorded MIDI to open it. If you use a synth plug-in when adding the MIDI track, you can avoid involving JACK. Caif Fluidsynth is particularly popular and can load new soundfonts, though Youshimi if you can't be bothered!

Exporting audio was very confusing last time we covered Qtractor, but it seems to have a reasonable GUI flow now. To export the session as a whole, choose Track > Export tracks > Audio, and follow your nose. If you choose Master as your output, it will export everything into a wave file, regardless of whether it's audio or MIDI.

Compared to Ardour nowadays, Qtractor's cluttered interface is quite confusing. But if you can get into a flow, and understand the Qtractor way of doing things, the combination of wave audio and MIDI may be all you ever need to make music. 💻

![](bbox=[0.08, 0.66, 0.92, 0.95])

> Qtractor's interface may be messier than Ardour's, but the MIDI functions are more powerful and the clip editing is utter genius.

Image credit: Andrew Flitzsymon