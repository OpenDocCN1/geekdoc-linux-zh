
forever; you must terminate it by typing CTRL-C. The second command plays back the file you've just recorded, so you can check to see that it recorded correctly.

**Caution** Your mixer's audio gain settings can be extremely important when recording a file. If set too high, loud sounds will reach plateaus at the maximum values you can record, which results in a static-filled distortion. If set too low, the sound may be inaudible unless you adjust your playback volume settings upward. Using GUI tools and editors can sometimes help by providing a visual display of recording levels.

## GUI Audio Playback and Recording Tools

The play program is a very basic recording program. The program provides little in the way of feedback about a recording in progress, and of course as a text-mode program, it's not appealing to less experienced users. One solution is a simple X-based audio recorder, such as the GNOME Sound Recorder (shown in Figure 27-3). This program has capabilities similar to those of play, but it provides a GUI interface. You can launch the program by typing grecord at an xterm prompt or by selecting the program from the GNOME menus. KDE provides a similar tool, krecord, which you can launch by typing krecord at an xterm prompt or selecting the program from the KDE menus. You can record a file by clicking the Record button, play it back by clicking Play, and save it by selecting File > Save As from the menu. You can adjust various recording options, such as the sample rate and number of channels, by selecting Settings > Preferences. This action produces a dialog box in which you can set many of the options you can set in play/record via its command-line switches.

More sophisticated GUI audio tools, such as glame, xvave, and Sweep provide the means to edit an audio file. Figure 27-4 shows a Sweep editing window. This window displays the sound file visually—time runs from left to right, and the volume of the sound is represented by the magnitude of the sound waves in the editing window.

![](img/f34d37e3abe9f4517128e54f80ab2616_693_0.png)

Figure 27-3. Simple GUI audio playback and recording utilities provide few options, but are adequate for simple playback or recording tasks.

![](img/f34d37e3abe9f4517128e54f80ab2616_694_0.png)

Figure 27-4. Advanced GUI audio utilities enable you to edit a sound file much as you can edit text files or graphics files.

You can select blocks of sound and apply various editing tools to them. For instance, you can increase or decrease the sample’s volume, reverse the sample, apply echo effects, and so on. Precisely what options are available depends upon the editor, of course.

## MP3 Tools

Audio CDs are a popular format for storing music; but for some uses, they’re awkward—as physical media, audio CDs can get lost or damaged, and it can be a hassle to juggle them in and out of players. It’s possible to extract audio tracks from a CD and store them as audio files, but these files tend to be fairly large. CD-quality recording is 44.1 kHz, 16-bit, with two channels, which works out to about 10MB per minute. Such values are large enough that even a modern 120GB hard disk could hold only about 20 CDs worth of music. To cope with this problem, a compressed format has been developed: MP3. Like the Joint Photographic Experts Group (JPEG) graphics file format, the MP3 file format is lossy, meaning that it intentionally corrupts data in the interest of saving file size. MP3 is designed to create changes that are difficult for humans to hear; though, so a huge size decrease can be attained with only a modest decrease in quality. High-quality MP3 files are usually about a fifth the size of their uncompressed originals, and lower-quality MP3 files can be even smaller. For this reason, the MP3 format has become a popular one for storing music for playback on computers. Portable MP3 players, similar to portable cassette or CD players, also exist, and they can hold dozens or hundreds of songs. Being able to manipulate and play MP3 files is therefore an important capability.

**Caution** Most music available today is copyrighted. Although MP3 manipulation programs enable you to copy such music, doing so may be illegal. As a general rule, copying for purely personal use, such as placing a library of MP3 files on your computer or a portable MP3 player, is OK, so long as you possess the original source. Giving MP3 files of copyrighted music to friends is not legal, though. Likewise, downloading MP3 files containing copyrighted music is not legal unless this download is authorized by the copyright holder (say, if you’ve bought a song in MP3 form on an authorized web site).

## Creating MP3 Files

If you want to create MP3 files from an audio CD, the first step is performing digital audio extraction (DAE), often called ripping, on the source CD. This step involves retrieving the digital audio data from the CD, using its EIDE or SCSI interface. After you’ve created uncompressed audio files, you can convert them to MP3 format. Neither of these steps uses your sound card directly. In practice, it’s sometimes possible to perform both steps at once. For instance, the text-based **c2dmp3** program provides a one-step method for performing this task. After installing the **c2dmp3** package or port, type **c2dmp3** to start the process.

**Caution** To perform DAE, you must have read/write access to your CD-ROM drive ( /dev/acd0 for EIDE CD-ROMs). The c2dmp3 software also uses the current directory to store temporary files, so you should launch the program only from a directory to which you have write access, and on a filesystem that has at least enough free space to hold a temporary file of compressed . wav files (about 10MB per minute).

After you start c2dmp3, the program asks you a series of questions:

- 1. Encoding option You can choose to encode an entire CD, just some tracks, or an existing . wav file. You can also use c2dmp3 to extract a track as a . wav file without encoding it as an MP3 file.
- 2. Sampling rate This term is used oddly in reference to MP3 files. Normally, the sampling rate is the number of samples per second, as described earlier in “Command-Line Audio Playback and Recording Tools.” In the case of MP3 files, though, it refers to the rate at which the file must be read to be played back, in kilobits per second. This measurement can be useful if you want to use MP3 files over a streaming medium—that is, delivered in real time via a web server or the like. For personal use, though, it’s best thought of as a compression level option. c2dmp3 provides three sampling rate options: 56, 128, and 256. The higher the sampling rate, the better the resulting sound quality, but the larger the file.
- 3. Output filename You must specify the output filename for the MP3 file. These files normally have names that end in .mp3.
- 4. CD-ROM drive The cdd2mp3 utility defaults to reading files from /dev/cdrom, but this file may not be present on your system. You may need to specify the actual CD-ROM device, such as /dev/acd0 for EIDE CD-ROMs or /dev/cd0 for SCSI CD-ROMs. Alternatively, you can create a symbolic link from the actual device to /dev/cdrom.
- 5. Track number If you want to encode just one track, the program asks you for the track number.

After you enter this information, cdd2mp3 begins work. The first step is reading the data from the CD-ROM drive. With many CD-ROM drives, this process takes much longer than it would take to play the track on an audio CD player. The reason has to do with the way that music is encoded on the CD, as opposed to data; there's no easy way to reliably seek to a specific point in an audio track, so whenever cdd2mp3 requests audio data, it must compare what it's retrieved to what it retrieved the last time to avoid overlapping or missing data. The retrieved track is stored in a file named track_n.wav, where n is the track number. After cdd2mp3 has retrieved the track, the program converts the .wav file into an MP3 file. This process can also take several minutes, depending upon your CPU speed—essentially, cdd2mp3 must compress the multi-megabyte .wav file, which is a CPU-intensive task. The result should be a file with the name you specified, which you can test with an MP3 player.

## Playing MP3 Files

Many MP3 players are available for FreeBSD. A few options include:

- **ksmplay** This program is a text-based MP3 player. It uses the curses library to position text elements on the screen.
- **mp3blaster** This program is another curses-based text MP3 player.
- **mp3** This is a KDE-based MP3 player.
- **replay** This is a GNOME-based MP3 player.
- **x11amp** This is a popular X-based MP3 player.

Playing an MP3 file works much like playing a .wav or other audio file, as described earlier, in "Command-Line Audio Playback and Recording Tools" and "GUI Audio Playback and Recording Tools." MP3 players are likely to include a somewhat different mix of options, though. One feature that these programs usually include is the ability to handle a playlist, which is a list of files that you want to play in one session. You can often save a playlist so that you can easily play the same set of songs without loading them all into a playlist every time you launch the MP3 player. Some MP3 players, such as x11amp (shown in Figure 27-5), provide additional options, such as a graphic equalizer.
