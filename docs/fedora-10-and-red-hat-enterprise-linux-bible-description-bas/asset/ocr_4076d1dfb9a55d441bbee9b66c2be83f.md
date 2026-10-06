# Chapter 8: Music, Video, and Images in Linux 327

There are lots of sites on the Internet for downloading MIDI files. Try the Ifni MIDI Music site (http://www.ifnmidi.com), which contains songs by the Beatles, Led Zeppelin, Nirvana, and others organized by album. Most of MIDI music is pretty simple, but you can have some fun playing it.

Fedora and RHEL come with the midi player. Kmid is not installed by default (find it in the kimedia package on the DVD). Kmid provides a GUI interface for midi music, including the ability to display karaoke lyrics in real time. There is the timidity+ package on the DVD, which lets you run MIDI audio from a Terminal window.

> NOTE: Use the timidity player if your sound card doesn't include MIDI support (install the timidity package). It can convert MIDI input into WAV files that can play on any sound card. Start timidity, type timidity.file at the command-prompt.

To start kmid, use kmid & from a Terminal window.

# Converting audio files with SoX

If you have a sound file in one format, but you want it to be in another format, Linux offers some conversion tools you can use to convert the file. The sox utility can translate and from any of the audio formats listed in Table 8-1.

# Table 8-1: Sound Formats Supported by the sox Utility

| File Extension or Pseudonym | Description | File Extension or Pseudonym | Description |
|---|---|---|--|
|.svx | 85VX Amiga musical instrument description format. | .aiff | Apple Ilc/Ilgs and SGI AIFF files. May require a separate archive to work with these files. |
|.au,.snd | Sun Microsystems AU audio files. This is a popular format. | .avr | Audio Visual Research format, used on the Mac. |
|.cdr | CD-R files used to master compact discs. | .cvs | Continuously variable slope delta modulation, which is used for voice mail and other speech compression. |
|.dat | Text data files, which contain a text representation of sound data. | .gsm | Lossy Speech Compression (GSM 06.10), to shrink audio data in voice mail and similar applications.