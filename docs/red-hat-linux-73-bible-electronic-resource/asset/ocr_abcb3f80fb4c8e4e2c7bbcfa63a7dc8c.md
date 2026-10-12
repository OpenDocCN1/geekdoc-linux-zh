+   3. In this example, sndconfig detects an Ensoniq 1371 sound card. Press Enter to select OK.
+   4. A message warns you that you are replacing the old /etc/conf.modules file. Press Enter to select OK.
+   5. A message tells you that a sound sample will play to check if the card is configured properly. Press Enter to select OK.
+   6. You are asked if you heard the sound.
+   7. If you hear the sound, select Yes and skip to Step 12. Otherwise select No to continue.
+   8. You are asked to manually configure your sound card. Press Enter to select OK.
+   9. A list of sound cards is displayed. Select your card and press Enter to select OK.
+   10. Select OK to try the sound card again.
+   11. You are asked again if you were able to hear the sample. If you hear the sound, select Yes to continue. Otherwise select No to try a different card.
+   12. You are warned that a new /etc/modules.conf file is being created (and the old one is being backed up). Press Enter to select OK.

At this point, you can try playing some audio. Insert a CD and open one of the CD players described in later sections (such as the gtcd or cdp players).

> **TIP:** When I configured my sound card, the default sound level was a bit low for my taste. I inserted a music CD to have something to listen to. Then I ran the **`amix`** command to adjust the volume levels. Volume (Vol) should be highlighted when **`amix`** opens. You can use the right and left arrows to adjust volume levels. Use the up and down arrows to choose particular sound devices: speaker, line, mic, CD, and so on. With a device highlighted, use the Tab key to be able to adjust balance for the device. Type **s** to save the changes and **q** when you are done. The amux utility will show you all the audio devices it can find; if you don't see the CD, microphone, or speaker, for example, they probably weren't properly detected and configured.

# Performing audio-file conversion

If you have a sound file in one format, but you want it to be in another format, Linux offers some conversion tools you can use to convert the file. The Sox utility can translate to and from any of the audio formats listed in Table 8-1.

> **TIP:** It may be that not all audio types are compiled into your version of Sox. Type **`sox -h`** to see the supported audio types. This also shows the options and effects that Sox supports.