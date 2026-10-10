This chapter covers utilities that enable you to process sound and graphic files. These utilities can make disk-based recordings of CD-ROM audio tracks, play MP3 and MIDI audio files, translate virtually any type of computer graphic file into another graphic format, and much more.

> TIP Some of the commands discussed in this chapter are not installed by default with most Linux distributions. See the Introduction for information on obtaining these commands by downloading them from the Internet.

# AT A GLANCE

| How Do I | See This Entry | Example |
|---|---|---|
| Convert a graphic file from one format to another? | **convert** | `convert jpeg image1.bmp image1.jpg` |
| Create a thumbnail index of all the graphic files in the working directory? | **convert** | `convert \`vid:*\.jpg\` catalog.jpg` |
| Create a printed jewel case label for a CD-ROM that I've just burned? | **cdlabelgen** | `cdlabelgen -c \`My Favorites\` -s \`2000\` -i \`Blues%Jazz%Rock%Alternative Rock%Techno%Indust rial\` -e images/mp3.eps > cover.ps` |
| Play an audio CD-ROM? | **cdp** | `cdp` |
| Make WAV recordings of all the audio tracks on an audio CD-ROM? | **cdparanoia** | `cdparanoia -B \`1\` |