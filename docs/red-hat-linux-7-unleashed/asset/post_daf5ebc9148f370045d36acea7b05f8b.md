
Programs can turn off the processing that the line driver does by default; the resulting behavior (raw mode) allows programs to read unprocessed input from the terminal driver (for example, CR is not mapped to LF), and control characters don't produce the signals described in the table earlier in this section. The `stty sane` command will return things to normal.

## Serial Communications

Although the terminal interfaces used most commonly under Linux are the console driver and the pseudo-terminals driven by programs such as *xterm*, *script*, and *expect*, the original terminal interface involved *serial* communications. In fact, this still lingers; in a pseudo-tty associated with an xterm window still has an associated baud rate as shown in the example in the section “The Terminal Device Driver” earlier in this chapter. Changing this baud rate has no actual effect. For real serial ports, however, the baud rate and many other parameters have a direct relevance. The device nodes relating to the serial ports are composed of two “teams,” with the names `/dev/cua*` and `/dev/ttyS*`. Starting with version 2.2 of the kernel, `/dev/ttyS*` is the “correct” name to use. `/dev/cua*`, while most likely, disappear from the next version or two. The device nodes allow you to use the same serial hardware for both incoming and outgoing serial connections.

## Configuring the Serial Ports

Serial port configuration is mostly done either with the `stty` command or directly by programs using the interface outlined in the *termios* manual page. The `stty` command offers almost all the configuration possibilities provided by *termios*; however, there are configuration issues for serial hardware that are not addressed by `stty`. The `setserial` command allows the configuration of the correct IRQ settings for each serial port and of extra-fast baud rates that the standard *termios* specification doesn't provide. For more detailed information, refer to the Linux Serial HOWTO and the manual page for *setserial*.

## Generic SCSI Devices

Not all SCSI devices are hard disks, CD-ROM drives, or tape drives. Some are optical scanners, CD-ROM recorders, or even electron microscopes. The kernel can't possibly abstract the interfaces for all possible SCSI devices, so it gives user programs direct access to SCSI hardware via the *generic SCSI* devices. These enable programs to send arbitrary SCSI commands to hardware. Although this arrangement offers the opportunity of wreaking havoc by mistake, it also offers the capability of driving all sorts of interesting hardware, of which the principal examples are CD-ROM recorders. The SCSI device nodes all have names starting with `/dev/sg_`. SCSI commands are sent to the devices by writing data to the device, and the results are read back by reading from the device.

### CD-ROM Recorders

*CD-ROM recorders* are devices for recording data on special media that can be read in ordinary CD-ROM drives. There are two stages in the writing of a CD: generating the CD image and writing that image to the media.

The surface of a CD-R (recordable CD) is only writable once, so if `mkisofs` worked like the other `mfs` tools, it would always generate image files representing empty CDs. For this reason, `mkisofs` populates the filesystem with files as it generates the image file. The same principles apply to CD-RW, which are CD-R that are rewritable. Under Linux they are treated just as CD-R, the only difference being that you can record over them a second time, or many more times for that matter.

The CD image file is produced by the `mkisofs` program, which generates the structures for an ISO 9660 filesystem and populates it with the files from a directory tree. CDs are not writable in the same sense as block devices; this is why they are not actually block devices. The image file must be written to the CD-R with a specialized program, `cdrecord`, which understands all the various proprietary schemes used for driving CD writers. All the CD writers supported by Linux (as of version 2.0.30 of the kernel) are SCSI devices, so the kernel accommodates this by providing access to the generic SCSI device interface that enables a program to send SCSI commands to these devices.

However, there is also support for some IDE CD writers, but these are all handled by using a special driver that lets IDE emulate SCSI.

While *burning* (writing) a CD, it is usually important that the flow of data to the writer keeps up with the speed at which the writer is going; otherwise, if the writer runs out of data to write, the CD-R is ruined. For this reason, it is usual to use `mkisofs` to generate an image file and then separately use `cdrecord` to write this image file to the CD writer.

It is possible to use a pipe to send the data from `mkisofs` directly to `cdrecord`. This often works either because a fast machine can ensure that `mkisofs` supplies the data fast enough to keep the CD writer busy or because the CD writer is not sensitive to data undersuffs. (Some of the more expensive ones have internal hard disks or very big RAM caches to which the data is written during an intermediate stage.) This technique is not recommended, however, because the generation of the intermediate image file has other benefits; it enables you to test your CD image before the final writing of the data takes place.

### Testing CD Images

Just as you can use `mfs` to create a filesystem inside an ordinary file, you can mount filesystems contained in ordinary files by using the loopback device driver described previously. The first example of mounting a loopback filesystem is a demonstration of how you can test a CD image.

## Other Character Devices

Several other varieties of character devices, such as `/dev/null`, are used frequently.

## The Controlling Terminal Device—`/dev/tty`

Most processes have a controlling terminal, particularly if they were started interactively by a user. *The controlling terminal*, which I refer to as simply `/dev/tty`, is used for initiating a conversation directly with the user (for example, to ask him something). An example is the `crypt` command:

```
$ fmt diary.txt | crypt | mail -s Diary confidant@linux.org
Enter key:
$
```

Here, the `crypt` command has opened `/dev/tty` to obtain a password. It was not able to use its own standard output to issue the prompt and its standard input to read the password because they are being used for the data to be encrypted.

> **Note**
> 
> Of course, it's unusual to send email encrypted with `crypt`. A better choice is probably **GnuPG**. This is an Open Source replacement for PGP.

More useful examples are commands that need to ask the operator something even if the input and output are redirected. A case in point is the `cpio` command, which prompts the operator for the name of a new tape device when it runs out of space. See the section “`/dev/null` and Friends” later in this chapter for another example.

## Nonserial Mice

Many computers have bus or PS/2 mice instead of serial mice. This arrangement has the advantage of keeping both of the two standard serial ports free, but the disadvantage of using up another IRQ. These devices are used by `gpm` and the X Window System, but most other programs don’t interact with them directly. Setting up your system with these mice is easy; the Red Hat Linux installation process pretty much takes care of it for you. If you have problems with your mouse, however, you should read the manual page for `gpm` and the Linux BusMouse HOWTO.

## Audio Devices

There are several audio-related device nodes on Linux systems, and they include the following:

| Device Node | Description |
| :--- | :--- |
| `/dev/sndstat` | Indicates the status of the sound driver |
| `/dev/audio*` | Sun-compatible audio output device |
| `/dev/dsp*` | Sound sampling device |
| `/dev/mixer` | For control of the mixer hardware on the sound card |
| `/dev/music` | A high-level sequencer interface |
| `/dev/sequencer*` | A low-level sequencer interface |
| `/dev/midi*` | Direct MIDI port access |

Setting up the sound driver under Linux can sometimes be difficult, but the `sndconfig` utility included with Red Hat makes this easier for most cards. If you have problems be sure to check out the Linux Sound HOWTO which provides useful advice.

## Random Number Devices

Many program features require the generation of apparently random sequences. Examples include games, numerical computations, and various computer-security-related applications. Numerical computing with random numbers requires that the sequence of random numbers be repeatable but also that the sequence “look” random. Games require apparently random numbers, but the quality of the random numbers is not quite as critical as for numerical computation programs. The system libraries produce repeatable sequences of “pseudo-random” numbers that satisfy these requirements well.

On the other hand, in many aspects of computer security, it is advantageous to generate numbers that really are random. Because you can assume that an attacker has access to the same sorts of random number generators that you do, using them is not very safe; an attacker can use these generators to figure out what random number you’ll use next. Sequences that are genuinely random must in the end be produced from the real world and not from the internals of some computer program. For this reason, the Linux kernel keeps a supply of random numbers internally. These numbers are derived from very precise timings of the intervals between “random” external events—for example, the user’s key presses on the keyboard, mouse events, and even some interrupts (such as from the floppy disk drive and some network cards). These “real” random numbers are used in security-critical contexts—for example, the choosing of TCP sequence numbers.
