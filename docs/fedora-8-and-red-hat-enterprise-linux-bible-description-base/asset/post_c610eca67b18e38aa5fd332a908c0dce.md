
If two channels are available on a track, you can adjust them individually. With the track selected, use the `q`, `w`, and `e` keys to adjust the left, both, and right channels up, respectively. Use `z`, `x`, and `c` to adjust those same channels down, respectively. When you are done using `alsamixer`, press the Esc key to exit.

Here are a few general rules for adjusting your audio channels:

- To avoid unwanted noise on playback or record, mute any tracks you are not using.
- An icon representing your GNOME Volume Control utility should appear on your desktop panel. The single slider associated with that icon may be set to adjust your master volume or headphone port output. Right-click that icon and select **Preferences** to change to a different port.
- To test that your audio channels are working, use the `speaker-test` command. For example, `speaker-test -c4` will send a tone to each of four speakers in turn (front left, front right, rear left, and rear right) to check that each is working. Note that the tone output may surprise you with its loudness.

## Setting your sound card to record

I added this section on setting your sound card to record because people often miss this step. You may run the `arecord` command or communications application (such as Ekiga) and wonder why nothing records. The reason is that you need to identify the capture device to use before you record and make sure its level is set high enough to work.

The easiest way to set the channel to use for audio capture is to use the GNOME Volume Control window described earlier. Click the **Capture** tab to see the available channels for capturing audio input. Then make sure that all audio devices are muted except the one you want to record from. Available devices include microphone, line-in, and CD. A red X through a microphone icon beneath each capture device indicates that it is muted.

Move the slider for your capture device up to an appropriate level. Then connect your microphone or input device (to line in), and then start the application you want to record from.

> **TIP:** Audacity is a nice application for recording and working with recorded sound in Fedora. You can install the `audacity` package from the Fedora repository (type `yum install audacity`).

## Choosing audio players

There are audio players in Fedora and RHEL for playing music and sound files in a variety of formats. Without adding any software, you can play commercial music CDs and Ogg Vorbis audio (which you can rip and encode yourself). MP3 support can be added to some of these players, while MP3 players outside of Red Hat distributions are also available.

- **CD Player (`gnome-cd`)** — This is the CD player that comes with the GNOME desktop. Besides having standard play buttons, this player lets you get track information automatically from a CD database (such as freedb.org). Or, if your CD isn't listed in the database, you can enter your own track information manually.
- **KsCD Player (`kscd`)** — The KsCD player comes from the KDE desktop. To use KsCD, the `kdemultimedia` package must be installed. From the Applications menu (KDE desktop), select **Sound & Video** → **KsCD** (or type `kscd` from a Terminal window). Like `gnome-cd`, this player lets you get title, track, and artist information from the CD database, and lets you submit information you type in yourself to a CD database (if your CD isn't found there).
- **Rhythmbox (`rhythmbox`)** — Import and manage your music collection with Rhythmbox music management and playback software for GNOME. Rhythmbox uses GStreamer and Sound Juicer to extract music from a CD, and then compresses that music using Ogg Vorbis, FLAC, or a low-quality WAV (for speech) audio format. Besides allowing you to create playlists of your music library, Rhythmbox also has features for playing Internet radio stations. Open Rhythmbox from the Applications menu by selecting **Sound & Video** → **Music Player**.
- **XMMS (`xmms`)** — The X Multimedia System (XMMS) audio player provides a simple, graphical player for playing Ogg Vorbis, WAV, FLAC, and other audio formats. XMMS has a fairly simple Windows Winamp-like look and feel, which you can adjust using a few dozen skins. (The `xmms` package is available in the Fedora repository. To add CD playing support to `xmms`, install the `xmms-cdread` package as well.)
- **ogg123, mpg321, aplay, or play** — If you don't have access to the desktop, you can use the text-based `ogg123`, `mpg321`, or `play` commands. The `ogg123` command comes with the `vorbis-tools` package, `aplay` is part of the `alsa-utils` package, and `play` comes with the `sox` package in Fedora and RHEL. The `mpg321` command comes in the `mpg321` package, which is available from the Livna.org RPMs site. (The `mpg321` command is covered under the GPL. There is an `mpg123` project, which is no longer maintained and is not fully covered under the GPL.)

The default CD audio player is Totem (`totem` command) for the current release. Totem is primarily a video player, so you might want to change the default to some other player that includes CDDB support and other CD-playing features. You can do that with the Removable Drives and Media window, as described in detail in the next section.

> **NOTE:** If you try some of these CD players and your CD-ROM drive is not working, see the sidebar "Troubleshooting Your CD-ROM" for further information.

## Automatically playing CDs

When you put an audio CD into your CD-ROM drive, a media player (`totem`) automatically pops up on your desktop and begins playing the CD. If you are using the GNOME desktop, you can thank the GNOME Volume Manager. The GNOME Volume Manager monitors your CD-ROM drives (as well as your other removable media, such as DVDs and digital cameras) and opens a CD player when it sees an audio CD.

If you don't want to have CDs automatically start playing or if you want to use a different CD player by default, you can change that behavior using the GNOME Volume Manager's Removable Drives and Media Preferences window. Select **System** → **Preferences** → **Hardware** → **Removable Drives and Media**. Then from the **Multimedia** tab, either turn off the **Play audio CD** selection or change the command that is run (for example, to `gnome-cd -d`).

Refer to the "Managing removable media (CDs, DVD, and cameras)" section of Chapter 3 for details on using the GNOME Volume Manager to change CD playing and mounting preferences.

## Troubleshooting Your CD-ROM

If you are unable to play CDs on your CD-ROM drive, here are a few things you can check to correct the problem:

- Verify that your sound card is installed and working properly (see "Configuring a sound card" earlier in this chapter).
- Verify that the CD-ROM drive was detected when you booted Linux. If your CD-ROM drive is an IDE drive, type `dmesg | grep "hd."`. You should see messages about your CD-ROM that look like this: `hdc: CD-ROM CDU701, ATAPI CDROM drive;` or this: `hdc: ATAPI 14X CD-ROM drive, 128KB Cache.`
- If you see no indication of a CD-ROM drive, verify that the power supply and cables to the CD-ROM are connected. To make sure that the hardware is working, you can also boot to DOS and try to access the CD.
- Try inserting a software CD-ROM. If you are running the GNOME or KDE desktop, a desktop icon should appear indicating that the CD is mounted by itself. If no such icon appears, go to a Terminal window and type `mount /media/cdrecorder`. Then list the contents using the `ls /media/cdrecorder` command. This tells you if the CD-ROM is accessible.
- Check that your CD-ROM drive is not blacklisted because of buggy firmware or other issues. See www.tldp.org/HOWTO/Hardware-HOWTO/cdrom.html.
- If you get the CD-ROM working, but it fails with the message `CDROM device: Permission denied` when you try to play music as a nonroot user, the problem may be that the device related to that medium is not readable by anyone but root. Type `mount | grep media` to see what device name represents the drive. Then (as the root user), if, for example, the CD device were `/dev/scd0`, type `chmod 644 /dev/scd0` to enable all users to read your CD-ROM and to enable the root user to write to it. One warning: If others use your computer, they will be able to read any CD you place in this drive.
