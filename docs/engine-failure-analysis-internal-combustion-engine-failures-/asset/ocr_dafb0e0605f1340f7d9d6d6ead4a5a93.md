# # cdda2wav

**cdda2wav [ option ] [ *filename* ]**

Reads audio tracks from audio CD-ROMs and writes the data to WAV files. If you do not specify a filename, the utility writes to **audio.wav** in the working directory. By default, the program samples the CD-ROM audio in stereo, using a sampling rate of 44,100 cycles per second.

> **TIP** Works if downloaded from RPM.

See also **cdparanoia**.

# ## OPTIONS

| Use This Option | To Do This |
|---|---|
| `-D *device* `-device` | Use the specified device (such as `/dev/cdrom`). For SCSI drives, use the generic_scsi interface (see `-l`) and indicate the SCSI bus number, ID, and LUN. Use the following syntax: `-D0, 4, 0` (bus 0, ID 4, LUN 0). |
| `-A *auxdevice* `-auxdevice *auxdevice`` | Use *auxdevice* as the CD-ROM drive for cooked ioctl usage. |
| `-a *divider* `-divider *divider`` | Set the rate to 44100Hz / *divider*. |
| `-B* `-bulk`` | Copy each track into a separate file. |
| `-b *bits* `-bits-per-sample *bits`` | Set the number of bits to sample per channel (8, 12, or 16). |
| `-c *channels* `-channels *channels`` | Specify the number of channels to use, as follows:
* **1** Mono recording.
* **2** Stereo recording.
* **s** Stereo recording with both channels swapped. |