
## Graphic File Types

The following table lists the graphic file formats that you are likely to encounter on a Linux system, organized by suffix (extension).

### COMMON GRAPHIC FILE FORMATS

| Extension | Description |
| :--- | :--- |
| .bmp, .dib | Microsoft Windows bitmap image file |
| .cgm | Computer Graphics Metafile |
| .eps | Adobe Encapsulated PostScript file |
| .gif | CompuServe graphics interchange format |
| .hpgl | Hewlett Packard plotter file |
| .ico | Microsoft Windows icon |
| .jpg, .jpeg, .jfif | Joint Photographic Experts Group JFIF format |
| .pbm | Portable bitmap format file |
| .pcd | Kodak Photo CD-ROM file |
| .pcx | PC Paintbrush file |
| .pgm | Portable graymap format (gray scale) |
| .pict | Apple Macintosh QuickDraw/PICT file |
| .png | Portable Network Graphics |
| .pnm | Portable anymap |
| .tga | Truevision Targa image file |
| .tiff | Tagged Image File Format |
| .xbm | X Windows system bitmap |
| .xpm | X Windows system pixmap file |
| .xwd | X Windows system window dump file |

## Alphabetical Command Reference

This section details commands for the following tasks:

- Playing, recording, and manipulating sound files (aumix, mikmod, mpg123, play, playmidi, rec, sox).
- Playing audio CD-ROMs (cdp).
- Converting and processing graphic files (combine, convert, identify, mogrify, montage).
- Recording CD-ROM audio tracks to WAV files (cdda2wav, cdparanoia).
- Creating labels for CD-ROM jewel boxes (cdlabelgen).

## aumix

**aumix [option]**

If typed without an argument, this command launches an interactive, text-based program that controls the various settings of the audio device. See the Commands table in this section for commands you can use in the interactive mode.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -b[ + | - ] [ n ] | Set the bass gain. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10–100). |
| -C filename | Specify a filename containing a color scheme. |
| -cl[ + | - ] [ n ] | Set the CD-ROM gain. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level. |
| -d device | Use the specified device instead of the default. |
| -f filename | Save settings to the specified filename. |
| -i[ + | - ] [ n ] | Set the line-in gain. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10–100). |
| -l[ + | - ] [ n ] | Set the line gain. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10–100). |
| -L | Load settings from $HOME/.aumixrc, or /etc/aumixrc if the former is inaccessible. |
| -m [+\|-][n] | Set the microphone level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -o [+\|-][n] | Set the line-out level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -p [+\|-][n] | Set the PC speaker level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -q | Query all devices and print their settings. |
| -s [+\|-][n] | Set the synthesizer level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -S [+\|-][n] | Save settings to $HOME/.aumixrc. |
| -t [+\|-][n] | Set the treble level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -v n | Set the main volume to the desired percentage (n). |
| -w [+\|-][n] | Set the PCM level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |
| -x [+\|-][n] | Set the imix level. Specify one of the following: + to increment by one level, - to decrement by one level, n to set the specific level (10-100). |

### COMMANDS

| Use This Command | To Do This |
| :--- | :--- |
| +, right arrow (→) | Increase level of the selected channel by 3%. |
| -, left arrow (←) | Decrease the level of the selected channel by 3%. |
| [ | Set the level of the selected channel to 0%. |
| ] | Set the level of the selected channel to 100%. |
| 1 | Set the level of the selected channel to 10%. |
| 2 | Set the level of the selected channel to 20%. |
| 3 | Set the level of the selected channel to 30%. |
| 4 | Set the level of the selected channel to 40%. |
| 5 | Set the level of the selected channel to 50%. |
| 6 | Set the level of the selected channel to 60%. |
| 7 | Set the level of the selected channel to 70%. |
| 8 | Set the level of the selected channel to 80%. |
| 9 | Set the level of the selected channel to 90%. |
| Q, q | End the program. |
| K, k | Show a description of the functions of keys and return to the Level/Balance screen. |
| L, l | Load settings from `$HOME/.aumixrc`, or from `/etc/aumixrc` if `$HOME/.aumixrc` is not available. |
| M, m | Mute or unmute. |
| O, o | Mute all channels but the current one. Use `U` or `u` to return to the main screen. |
| PgDn, down arrow (↓) | Select the next control down. |
| PgUp, up arrow (↑) | Select the next control up. |
| S, s | Save settings to the rc file. |
| U, u | Undo any muting. |
| Tab, Enter, <, >, comma and period (.) | Toggle between level and balance controls. |

### EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| aumix | Starts the volume control utility in the interactive mode. |

## cdda2wav

**cdda2wav [ option ] [ *filename* ]**

Reads audio tracks from audio CD-ROMs and writes the data to WAV files. If you do not specify a filename, the utility writes to **audio.wav** in the working directory. By default, the program samples the CD-ROM audio in stereo, using a sampling rate of 44,100 cycles per second.

> **TIP** Works if downloaded from RPM.

See also **cdparanoia**.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-D *device* `-device` | Use the specified device (such as `/dev/cdrom`). For SCSI drives, use the generic_scsi interface (see `-l`) and indicate the SCSI bus number, ID, and LUN. Use the following syntax: `-D0, 4, 0` (bus 0, ID 4, LUN 0). |
| `-A *auxdevice* `-auxdevice *auxdevice`` | Use *auxdevice* as the CD-ROM drive for cooked ioctl usage. |
| `-a *divider* `-divider *divider`` | Set the rate to 44100Hz / *divider*. |
| `-B* `-bulk`` | Copy each track into a separate file. |
| `-b *bits* `-bits-per-sample *bits`` | Set the number of bits to sample per channel (8, 12, or 16). |
| `-c *channels* `-channels *channels`` | Specify the number of channels to use, as follows:<br>- **1** Mono recording.<br>- **2** Stereo recording.<br>- **s** Stereo recording with both channels swapped. |
| `-C endianness, --cdrom-endianness endianness` | Sets the endianness (bit order) of the CD-ROM device to little (LSB), big (MSB), or guess. |
| `-d duration, --duration` | Set the recording duration in seconds. Use 0 for the whole track. |
| `-e, --echo` | Copy audio data to the sound device while recording. |
| `-E endianness, --output-endianness endianness` | Set the endianness (bit order) of the output device to little (LSB) or big (MSB). |
| `-F, --find-extremes` | Find extreme amplitudes in samples. |
| `-G, --find-mono` | Determine whether input samples are in mono. |
| `-H, --no-infifo` | Skip writing the info and cddb files. |
| `-i index, --index index` | Start at the specified index. |
| `-I interface, --interface interface` | Set the interface for CD-ROM access to generic, scsi or cooked, ioctl. For SCSI CD-ROM drives on Linux, use the generic, scsi interface. |
| `-J, --info-only` | Provide information about the disk without actually writing any information. |
| `-l n, --buffers-in-ring n` | Uses a ring buffer with n buffers total. |
| `-m, --mono` | Record in mono. |
| `-M n --md5 n` | Calculate MD-5 checksum for n bytes from the beginning of the track. |
| `-n n, --sectors-per-request n` | Read n sectors per request. |
| `-O type, --output-format type` | Specify the output type (WAV, SUN, CDR, or RAW). |
| `-o n --offset n` | Start n offset sectors behind the start track. |
