playing different types of audio files). You can also refer to the Linux Audio Users Guide (http://l au.linuxaudio.org).

> **NOTE** You can find Linux HOWTOs at www.tldp.org.

# **Detecting Your Sound Card Driver**

During the first startup after you install CentOS, the Firstboot set-up agent tries to detect and configure your sound card. If that process was not successful, it is recommended you file a bug report. You can adjust sound settings with the Sound choice under the Preferences menu.

> **TIP** Audio may be muted when you first install CentOS. If you are not able to hear the test of your sound card, use Volume Control or `alsamixer` (as described later in this chapter) to unmute and adjust the volume on your audio input.

To open the Audio Configuration window, run the `system-config-soundcard` command. If your sound card was detected, the Audio Configuration window should appear, as shown in Figure 7-1. Click on the Play button to the left of the slider, and you should hear a test sound. You can move the slider to the right to make sure the volume is set high enough to hear it.

# FIGURE 7-1

The Audio Configuration window detects your sound card.

![](bbox=[0.11, 0.57, 0.7, 0.9])