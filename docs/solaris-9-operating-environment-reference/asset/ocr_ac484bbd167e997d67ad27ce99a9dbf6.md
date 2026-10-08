# 80

# audioconvert

voice
Equivalent to
encoding=ulaw,rate=8k,channels=mono.

cd
Equivalent to
encoding=linear16,rate=44.1k,channels=
stereo

dat
Equivalent to
encoding=linear16,rate=48k,channels=
stereo.

format
Specify the audio file format. Valid formats are:

sun
Sun-compatible file format (the default).

raw
Read or write raw audio data with no audio header or
in conjunction with an offset to import a foreign audio
file format.

offset
(-i only) Specify a byte offset to locate the start of the
audio data. You can use this to import audio
data that contains an unrecognized convert header.

# Usage

See largefile(5) for the description of the behavior of audioconvert when
encountering files greater than or equal to 2 Gbytes (2**31 bytes).

# Examples

The following example records voice data and compresses before storing it in a file.

```
castle% audiorecord -f g721 > mydata.au
```

The following example uses the file command to verify that the mydata.au file was
converted.

```
castle% file mydata.au
mydata.au: audio data: compressed (4-bit G.721 ADPCM), mono, 8000 Hz
castle%
```

The following example concatenates two Sun format audio files, regardless of the
data format, and outputs an 8-bit u-law, 16 kHz, mono file.

```
castle% audioconvert -f u-law,rate=16k,mono -o outfile.au infile1 infile2
```

The following example uses the file command to verify that the output.au file was
converted.

```
castle% file output.au
outfile.au: audio data: 8-bit u-law, mono, 16000 Hz
castle%
```

The following example converts a directory containing raw voice data files, in place,
to Sun format and adds a file header to each file.

```
castle% audioconvert -p -i voice -f sun *.au
```