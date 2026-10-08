
## Part III: Linux, Huh! What Is It Good For? Absolutely Everything!

![](img/8c094d1b36276212c03d10d898508a6e_173_0.png)

**Figure 11-4:** The GNOME Toaster window.

## Chapter 12

## Live from the Net

### In This Chapter

- Using XMMS to listen to Internet audio streams
- Listening to live radio and playing DVDs with MPlayer

One of the great innovations of recent times is the use of the Internet to transmit — stream — audio and video programs. Streaming technology provides the ability for anyone to create a radio or TV station unlimited in terms of geography and governmental approval; it also can be done inexpensively. Using streaming technology, computer users can listen to or view those broadcasts from anywhere.

This chapter describes how to use your Red Hat Linux machine as both an audio radio receiver and a DVD video player. We use the open source XMMS and MPlayer applications to listen to the Net.

### Using the XMMS Audio Player

The open source XMMS (X MultiMedia System) application is a great tool for listening to audio streams and files. XMMS plays .wav files produced by `grtp` / `cdparanoia` by default. It also plays the up-and-coming open source Ogg/Vorbis format (codec).

The Ogg codec doesn't use any proprietary or patented algorithms. Ogg is free for anyone to use, and people and organizations that don't want to depend on proprietary systems are discovering it; Ogg also produces higher-fidelity audio streams than other popular systems, such as MP3. Why depend on another corporation's whims when you don't have to?

![](img/8c094d1b36276212c03d10d898508a6e_175_0.png)

You can use XMMS to listen to some of the music you may have saved in Chapter 11. If you used $grip$ to save music to your home directory and you want to listen to it, open XMMS and right-click the window. Choose Open $\rightarrow$ File and select any of the WAV files you created.

![](img/8c094d1b36276212c03d10d898508a6e_175_1.png)

$Ogg$ is the system used to format audio streams, and Vorbis is used to compress formatted audio streams. Unlike most other technological systems, Ogg/Vorbis isn't an acronym but rather is named after science fiction characters. For more information about Ogg/Vorbis and similar open source multimedia systems, go to www.vorbis.com.

Now that you have a bit of technological background, you can start using XMMS to listen to Ogg/Vorbis streams:

1. **Log in to your computer and open Mozilla** by clicking the blue globe icon in the GNOME Panel. Enter the address www.vorbis.com/music.psp in the Mozilla text box.
2. **Click any of the Track links.** For example, click the first one, Lepidoptera. The Downloading Epoc-Lepidoptera.ogg dialog box opens.
3. **Click the OK button and then the Save button.** The Enter the Name of File to Save to window opens, and Mozilla saves the music file to your home directory.
4. **Start XMMS by clicking the GNOME Menu and choosing Sound & Video $\rightarrow$ Audio Player.** An XMMS window opens. Figure 12-1 shows the player.
5. **Right-click the XMMS window, choose Play File, and click the filename you just saved to disk.** When you click the OK button, XMMS starts playing the music.

![](img/8c094d1b36276212c03d10d898508a6e_175_2.png)

![](img/8c094d1b36276212c03d10d898508a6e_175_3.png)

The Vorbis Web page provides links to other Ogg-capable sources. For example, click the Music Sites Page link, near the top of the www.vorbis.com/music.psp page. You see a page with links to other sources. For example, click the WCPE link to go to a Web page that streams classical music.

Now is a good time to describe how to configure Mozilla to automatically start XMMS whenever you click Ogg/Vorbis sources and streams:

1. **Log in and open Mozilla and then click the Edit::Preferences menu.** The Preferences window opens.
2. **Choose Navigator::Helper Applications.** The Helpers Applications subwindow opens in the Preferences window. Red Hat has added a MIME (Multipurpose Internet Mail Extensions) entry for Ogg, which is displayed as `application/x-ogg` in the File types subwindow.
3. **Click application/x-ogg and then the Edit button.** The Edit Type dialog box opens, displaying the information that it knows how to handle the Ogg-formatted media. Figure 12-2 shows the completed Edit Type dialog box.

   This list describes the various fields:
   - **MIME type:** The MIME type associated with the helper application. If you have read Chapter 10, you know that MIME types help your computer decide how to handle different media formats and types. Enter `audio/x-ogg` in this field.
   - **Description:** Any short text describing the MIME type.
   - **Extension:** The file type extension in this field. In this case, Ogg files use the `ogg` extension.
   - **When a file of this type is encountered:** What you want to do with the stream when the MIME type is encountered. You can choose to use the default application, which in this case is XMMS; specify an application to use; or save the information to disk as a file.
   - **Always ask me before handling files of this type:** Forces Mozilla to prompt you before doing anything with the MIME type.

4. Click the **Open it With** button and enter `/usr/bin/xmms` in the text box.
5. Click the **OK** button in the **Edit Type** dialog box to return to the **Preferences** window.
6. Click the **OK** button in the **Preferences** window to return to **Mozilla**.

![](img/8c094d1b36276212c03d10d898508a6e_177_0.png)

Mozilla now launches XMMS whenever you click a link to an Ogg/Vorbis source. XMMS starts and connects and then plays the stream.

![](img/8c094d1b36276212c03d10d898508a6e_177_1.png)

XMMS uses the Enlightened Sound Daemon (esd) process by default to access your computer's speakers. Designed to allow multiple audio players to simultaneously use your computer's speakers, esd sometimes gets confused and you have to restart it. Log in as root, open a GNOME Terminal window, and run the command `killall -HUP esd`. If that doesn't work, you can configure XMMS to use another output system. Right-click the XMMS window and choose Options $\rightarrow$ Preferences. Click the Output Plug-in subwindow and select the OSS Driver 1.2.7 plug-in. Click the Apply button and then the OK button.

### Using the Fabulous MPlayer

Whenever a desperate need exists, the Superman — err — the open source movement, comes in to save the day. Until recently, you couldn't use any single Linux application to listen to and view most popular streaming formats. Now, MPlayer has burst on the scene and fills that gap.

MPlayer can play most popular (and many obscure) audio and video streaming formats. Although it's under intense development, it's still technically in the beta development phase. However, MPlayer is quite usable, and we think that you should consider using it. We do!

This list shows some streaming formats MPlayer can play:

- MPEG-1/Layer 3 (MP3): MP3 is a popular but proprietary codec used for both storing and streaming audio.
- Ogg/Vorbis: This new up-and-coming open source streaming format is unencumbered by any copyrights or patents, like other formats are.
- Microsoft Media Server (MMS): You can listen to radio broadcasts that use the popular MMS format with MPlayer. Previously, you needed to use the Microsoft client to listen to MMS streams.
- Digital Versatile Disc (DVD): You can play DVDs from your computer with MPlayer.
- RealAudio: You need to download, compile, and install the RTSP package to use RealAudio.

MPlayer is not now included in the Red Hat Linux distribution. We hope that it will be later, but for now you have to obtain it from its developers. These steps describe how to download, install, and use MPlayer:

1. Log in, open Mozilla, and go to `www.mplayerhq.hu/homepage/download.html`.
2. Click the latest Red Hat RPM version. At the time this book was written, the latest Red Hat RPMS was found in the MPlayer Red Hat 7.x RPM packages. The 7.x packages work on Red Hat 10 systems.
3. Download each of these packages:
   - `mplayer`
   - `mplayer-common`
   - `mplayer-gui`
   - `mplayer-skins`
   - and this font package: `MPlayerISO-8859-1-font`
   
   At the time this edition of the book was written, the most recent MPlayer RPM package was version 0.92. You may see — and should use — the most recent version available.
4. Open a GNOME Terminal window and change to root:
   ```
   su -
   ```
   Enter the root password when prompted.
5. Install the package:
   ```
   rpm -ivh --nodeps mplayer*
   ```
