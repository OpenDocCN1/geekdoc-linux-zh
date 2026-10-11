# **NOTE**

If you set your recording level too low, you might be able to amplify the signal at playback by turning up the volume. This will also amplify background noise, however. If you set the recording level too high, the result is *clipping*—the digital recording stores a series of maximum or minimum values, which ends up producing a harsh, grating sound. In extreme cases, you might hear nothing but clicks in a severely clipped recording.

+   5. When you’ve adjusted your recording level to your satisfaction, begin recording in earnest, and stop whenever you’re done.

# **TIP**

Aside from turntables, the electrical requirements of most stereo equipment are standardized. You can therefore connect, say, a cassette recorder directly to your sound card’s line input if you want to record a cassette, without going through the stereo system.

# # Avoiding Ground Loops

One problem you might encounter when you connect your stereo and your Linux computer is that of a *ground loop*. Many electronic devices, including desktop computers, are *grounded* in one way or another. For instance, the third prong on a computer’s electric plug grounds the computer. The details of how a ground is achieved vary, but the result is the same: An electrical connection between the device and the ground—literally the earth outside your building. The ground serves as a safety feature; excess current can be dumped to ground when necessary. Surge protectors use this characteristic to protect the computer from power surges.

The problem arises when two or more *different grounds* are used by different components in an audio setup. When this happens, the result is a feedback loop that produces a 60Hz hum. (In North America, AC electrical supplies run at 60Hz. In Europe, it’s 50Hz, so a ground loop creates a 50Hz hum.) Possible specific causes of this problem include

+   - **Using different electrical outlets** Ideally, all the electrical outlets in a building are grounded at the same point. This isn’t always the case, however, particularly if a building’s electrical system has been expanded or modified over the years.
+   - **Improper electrical grounding** If the grounding of your electrical system wasn’t done correctly, you might get a ground loop because, in effect, a proper ground isn’t available.