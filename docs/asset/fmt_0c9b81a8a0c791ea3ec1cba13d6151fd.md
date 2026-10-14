
一旦你安装了音频转换器，你可以通过选择“应用程序”->“声音”来执行它。要添加你想要的文件，点击“添加文件”（`Add File`）选择你想要转换的文件。如果你已经有了这些文件，点击“添加目录”（`Add Directory`）选择它们。这将显示音频转换器的主对话框，如图 16-48 所示。

### 图 16-48

启动音频转换

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_653_0.png)

### 图 16-49

待转换的文件

# Chapter 16: Working with Multimedia

## FIGURE 16-45

Playing Internet radio in Rhythmbox

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_650_0.png)

To subscribe to a podcast, right-click the Podcast entry in the Rhythmbox Source pane, and select "New Podcast" from the pop-up menu. A dialog appears in which you can enter the URL of the podcast you are interested in. Click `Add` to add that to your list of current Podcast feeds, as shown in Figure 16-46.

You can then click on the Podcast entry to show all of your Podcast feeds, and download any available podcast by right-clicking on an available podcast and clicking "Download episode" from the pop-up menu. Once a podcast has downloaded, you can listen to it by simply double-clicking its name.

You can customize where your downloaded podcasts are stored and the frequency with which Rhythmbox looks for new podcasts by selecting the `Edit Preferences` command and clicking the Podcast tab. This displays the dialog shown in Figure 16-47, which enables you to update those settings.

# Part II: Ubuntu for Desktop Users

## FIGURE 16-46

Downloading and playing podcasts in Rhythmbox

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_651_0.png)

10 episodes, 164.9 MB

## FIGURE 16-47

Customizing podcast settings in Rhythmbox

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_651_1.png)

# Chapter 16: Working with Multimedia

## Converting Audio Formats

It's almost inevitable that you'll eventually get some music from free downloads, off the Internet, or after ripping it from your CDs, only to find that it isn't in "right" format for some other purpose. The best examples of these are things like:

- Ripping CDs into Ogg Vorbis format and then wanting to play them on an iPod, which can play Ogg files
- Downloading live concert recordings in FLAC format, only to find that this format is not usable with iPod (and probably never be because of the size of the FLAC files)
- Wanting to create "greatest hits" CD for your car, only to find that you can't create a playable audio CD from MP3, Ogg, or FLAC files

Regardless of which format you can't use, it's irritating to have music that you can play on your desktop system but not in portable music players, CDs and so on. The problem that these examples expose is the fact that specific devices and types of media require specific audio formats. Apple's iPod can only play files in MP3 or Apple's own formats; audio CDs must convert WAV files; and so on. cd-burning applications like `Brasero` and `k3b` will automatically convert files to the WAV format that when burning CDs, but do so on the fly. If you actually want to convert audio files that you already have so that you can permanently use them in some other format?

Luckily Ubuntu provides a great solution to these sorts of problems with the Sound Converter application. As the names imply, this application's sole function is to convert digital audio files from one to another.

Because not everyone is using their Ubuntu system for serious audio work, Sound Converter isn't installed by default. You must install Sound Converter yourself to use your favorite Package Management application as discussed in Chapter 19.

### Tip

Sound Converter uses the Gstreamer Framework discussed earlier in this chapter in the section on "Configuring the Gstreamer Plug-ins. You must follow the instructions in that section before trying to use Sound Converter—at least before to successfully use Sound Converter."
