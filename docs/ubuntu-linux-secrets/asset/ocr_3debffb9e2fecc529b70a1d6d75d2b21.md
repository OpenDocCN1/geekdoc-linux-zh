It wasn’t all that long ago that sound on a computer just meant a series of beeps and blips coming out of a tiny computer speaker. Over the past few years the computer world has exploded with audio features. From playing and extracting songs on a CD to listening to streaming radio stations on a web site, there are plenty of reasons to have audio software on your workstation. Ubuntu doesn’t disappoint the audiophile with its basic installation packages. Plenty of audio features are built into Ubuntu, and you can download additional packages to provide even more audio features. This chapter walks through the basics of using your Ubuntu workstation to process audio files and CDs.

# Audio File Basics

Before diving into the software packages, it’s a good idea to first cover some of the basics of the open-source audio world. Unfortunately, the audio world is full of legal and ethical issues that cause problems for the open-source software enthusiast. You’ll need to know what to expect, or you might be disappointed.

First, let’s take a quick look at the popular audio file formats used on computers, portable music players, and the Internet. These formats are shown in Table 11-1.

| Extension | Name | Description |
|---|---|---|
| .aac | Advanced audio coding | An ISO standard audio compression format made popular as the default format for Apple iPod music players |
| .flac | Free lossless audio codec | An open-source, lossless audio format that doesn’t use compression |
| .ogg | Ogg Vorbis | An open-source audio compression format equivalent to MP3 compression and quality |
| .mp3 | MPEG-1 audio layer 3 | A patented audio compression format requiring licensing rights |
| .wav | Waveform audio format | A Microsoft and IBM standard for uncompressed audio |
| .wma | Windows media audio | A proprietary audio compression format created by Microsoft and controlled by strict licensing requirements |


For each specific audio file format, Ubuntu must use software that can play the audio file. These programs are called codecs. Each codec specializes in a specific audio file format. Ubuntu includes codecs for the FLAC, OGG, and WAV audio file formats by default. There are reasons why it doesn’t contain codecs for the others by default.

By far the most controversial audio file format is MP3. Despite the widespread popularity of the MP3 audio format (or maybe because of it), MP3 has been the subject of numerous legal battles over the past few years based on patent infringement. Because of this legal problem, many Linux distributions shy away from supporting MP3 files by default.