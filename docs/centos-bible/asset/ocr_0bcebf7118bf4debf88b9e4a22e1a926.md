adjust volume levels together or separately. A Mute button lets you mute or unmute sound for each device.

# **FIGURE 7-2**

The Volume Control window provides simple, intuitive controls for setting audio levels.

![](bbox=[0.08, 0.27, 0.35, 0.44])

An alternative is to use the utilities that come with the als a-utils package in CentOS. In particular, that package contains the a l s a m i x e r utility, which lets you adjust or mute the various sound tracks. It also lets you select the device from which you can record or otherwise capture audio input.

The a l s a m i x e r utility is an ncurses application, which means that it is viewed graphically from a shell. It can be used to manage sound levels for more than one sound card on a computer, each with multiple devices representing it. Type a l s a m i x e r from a Terminal window to start it in Playback mode (to adjust audio output) or a l s a m i x e r - V capture (to select an audio capture device and adjust audio capture level).

Figure 7-3 shows an example of the a l s a m i x e r .

Here are some ways to adjust your audio with a l s a m i x e r:

+   - Use the right and left arrow keys to move among the different sound tracks.
+   - Use the up and down arrow keys to adjust the levels of the current tracks.
+   - Press m to mute or unmute the current track (Playback mode only).
+   - Press the spacebar to make the current track the capture device, for devices such as microphone or line-in that are appropriate for capturing audio. Then adjust the Capture bar to set the level at which audio is captured. (Note that this feature works in Capture mode only: a l s a m i x e r - V c a p t u r e .)