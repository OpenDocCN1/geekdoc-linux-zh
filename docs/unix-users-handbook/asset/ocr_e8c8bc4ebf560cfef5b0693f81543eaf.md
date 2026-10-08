In order to start up a subsystem, you would simply edit the appropriate configuration file in /etc/rc.config.d. An example showing /etc/rc.config.d/audio is shown with the AUDIO_SERVER variable set to 1.

```
#                    ***********    File:        /etc/rc.config.d/audio
**************
# Audio server configuration.  See audio(5)
# AUDIO_SER:           Set to 1 to start audio server daemon
#

AUDIO_SERVER=1
```

This example results in the following message being shown at the time the system boots:

Start audio server daemon ............................[ OK ]

and this message at the time the system is shut down:

Stopping audio server daemon ..........................OK

I have mentioned run levels several times in this discussion. Both the startup and shutdown scripts described here, as well as the /etc/inittab file, depend on run levels. Run levels are different among UNIX variants. I have never seen all the same run-level definitions for different UNIX variants. In general, the lower run levels are used for lower-level functionality, and you initiate more advanced capabilities as the run levels increase. This generalization is not always true, so you want to check for the UNIX variant you are using. The following is a list of run levels and how they are used: