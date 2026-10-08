
# audioconvert 79

# Operands

file Concatenate and convert the named audio files to the output format, and write them out. If you specify no file name or if you specify the special file-name dash (-), read audio data from the standard input.

# Format Specification

The syntax for the input and output format is a set of keyword=value pairs with no intervening white space.

keyword=value{keyword=value...}

- - rate If values are unambiguous, you can omit the preceding keyword. Specify the audio sampling rate per second. If a number is followed by the letter k, it is multiplied by 1000 (for example, 44.1k = 44100), commonly used sample rates are 8k, 16k, 32k, 44.1k, and 48k.
- channels Specify the number of interleaved channels as an integer. You can also use the words mono or stereo to specify one- or two-channel data.
- encoding Specify the digital audio data representation. Encodings determine precision implicitly (ulaw implies 8-bit precision) or explicitly as part of the name (for example, linear16). Valid encoding values are:
  - ulaw CCIT G.711 u-law encoding is an 8-bit format primarily used for telephone-quality speech.
  - alaw CCIT G.711 a-law encoding is an 8-bit format primarily used for telephone-quality speech in Europe.
  - linear8, linear16, linear32 Linear Pulse Code Modulation (PCM) encoding. The name identifies the number of bits of precision. linear16 is typically used for high-quality audio data.
  - pcm Same as linear16.
  - g721 CCIT G.721 compression format uses Adaptive Delta Pulse Code Modulation (ADPCM) with 4-bit precision. Its primary use is to compress u-voice data with a 2:1 compression ratio.
  - g723 CCIT G.723 compression format uses Adaptive Delta Pulse Code Modulation (ADPCM) with 3-bit precision. Its primary use is to compress u-voice data with an 8:3 compression ratio. The audio quality is similar to that of G.721 but may result in lower quality when used for speech data.

The following encoding values are also accepted as shorthand for the sample rate, channels, and encoding:

# 80

# audioconvert

voice
Equivalent to
encoding=ulaw,rate=8k,channels=mono.

cd
Equivalent to
encoding=linear16,rate=44.1k,channels=stereo

dat
Equivalent to
encoding=linear16,rate=48k,channels=stereo.

format
Specify the audio file format. Valid formats are:

sun
Sun-compatible file format (the default).

raw
Read or write raw audio data with no audio header or in conjunction with an offset to import a foreign audio file format.

offset
(-i only) Specify a byte offset to locate the start of the audio data. You can use this to import audio data that contains an unrecognized convert header.

# Usage

See largefile(5) for the description of the behavior of audioconvert when encountering files greater than or equal to 2 Gbytes (2**31 bytes).

# Examples

The following example records voice data and compresses before storing it in a file.

```
castle% audiorecord -f g721 > mydata.au
```

The following example uses the file command to verify that the mydata.au file was converted.

```
castle% file mydata.au
mydata.au: audio data: compressed (4-bit G.721 ADPCM), mono, 8000 Hz
castle%
```

The following example concatenates two Sun format audio files, regardless of the data format, and outputs an 8-bit u-law, 16 kHz, mono file.

```
castle% audioconvert -f u-law,rate=16k,mono -o outfile.au infile1 infile2
```

The following example uses the file command to verify that the output.au file was converted.

```
castle% file output.au
outfile.au: audio data: 8-bit u-law, mono, 16000 Hz
castle%
```

The following example converts a directory containing raw voice data files, in place, to Sun format and adds a file header to each file.

```
castle% audioconvert -p -i voice -f sun *.au
```

# audioplay 81

The following example uses the file command to verify that both the files in the directory were converted.

```
castle$ file *
mydata.au: audio data: 8-bit u-law, mono, 16000 Hz
outfile.au: audio data: 8-bit u-law, mono, 16000 Hz
castle$
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|--- |--- |
| Architecture | SPARC, IA |
| Availability | SUNmauda |
| Interface Stability | Evolving |

# See Also

audioplay(1), audiorecord(1), file(1), attributes(5), largefile(5)

# audioplay — Play Audio Files

# Synopsis

```
/usr/bin/audioplay [-iv] [-v vol] [-b bai] [-p speaker | line] [-d dev] [file...]
```

# Description

audioplay copies the named files (or standard input if you specify no file) to the audio device. If you do not specify a file, the volume, balance, and port settings are applied. The input must contain an audio file header. If you use the -i option and the device is busy, an error message is printed and exit. The audio data is automatically uncompressed before playing. Compressed ADPCM (G.721) is not supported by the audio device. Minor deviations in sampling frequency (that is, less than 8000 Hz) are ignored. If you use the -V option, such deviations are flagged with warning messages.

# Bugs

audioplay currently supports a limited set of formats. If the input is not in a format supported by the audio device, you must first convert it to a temporary file. For example, to convert to voice on-the-fly, use the following command.

```
castle$ audioconvert -f voice | audioplay
```

# Options

- -? Print a command-line usage message.
- -b bal Set the output balance to the specified value before playing and reset it to its previous level when audioplay exits. The bal argument is an integer value between -100 and 100, inclusive. A value of -100 indicates left balance, 0 middle, and 100 right. If you do not specify this, leave the output balance at the level most recently set by any process.
- -d dev Direct output to an alternate audio device. If you do not specify the -d option, use the AUDOPLAY environment variable. Otherwise, use /dev/audio as the default.
- -i Immediately exit if the audio device is unavailable (that is, another process has write access), audioplay ordinarily waits until it can obtain access to the device. When you use the -i option and the device is busy, print an error message and exit immediately.
- -p speaker | line Select the built-in speaker (the default), headphone jack, or line out as the destination of the audio output signal. If you do not specify this, the output port remains unchanged. Not all audio adapters support all of the output ports. If the named port does not exist, use an appropriate substitute.
- -v vol Set the output volume to the specified value before playing and reset it to its previous level when audioplay exits. The vol argument is an integer value between 0 and 100, inclusive. If you do not specify this, leave the output volume at the level most recently set by any process.
- -V Give verbose output on the standard error when waiting for access to the audio device or sample rate deviations are detected.

# Operands

- -file Audio files named on the command line are played sequentially. If you specify no file names, the standard input stream (if it is not a TTY) is played. The input stream must contain an audio file header. You can use the special file name - to read the standard input stream instead of a file. If you supply a relative path name, the AUDOPATH environment variable is consulted.
