+   *   **WAV Audio** — Supports these WAV audio codecs: PCM, uLaw, MSADPCM, Intel DVI, and GSM. Any animation that doesn’t already have audio can add a WAV audio and be played with Xanim.
+   *   **AU Audio** — Any animation that doesn’t already have audio can add an AU audio and be played with Xanim.

> TIP: To play an audio file along with a video clip, type `xanim vidfile audfile`, where `vidfile` is the name of a video clip or animation and `audfile` is the name of a WAV or AU audio file. The two files begin playing together.

To start Xanim, type the following command from a Terminal window on your desktop:

```
$ xanim file
```

where *file* is the name of a video, animation, or audio file in a supported format. Figure 8-8 shows the Xanim viewer. The image on the right is an AVI file being played. On the left are the controls.

![](bbox=[0.1, 0.41, 0.54, 0.59])

Figure 8-8: Use controls to play and control video content with Xanim.

The controls are fairly straightforward. Controls along the top row (in the order they appear) let you go back one frame at a time, play backward, pause, play forward, and go forward one frame at a time, respectively. Plus and minus keys let you speed up and slow down play, respectively. The plus and minus speakers let you increase or decrease the sound volume.

You can also control Xanim play from the mouse or the keyboard. Move forward or backward a frame at a time using the right and left mouse buttons, respectively. Press the middle mouse button to start and stop the animation. From the keyboard, press the Spacebar to start and stop the animation. To quit Xanim, press Q.

Here are a few cool things to do with Xanim:

+   *   Try starting Xanim with the `+root` option. This causes the video or animation to be tiled on to the root X screen as it plays.