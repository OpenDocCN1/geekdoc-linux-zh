# OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| -t type, --type=type | **smp** Turtle Beach SampleVision sound. |
| | **sna** Sun/NeXT AU sound file. |
| | **txw** Yamaha TX-16W sampler. |
| | **ub** Unsigned byte RAW sound file. |
| | **ul** ULaw RAW sound file. |
| | **uw** Unsigned word sound file. |
| | **vms** Compressed speech file. |
| | **voc** Sound Blaster VOC sound. |
| | **wav** Microsoft WAV sound. |
| -v volume, --volume=volume | Change the audio output to the specified volume (less than 1.0 decreases, more than 1.0 increases). |
| --version | Show version of play/rec. |
| -X, --xinu | Reverse the byte order of the sample. |

# EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `play mysound.wav` | Plays the specified sound file (mysound.wav). |
| `play mysound.wav echo 40 12` | Plays the specified sound file (mysound.wav) with an echo effect (40-millisecond delay and 12-millisecond decay). |

# playmidi

```
`playmidi [ option ] [ filename ]`
```

Plays the MIDI file specified by filename. Available options enable you to play or suppress specified MIDI channels (see the MIDI Channels table in this section). To play WAV, AU, and other wave-table sounds, see play. To play MP3s, see mpg123.