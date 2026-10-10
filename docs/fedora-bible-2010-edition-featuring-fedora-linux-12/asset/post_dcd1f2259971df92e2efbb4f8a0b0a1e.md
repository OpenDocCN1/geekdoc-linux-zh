
```
$ echo "Hello There" > /dev/pts/0
```

The words Hello There appear in that Terminal window. You can try sending messages among several Terminal windows. If a user who is logged on to the computer has terminal permissions open, you can send messages to him or her in this way, too. (I knew people who would send a dictionary file to an unsuspecting user's terminal. Although it wasn't destructive, it was annoying if you were trying to get work done.)

To get information from the ALSA service about your sound cards, list the contents of the following files (for example, `cat /proc/asound/devices`):

- `/proc/asound/devices` — Contains available capture, playback, and other devices associated with your sound system.
- `/proc/asound/cards` — Contains the names, model numbers, and IRQs of your sound cards.

For general information about sound in Linux, see the Sound-HOWTO (for tips about sound cards and general sound issues) and the Sound-Playing-HOWTO (for tips on software for playing different types of audio files). You can also refer to the Linux Audio Users Guide (http://lau.linuxaudio.org).

> **NOTE:** You can find Linux HOWTOs at http://www.tldp.org.

## Detecting your sound card driver

During the first startup after you install Fedora, the Firstboot setup agent tries to detect and configure your sound card. If that process was not successful, the Fedora Project recommends you file a bug report. Unlike previous releases, sound card detection should "just work" in current releases.

You can adjust sound settings and see what sound cards were detected from the Sound Preferences window. From the System menu, select Preferences ➔ Sound Preferences. Then choose the Hardware tab. Figure 7-1 shows an example of the Sound Preferences window.

> **TIP:** Audio may be muted when you first install Fedora. If you are not able to hear the test of your sound card, use Sound Preferences or alsamixer (as described later in this chapter) to unmute and adjust the volume on your audio input.

At this point, you can check the audio hardware that was detected, adjust input and output volume, and see sliders on (the Applications tab) for audio applications that are running.

Try playing an audio file. Insert a CD and open one of the CD players described in the following section. If you don't hear any sound, but the utility seems to have detected your sound card, refer to the next section and try adjusting your audio levels. If that doesn't work, try some of the debugging procedures suggested in the ALSA Wiki (http://alsa.opensrc.org/).

![](img/c78bdcb5b7842a0d73dcc98921f872a2_283_0.png)

**Figure 7-1:** The Sound Preferences window lets you check and adjust audio settings.

> **TIP:** If there is a data CD in your CD drive, you may not be able to simply eject it to play your music CD. To eject a data CD, close any windows that may have an open file from the CD, and then unmount the CD in your drive (if one is mounted) by typing `umount /media/cdrecorder` as root user from a Terminal window (the mount point name may be something other than `cdrecorder`). Then you can eject the old CD and place an audio CD in the drive. If the CD appears as an icon on the desktop, you can right-click the CD icon and select Eject to eject the disc.

## Adjusting sound levels

Every audio output (Playback) and input (Capture) device associated with your sound cards can be adjusted or muted using one of several different tools that come with Fedora. From the Sound Preferences window described earlier, select the Applications tab to adjust sound levels for individual applications. Figure 7-2 shows the Applications tab.

A separate menu choice available with the applet allows you to quickly mute the sound. In addition, if you simply click on the applet, GNOME presents a volume slider to make it easy to adjust the current volume—the most likely operation when it comes to sound.

The alsamixer utility is an ncurses application, which means that it is viewed graphically from a shell. It can be used to manage sound levels for more than one sound card on a computer, each with multiple devices representing it. Type **alsamixer** from a Terminal window to start it in playback mode (to adjust audio output) or **alsamixer -V capture** (to select an audio capture device and adjust audio capture level).

![](img/c78bdcb5b7842a0d73dcc98921f872a2_284_0.png)

**Figure 7-2**: The Sound Preferences window allows you to control audio input and output.

Here are some ways to adjust your audio with alsamixer:

- Use the right and left arrow keys to move among the different sound tracks.
- Use the up and down arrow keys to adjust the levels of the current tracks.
- Press M to mute or unmute the current track (playback mode only).
- Press the spacebar to make the current track the capture device, for devices such as microphone or line-in that are appropriate for capturing audio. Then adjust the Capture bar to set the level at which audio is captured. (Note that this feature works in capture mode only: **alsamixer -V capture** or by pressing F4 in alsamixer.)

Tracks that are muted appear with an MM at the bottom of the slider. When unmuted and at the lowest volume level, 00 appears instead. If more tracks are available than can appear on the screen, the right arrow key enables you to scroll to the right to display additional track bars.

If two channels are available on a track, you can adjust them individually. With the track selected, use the q, w, and e keys to adjust the left, both, and right channels up, respectively. Use z, x, and c to adjust those same channels down, respectively. When you are done using alsamixer, press the Esc key to exit.

Here are a few general rules for adjusting your audio channels:

- To avoid unwanted noise on playback or record, mute any tracks you are not using.
- An icon representing your Sound Preferences utility should appear on your desktop panel. The single slider associated with that icon may be set to adjust your master volume or headphone port output. Right-click that icon and select Preferences to change to a different port.
- To test that your audio channels are working, use the speaker-test command. For example, speaker-test -c4 will send a tune to each of four speakers in turn (front left, front right, rear left, and rear right) to check that each is working. Note that the tone output may surprise you with its loudness.

> By default alsamixer will try to use the an emulated device provided by PulseAudio and will likely have only one or two mixers to control. If you want to control the underlying real ALSA device and all of its associated controls, press F6 in alsamixer to choose your sound card. If you have more than one sound card, each sound card is identified by a number, with zero identifying the first sound card. For example, to start alsamixer for your second sound card, type $ alsamixer -c 1.

## Setting your sound card to record

I added this section on setting your sound card to record because people often miss this step. You may run a communications application (such as Ekiga) and wonder why nothing records. The reason is that you need to identify the capture device to use before you record and make sure its level is set high enough to work.

The easiest way to set the channel to use for audio capture is to use the Sound Preferences window described earlier. Click the Input tab and choose the device that controls your computer microphone (or other input device). Then make sure that all audio devices are muted except the one you want to record from. Available devices might include microphone, line-in, and CD. A red ✗ through a microphone icon beneath each capture device indicates that it is muted.

Move the slider for your capture device up to an appropriate level. Then connect your microphone or input device (to line in) and start the application you want to record from.

> Audiacity is a nice application for recording and working with recorded sound in Fedora. You can install the audiacity package from the Fedora repository (type yum install audiacity).

## Choosing audio players

There are audio players in Fedora for playing music and sound files in a variety of formats. Without adding any software, you can play commercial music CDs and Ogg Vorbis audio
