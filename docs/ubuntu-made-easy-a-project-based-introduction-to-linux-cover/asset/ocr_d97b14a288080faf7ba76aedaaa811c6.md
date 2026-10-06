the order of the day when it comes to sound problems, I'm afraid, although I've tried to explain as many of the relevant options as possible in this section to help you out.

If the problem has more to do with what you're not seeing when you're not hearing, you're possibly in an easier ride. Video problems tend to be easier to fix—most of the time, all you'll need to find the right piece of software to install and then, erm. Skip to the end of the section for video issues.

# Ubuntu Doesn't Play Any Sounds

There are many reasons why Ubuntu might not be playing sounds. I'll concentrate on some of the more basic issues in this section, but if none of this helps, you can always try the Ubuntu forums or IRC; both are discussed in Chapter 21 troubleshooting.

To start troubleshooting, find a song on your computer and play it in Rhythmbox or the Totem Player. If you need it, a sample called "Josh Woodward - Swansong" is available in the /usr/share/example-content/Ubuntu_Free_Culture_Showcase folder.) You need to have a sound file playing constantly in the background so that you can tell changing any of these settings worked.

If you are unable to start playing the file, Ubuntu may not have detected your sound card. Open a Terminal using the Dash, type apply -1 into it, and press ENTER. If the list of playback devices is empty, your sound card hasn't been detected. In this case, you'll definitely need to get some community support—again, see Chapter 21 for more information using the Ubuntu forums and IRC.

Assuming you can play the file, check that your speakers are turned, turned up, and plugged into the correct socket (it's a light green color). Many times in the past, I've plugged my speakers into the microphone socket and sat there wondering why they were silent. You're confident that your speakers are okay, try the following steps:

+   1. Click the speaker icon on the top panel and select Sound Settings from the menu that pops up. The Sound window will appear (Figure 22-7).
2. Make sure that the Mute option is not checked and that the Output slider at the bottom of the window is pulled all the way to the right.
3. Click the Applications tab and make sure that none of the applications in the list are muted or set to a low volume.
4. Click the Output tab and make sure that the right connector is chosen. If you're not sure, trying different connectors by trial and error until you get one that works. If none of them work, return this option to your initial setting (usually Speakers—Built-in Audio).

If none of this helped, check out https://wiki.ubuntu.com/Audio/ or https://wiki.ubuntu.com/DebuggingSoundProblems/. The latter is a brief guide to identifying sound problems, which requires a little work in the Terminal.