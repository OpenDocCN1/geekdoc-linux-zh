Cross-CD playlists of MP3 files are no problem, provided you've created the MP3 files.

+   ■ **CPU load** Playing an MP3 file requires a certain amount of CPU time to decompress the MP3 data and send it to the sound card. Playing an audio CD, on the other hand, requires almost no CPU time.

In the end, whether you want to play your audio CDs directly or extract CD tracks into MP3 files and play them indirectly is a matter of personal preference and your specific needs.

# # Audio/Video Applications

So far, this chapter has described only the audio portion of the multimedia equation. True multimedia tools, though, provide more than audio playback or recording; these tools also provide video playback or recording. In most cases, AV tools require no special hardware, aside from the sound card, because most AV tools exist to deliver content to end users. In a few cases, such as videoconferencing, you need to connect a digital camera to get the full benefit of such tools. Unfortunately, FreeBSD's support for such hardware is still embryonic, so this chapter focuses upon audio/video playback tools. These often exist as stand-alone programs, but AV files are often found on the Web (movie trailers on film sites, for instance), so linking players to a web browser is sometimes an important task to accomplish.

# ## Audio/Video File Formats

As you browse the Web or obtain AV files, you may notice that they come in several different formats. Some of these formats are well supported in FreeBSD, but others aren't. The most popular formats are

+   ■ **AC-3, aka ATSC A/52** This encoding method is used mainly with digital television signals and DVDs. FreeBSD supports it through the liba52 project (http://liba52.sourceforge.net).

+   ■ **MPEG-1 and MPEG-2** *The Moving Picture Experts Group (MPEG)* has released several file formats. (In fact, the popular MP3 audio file format originates with this group.) The MPEG-1 and MPEG-2 formats are popular for distributing computer AV files. The libmpeg2 (http://libmpeg2.sourceforge.net) and MPEG Audio Decoder (http://www.mars.org/home/rob/proj/mpeg/) projects provide support for these file formats in FreeBSD.

+   ■ **RealVideo** This popular format was developed by RealNetworks (http://www.real.com) as a video streaming format. It's related to the RealAudio format that's also used by RealNetworks. This file format