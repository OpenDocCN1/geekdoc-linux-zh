# 82

# audioplay

The format conversion does not always keep up with the audio output. If this is the case, convert to a temporary file before playing the data.

# Options

+   -?\ Print a command-line usage message.

+   -b bal Set the output balance to the specified value before playing begins and reset it to its previous level when audioplay exits. The bal argument is an integer value between -100 and 100, inclusive. A value of -100 indicates left balance, 0 middle, and 100 right. If you do not specify this, leave the output balance at the level most recently set by any process.

+   -d dev Direct output to an alternate audio device. If you do not specify the -d option, use the AUDOPLAY environment variable. Otherwise, use /dev/audio as the default audio device.

+   -i Immediately exit if the audio device is unavailable (that is, another process has write access), audioplay ordinarily waits until it can obtain access to the device. When you use the -i option and the device is busy, print an error message and exit immediately.

+   -p speaker | line Select the built-in speaker (the default), headphone jack, or line out as the destination of the audio output signal. If you do not specify this, the output port remains unchanged. Not all audio adapters support all of the output ports. If the named port does not exist, use an appropriate substitute.

+   -v vol Set the output volume to the specified value before playing begins and reset it to its previous level when audioplay exits. The vo2 argument is an integer value between 0 and 100, inclusive. If you do not specify this, leave the output volume at the level most recently set by any process.

+   -V Give verbose output on the standard error when waiting for access to the audio device or sample rate deviations are detected.

# Operands

+   -file Audio files named on the command line are played sequentially. If you specify no file names, the standard input stream (if it is not a TTY) is played. The input stream must contain an audio file header. You can use the special file name - to read the standard input stream instead of a file. If you supply a relative path name, the AUDOPATH environment variable is consulted.

# Usage

See largefile(5) for the description of the behavior of audioplay when encountering files greater than or equal to 2 Gbytes (2**31 bytes).