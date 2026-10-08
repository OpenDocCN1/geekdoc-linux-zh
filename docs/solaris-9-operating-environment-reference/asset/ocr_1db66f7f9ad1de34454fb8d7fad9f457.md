# mixerctl 861

mopoke% mixerctl -e
Audio mixer for /dev/audictl is enabled

mopoke%

The following example prints information for the audio device.

```
mopoke% mixerctl -i
Device /dev/audictl:
Name = SUNW, audiots
Version = a
Config = onboardi
```

Audio mixer for /dev/audictl is enabled

mopoke%

The following example prints the audio_info_t structure for the device along with
the device type information. This option implies the -i option.

```
mopoke% mixerctl -v
Device /dev/audictl:
Name = SUNW, audiots
Version = a
Config = onboardi
```

Audio mixer for /dev/audictl is enabled
Sample Rate

```
Play 48000
Record 48000
Channels 2
Play 2
Record 2
Precision 16
Play 16
Record 16
```

```
Encoding 3 (linear)
Record 3 (linear)
Gain 191
Record 127
Balance 32
Play 32
Record 32
```

```
Port 0x00000003 (SPKR|HDPHONE)
Record 0x00000001 (MIC)
Avail Ports 0x00000007 (SPKR|LINE)
Play 0x00000043 (MIC|LINE|CODEC LOOPBACK)
Record 0x00000005 (SPKR|LINE)
Play 0x00000043 (MIC|LINE|CODEC LOOPBACK)
```