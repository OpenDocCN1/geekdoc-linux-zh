
volume control. Generally, you should use the query macros first to establish the capabilities, or perhaps merely the presence, of a sound device before beginning to manipulate it.

Regarding the mixer, the sound API abstracts its capabilities into a set of channels, so the first thing you have to do is find out how many channels are available and what they are. Table 13.1 provides a partial list of the most common channels (a complete list is contained in `<sys/soundcard.h>`).

## Table 13.1: Common Mixer Channels

| Channel | Description |
|---|---|
| SOUND_MIXER_VOLUME | Master output level |
| SOUND_MIXER_BASS | Bass level of all output channels |
| SOUND_MIXER_TREBLE | Treble level of all output channels |
| SOUND_MIXER_SYNTH | Volume control of all synthesizer input such as the FM chip or the wave table |
| SOUND_MIXER_PCM | Output level of the audio devices /dev/audio and /dev/dsp |
| SOUND_MIXER_SPEAKER | Output level for the PC speaker, if it is connected directly to the sound card |
| SOUND_MIXER_LINE | Volume level for the line in jack |
| SOUND_MIXER_MIC | Volume level for microphone input |
| SOUND_MIXER_CD | Volume level for audio CD input |
| SOUND_MIXER_ALTPCM | Volume level for alternate audio device (such as the PAS16 boards Sound Blaster emulation) |
| SOUND_MIXER_RECLEV | Master recording volume level control |

The macro SOUND_MIXER_NRDEVICES reports the maximum number of devices known to the sound driver at any given time; SOUND_MIXER_READ_DEVMASK sets a bitmask that indicates the available channels.

SOUND_MIXER_READ_RECMASK sets a bitmask indicating the available recording devices. SOUND_MIXER_READ_STEREODEVS sets a bitmask indicating which channels are capable of supporting stereo output. This information gives you the ability to set the volume on each channel independently, thus providing a type of balance control. Another call, SOUND_MIXER_READ_CAPS, sets a bitmask that describes a mixer's general capabilities.

The mixer portion of the sound API also provides two macros that contain printable strings for human-readable output: SOUND_DEVICE_LABELS and SOUND_DEVICE_NAMES. The only difference between these is that the labels in SOUND_DEVICE_NAMES have no embedded blanks or uppercase letters.

To get and set the mixer volume, finally, use the `SOUND_MIXER_READ`(channel) and `SOUND_MIXER_WRITE`(channel) macros. The following code snippet, for example, sets the current volume of the mixer device to 50 percent of its maximum range:

```c
int vol = 50;

if((ioctl(fd, SOUND_MIXER_WRITE(SOUND_MIXER_MIC), &vol)) < 0)
	/* Call failed, so degrade gracefully */
else
	/* Call succeeded, more code here */
```

vol stores the volume level (often called gain) to set, and SOUND_MIXER_MIC is the channel on which the volume is being set. The first byte contains the volume for the left channel, while the right channel is set in the second byte. After the call, vol contains the new value, which is slightly different from the volume level you set due to hardware peculiarities.

## Examples

![](img/be588b36b489136ce784030a08a1d3d4_319_0.png)

### Example 1

The following program, `mixer_status`, queries the mixer device for its available channels and displays their current settings:

```c
/*
 * mixer_status.c - example program to display mixer settings.
 * Copyright (c) 1994-96 Jeff Tranter (jeff_tranter@xmission.com)
 * Heavily modified by Kurt Wall (kwall@xmission.com)
 */

#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <sys/soundcard.h>

/* Utility function for printing status */
void prn_stat(int condition);

int main(void)
{
    int fd;                        /* File descriptor for mixer device */
    int level;                     /* Volume setting */
    char *device = "/dev/mixer";

    /* Bitmasks for device settings */
    int recsrc, devmask, recmask, stereodevs, caps;
    /* Names of mixer channels */
    const char *labels[] = SOUND_DEVICE_LABELS;
    int i;

    /* Open the mixer device read only */
    if((fd = open(device, O_RDONLY)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    /* Get mixer information */
    if((ioctl(fd, SOUND_MIXER_READ_RECSRC, &recsrc)) < 0)
        perror("SOUND_MIXER_READ_RECSRC");
    if((ioctl(fd, SOUND_MIXER_READ_DEVMASK, &devmask)) < 0)
        perror("SOUND_MIXER_READ_DEVMASK");
    if((ioctl(fd, SOUND_MIXER_READ_RECMASK, &recmask)) < 0)
        perror("SOUND_MIXER_READ_RECMASK");

    if((ioctl(fd, SOUND_MIXER_READ_STEREODEVS, &stereodevs)) < 0)
        perror("SOUND_MIXER_READ_STEREODEVS");
    if((ioctl(fd, SOUND_MIXER_READ_CAPS, &caps)) < 0)
        perror("SOUND_MIXER_READ_CAPS");

    /* Print mixer information */
    printf("Status of %s:\n\n", device);
    printf("Mixer         Recording Active    Stereo\nCurrent\n");
    printf("Channel       Source    Source    Device\nLevel\n");
    printf("-----------------------------------------------------------------\n");
    printf("---------------------------\n");

    /* Loop over all devices */
    for (i = 0; i < SOUND_MIXER_NRDEVICES; ++i) {
        /* Only interested in available devices */
        if((1 << i) & devmask) {
            /* Print channel number and name */
            printf("%2d %-8s", i, labels[i]);
            /* Is it a recording source? */
            prn_stat((1 << i) & recmask);
            /* Is it active? */
            prn_stat((1 << i) & recsrc);
            /* Does it have stereo capability? */
            prn_stat((1 << i) & stereodevs);
            /* If stereo, show both levels */
            if ((1 << i) & stereodevs) {
                if((ioctl(fd, MIXER_READ(i, &level)) < 0)
                    perror("SOUND_MIXER_READ");
                else
                    printf(" %3d%% %3d%%", level & 0xff, (level & 0xff00) >> 8);
            } else { /* Only one channel */
                if((ioctl(fd, MIXER_READ(i, &level)) < 0)
                    perror("SOUND_MIXER_READ");
                else
                    printf("    %3d%%", level & 0xff);
            }
        }
        printf("\n");
    }

    /* Are recording sources exclusive? */
    printf("\nNote: Choices for recording source are ");
    if (!(caps & SOUND_CAP_EXCL_INPUT))
        printf("not ");
    printf("exclusive.\n");

    /* Close */
    close(fd);
    return 0;
}

void prn_stat(int condition)
{
    condition ? printf("  YES  ") : printf("  NO  ");
}
```

The first five `ioctl` calls set bitmasks in their corresponding integer arguments (`recsrc`, `devmask`, `recmask`, `stereodevs`, and `caps`). After printing a table header, `mixer_status` loops through the available mixer channels. If the mixer has that particular channel, the conditional block executes and displays some of the available information for that channel.

Note in particular the way the bitmasks are tested:

`(1 << channel) & bitmask;`

The parenthesized expression left-shifts a channel number onto 1, and then bitwise ANDs the resulting value with `bitmask`. If the given channel exists, the expression evaluates to 1. If the channel is not available, it evaluates to 0. So, for example, if a channel, say, `SOUND_MIXER_VOLUME` is stereo-capable, `(1 << SOUND_MIXER_VOLUME) & stereodevs` (as set in the program) evaluates to 1.

On my system, which has a genuine Sound Blaster, `mixer_status` generated the following output:

![](img/be588b36b489136ce784030a08a1d3d4_322_0.png)

## Output

```
$ ./mixer_status
Status of /dev/mixer:
```

|   | Mixer Channel | Recording Source | Active Source | Stereo Device | Current Level |
|---|---|---|---|---|---|
| 0 | Vol | NO | NO | YES | 90% 90% |
| 1 | Bass | NO | NO | YES | 75% 75% |
| 2 | Trebal | NO | NO | YES | 75% 75% |
| 3 | Synth | YES | NO | YES | 75% 75% |
| 4 | pcm | NO | NO | YES | 100% 100% |
| 5 | Spkr | NO | NO | NO | 75% |
| 6 | Line | YES | NO | YES | 75% 75% |
| 7 | Mic | YES | YES | NO | 0% |
| 8 | CD | YES | NO | YES | 75% 75% |
| 9 | Mix | NO | NO | NO | 0% |
| 12 | IGain | NO | NO | YES | 75% 75% |
| 13 | OGain | NO | NO | YES | 75% 75% |

Note: Choices for recording source are not exclusive.

As you can see, the mixer device lacks several channels, such as an alternative audio device (`SOUND_MIXER_ALTPCM`).

![](img/be588b36b489136ce784030a08a1d3d4_323_0.png)

### Example 2

The next program, `setvol`, enables you to set the volume level interactively.

```c
/*
 * setvol.c - Set volume level interactively
 * mixer device
 * Copyright (c) 1994-96 Jeff Tranter (jeff_tranter@mitel.com)
 * Heavily modified by Kurt Wall (kwall@mission.com)
 */
#include <unistd.h>

#include <stdlib.h>
#include <stdio.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <sys/soundcard.h>

int main(int argc, char *argv[])
{
    int left, right, level;          /* Volume settings */
    int device;                     /* Which mixer device to set */
    int i;                          /* File descriptor for mixer */
    int fd;
    /* Bitmasks for mixer information */
    int devmask, stereodevs;
    char *dev = "/dev/mixer";
    char buf[5];

    /* Open mixer for read and write */
    if((fd = open(dev, O_RDWR)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    /* Get information about the mixer */
    if((ioctl(fd, SOUND_MIXER_READ_DEVMASK,
             &devmask)) < 0)
        perror("SOUND_MIXER_READ_DEVMASK");
    if((ioctl(fd, SOUND_MIXER_READ_STEREODEVS,
```
