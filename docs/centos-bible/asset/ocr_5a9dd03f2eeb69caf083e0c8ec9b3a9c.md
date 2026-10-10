# Part II  Using CentOS

![](bbox=[0.17, 0.12, 0.75, 0.46])

Tracks that are muted appear with an `MM` at the bottom of the slider. When unmuted, `00` appears instead. If more tracks are available than can appear on the screen, the right arrow key enables you to scroll to the right to display additional track bars.

If two channels are available on a track, you can adjust them individually. With the track selected, use the **q**, **w**, and **e** keys to adjust the left, both, and right channels up, respectively. Use **z**, **x**, and **c** to adjust those same channels down, respectively. When you are done using `alsamixer`, press the [Esc] key to exit.

Here are a few general rules for adjusting your audio channels:

+   - To avoid unwanted noise on playback or record, mute any tracks you are not using.
+   - An icon representing your GNOME Volume Control utility should appear on your desktop panel. The single slider associated with that icon may be set to adjust your master volume or headphone port output. Right-click on that icon and select **Preferences** to change to a different port.
+   - To test that your audio channels are working, use the `speaker-test` command. For example, `speaker-test -c 4` will send a tone to each of four speakers in turn (front left, front right, rear left, and rear right) to check that each is working. Note that the tone output may surprise you with its loudness.

> **TIP**  If you have more than one sound card, each sound card is identified by a number, with zero identifying the first sound card. For example, to start `alsamixer` for your second sound card, type `alsamixer -c 1`.