# identify

**identify** *filename*
Determines the format and characteristics of the graphic file specified by *filename* and checks to see whether the image is incomplete or corrupt. You can specify more than one filename using shell patterns (see the section “Shell Patterns” in Chapter 4). Use with the --verbose option to see a wealth of information about each graphic file. This utility is part of the ImageMagick package, which can be downloaded at http://www.imagemagick.org.
See also **combine**, **convert**, **mogrify**, **montage**.

OPTIONS

Use This Option | To Do This
:-- | :--
--ping | Determine image characteristics efficiently
--verbose | Show detailed information about the image

EXAMPLE

This Command | Does the Following
:-- | :--
`identify -verbose image1.jpg` | Displays information about the specified graphics file (image1.jpg).

# mikmod

**mikmod** [ *option* ] [ *module* | *playlist* ]
Launches an interactive text-based utility that plays a variety of SoundTracker and SoundTracker-derived module formats. Also handles playlists. Supported module formats include IT, XM, MOD, MTM, S3M, STM, ULT, FAR, MED, DSM, AMF, IMG, and 669. See the Commands table in this section for commands that you can use in the interactive mode.