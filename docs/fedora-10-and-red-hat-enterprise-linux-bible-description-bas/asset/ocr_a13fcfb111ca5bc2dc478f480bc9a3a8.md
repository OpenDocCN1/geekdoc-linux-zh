# Chapter 8: Music, Video, and Images in Linux 309

yourself. For example, you can purchase codecs for non-free audio and video content, such as MPEG4 video, Windows Media, and others.

A company called Fluendo (http://www.fluendo.com), which is responsible for the Gstreamer multimedia framework in Fedora, purchased an unlimited MP3 license that allows you to download the Fluendo MP3 Decoder for free, to play your MP3 audio files. You can pay a small fee to get audio/video codecs such as Dolby AC3 Audio Decoder, Windows Media MMS Network Streamer Reader, MPEG4 Part 2 Video Decoder. Read the licensing agreement that you appear before you download it. Unlike software that comes with Fedora, you cannot freely redistribute the codecs you get from Fluendo.

# Listening to Music in Linux

Good-quality sound hardware is considered a necessity for today's desktop and laptop systems. While playing songs downloaded from the Internet, sound tracks to digital movies, or audio from a TV card, any user-friendly operating system has to support a healthy list of sound hardware and audio applications.

Most popular sound devices for the PC, whether on separate cards or built into your computer's motherboard, will be automatically detected when a Fedora or RHEL system boots. Appropriate modules will be loaded, so you can immediately begin using your sound card.

Beginning with Fedora 8, PulseAudio (http://www.pulseaudio.org) became the default sound system with Fedora, taking over spot from Advanced Linux Sound Architecture (ALSA). PulseAudio basically provides the interfaces between audio applications and your sound card. A major improvement over other audio systems is that it allows you to control volume levels separately for different applications. Also, by incorporating plug-ins, PulseAudio lets you use audio applications that were designed for ALSA.

To control playback volumes and audio input and output devices, the pulseaudio package includes the PulseAudio Volume Control. The alsa-utils RMP package contains the commands and configuration files you can use to tune your sound card and adjust audio levels. Other friendly graphical tools have been used by the GNOME and KDE projects for managing sound.

After your sound card is working and audio levels are adjusted, you can use any of the dozens of audio applications that come with Linux with your sound card. These applications include music players, video players, video conferencing applications, games, and audio recorders, to a name few.

As for audio content, the following list describes the types of audio content you might want to play, which players can be used for each type of content, and whether or not the software comes with Fedora or RHEL. (If not, I describe where you can get software to play that content and issues associated with getting and using that.)