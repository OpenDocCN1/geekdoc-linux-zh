+   - **Weak** The number of packets which appear to have weak IV's. This column counts the number of packets with weak IV's. Not a problem commonly seen nowadays, but excessive weak packets could be an indication of problems or an attack.

```
# Does the GUI use sound?
# NOT to be confused with "sound" option later, which is for the SERVER to make
# noise on whatever host it's running on.
sound=true
```

The sound option enables the client (as opposed to the server) sound options. The client can make noises and play sounds on various events (new network, and so forth). This can be very useful for systems where you can't keep your eye on the system (like in a moving car).

It's best to use either the server sound or the client sound, but not both at the same time or it will be awfully confusing and noisy.

```
# Path to sound player
soundplay=/usr/bin/play
```

If the client is to play sound, it obviously needs to know what program on your system it should use to play them. By default it's /usr/bin/play, but adjust to your system's specific sound player.

```
# Optional parameters to pass to the player
# soundopts=--volume=.3
```

If you want to get fancy, you can also pass parameters such as sound volume or any other command-line parameters for your player program. Simple specify them as you would on the command line.

```
# New network found
sound_new=@sharedatadir@/kismet/wav/new_network.wav
# Weppd new netwrok
# sound_new_wep=@sharedatadir@/kismet/wav/new_wep_network.wav
# Network traffic sound
sound_traffic=@sharedatadir@/kismet/wav/traffic.wav
# Network junk traffic found
sound_junktraffic=@sharedatadir@/kismet/wav/junk_traffic.wav
# GPS lock acqired sound
# sound_gpslock=@sharedatadir@/kismet/wav/foo.wav
```