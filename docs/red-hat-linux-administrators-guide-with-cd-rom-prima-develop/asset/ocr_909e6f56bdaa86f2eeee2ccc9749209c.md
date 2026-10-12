# SOUNDING OFF ON LINUX



```
```
GENRE live
URL http://icecast.ksl.com/
PUBLIC 1
X_AUDIOLCAST_LOGIN
# ICY_LOGIN

PASSWORD my_secret_password
SAMPLE_RATE 24000

MONO

# uncomment this line if you want to listen to a playlist
# NO_SOUNDCARD

# uncomment this line if you want to listen to streams
SOUNDCARD
HALF_DUPLEX
# USE_LAME3 lame
USE_MP3ENC /usr/local/gnu/mp3enc31/mp3enc31
SOUND_DEVICE /dev/dsp
MOUNTPOINT live
BITRATE 24000
VBR_QUALITY 1

# uncomment this line if you want to listen to a playlist
# MIXER

# uncomment this line if you want to listen to streams
NO_MIXER

#PLAYLIST playlist
DECODER_COMMAND mpg123
# MIX_CONTROL_MANUAL
# CONTROL_FILE mix_command
# TRACK_LOGFILE track.log

# VERBOSE 10
```
```

Several items in this listing have been commented out either because their features have not yet been implemented or because they are not required on this particular server.

To create a playlist so that you can operate your system as a jukebox and send streaming MP3 static files located on your hard drive over the Internet, you will want to reverse the SOUNDCARD and MIXER features, which currently have double comments in front of them. To operate as a jukebox, remove the pound signs from in front of the MIXER and NO_SOUNDCARD features.