# SOX

sox [option] input file output file [effect]
Translates sampled sounds from the input format specified by input file to another format, stored in output file, with the optional effect. This command is most often used in shell scripts or as a filter between two other commands. To play sampled sounds, use play. To play MP3s, use mpg123. To play MIDI files, use playmidi.

# OPTIONS

| Use This Option | To Do This |
|---|---|
| -a | Set the data format type to ADPCM. |
| -A | Set the data format type to Alaw (logarithmic). |
| -b | Use bytes to describe the size of the sample. |
| -c n, --channels=n | Define the number (n) of channels of the file. |
| -d | Use 64-bit, double-floating point notation to describe the size of the sample. |
| -D | Use 80-bit, IEEE-floating point notation to describe the size of the sample. |
| -f | Use 32-bit floating point notation to describe the size of the sample. |
| -f format, --format=format | Specify the bit format of the sample. The available options are<br>a ADPCM.<br>A Alaw (logarithmic).<br>g GSM.<br>s Signed linear (2's complement).<br>U Ulaw (logarithmic).<br>u Unsigned linear. |
| =g | Set the data format type to GSM. |
| -h, --help | Show the available options. |
| -I | Use 32-bit words to describe the size of the sample. |
| -P | Run in preview mode. |