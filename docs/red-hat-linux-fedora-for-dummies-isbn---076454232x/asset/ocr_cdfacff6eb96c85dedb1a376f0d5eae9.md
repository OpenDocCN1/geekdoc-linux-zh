# 158 Part III: Linux, Huh! What Is It Good For? Absolutely Everything!

![](bbox=[0.13, 0.13, 0.55, 0.35])

Mozilla now launches XMMS whenever you click a link to an Ogg/Vorbis source. XMMS starts and connects and then plays the stream.

![](bbox=[0.12, 0.43, 0.22, 0.51])

XMMS uses the Enlightened Sound Daemon (esd) process by default to access your computer's speakers. Designed to allow multiple audio players to simultaneously use your computer's speakers, esd sometimes gets confused and you have to restart it. Log in as root, open a GNOME Terminal window, and run the command `killall -HUP esd`. If that doesn't work, you can configure XMMS to use another output system. Right-click the XMMS window and choose Options\ Preferences. Click the Output Plug-in subwindow and select the OSS Driver 1.2.7 plug-in. Click the Apply button and then the OK button.

# Using the Fabulous MPlayer

Whenever a desperate need exists, the Superman — err — the open source movement, comes in to save the day. Until recently, you couldn't use any single Linux application to listen to and view most popular streaming formats. Now, MPlayer has burst on the scene and fills that gap.

MPlayer can play most popular (and many obscure) audio and video streaming formats. Although it's under intense development, it's still technically in the beta development phase. However, MPlayer is quite usable, and we think that you should consider using it. We do!

This list shows some streaming formats MPlayer can play: