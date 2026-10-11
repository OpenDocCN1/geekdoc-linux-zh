# Kodi: Media made easy

Kodi – formerly known as XBMC – is an awesome way to bring Linux right into your living room.

# Quick tip

If you use Kodi via OSMC, it can also be used as a hotspot for other devices or wireless extender. Under internet settings you can turn a wired connection into an extra hotspot, or if Kodi connects to your router wirelessly, you can extend the connection through an ethernet port to a device that doesn't have wireless built-in.

There are plenty of great media players available for Linux, capable of finding, organising and accessing your digital media library wherever it is on your hard drive or around the house. But the ultimate media player, which turns your PC into a set-top box, is Kodi. Originally developed for the XBox (and formerly known as Xbox Media Center), Kodi is an application that puts digital media into a "10 foot interface" for viewing with a remote on large TV. It's truly cross platform – there are versions of Kodi available for Windows or macOS, but Linux is its spiritual home.

Kodi is brilliant. It can be used to playback digital media, and can also play CDs, DVDs, Blu-ray discs and more, plus it has an extensive library of add-ons put together by fans that will access online resources like streaming BBC iPlayer or any one of a number of TV channels from around the world – including some high profile sports ones – and online archives of favourite TV shows, like South Park.

It also works with most DVB-T cards so you can watch live TV or turn your PC into a PVR system capable of recording shows for playback later.

# Getting Kodi

Kodi isn't available in the standard Ubuntu repositories. To install it on your current machine, you'll need to open up a terminal and add the Kodi repository. Press [Alt]+[Ctrl]+[T] to open a terminal and type:

```
sudo apt-add-repository ppa:team-xbmc/ppa
sudo apt-get update
sudo apt-get install kodi
```

Kodi is a small download, only around 75MB in its latest release form. After installing it, you'll notice by default Kodi runs in full screen mode with no obvious way to get back to the desktop. Don't panic, just remember that it's designed for use on a big screen and ideally aimed at a media centre machine with a single purpose – not as a replacement for Rhythmbox and Totem.

+   - Kodi has dozens of add-ons in its repositories, many of which allow access to content they probably shouldn't.

To get back to the desktop, simply click the power button and select Exit. To run Kodi in a window, go to System > Settings > System and click the Video Output tab. From here, you can then change the Display Mode to Windowed or Full Screen.

You can see from the above example that Kodi's main weakness is that some of the menus are a little over complicated. The upside is that it's highly customisable: you can tweak lots of settings from subtitles to the kind of hardware accelerated decoding you prefer in the menus, so be careful not to change anything you don't fully understand.

Because Kodi is intended for use on a dedicated media centre/set-top box machine, you'll find several disk images at the Kodi.tv website. These are customised operating systems (usually based on Ubuntu) that will boot a machine straight into Kodi, and have most desktop apps removed for maximum stability.

There are images of Kodi operating systems for non-traditional PCs too, like the Raspberry Pi (the best is OSMC) and there's an Android app too. The latter means it is available for dedicated devices like the Amazon Fire TV, which plugs into a spare HDMI port on your TV.

# Getting started

Importing a media library into Kodi is fairly straightforward. Click on Videos, then Files and select "Add Videos". This will bring up a file browser so you can point Kodi at the place where your videos are stored. If it search through folders, so you can add a whole drive, but it will add all clips in the folder/drive selected. It's best, therefore, to point it at a dedicated video library where you want a screen full of short clips sent via an instant messaging app or in your browser history.

The file browser isn't especially intuitive for newcomers if you're not used to the way Linux is organised under the hood. To find a hard drive other than the one your operating system is installed on, you'll need to go to Browse > Root file system > Media and find your drive, for example. The good news is that it's easy to add the contents of remote storage using the UPNP search tool in this same menu.

Adding music to your Kodi library is the same process from the Music tab on the homepage.

There's some really good news if you've got a large library of digital files built up over many years, with lots of different naming conventions and file type too. By default, Kodi will automatically cross reference files with online databases of TV shows and movies. That means it will display information about a show or film, and correctly number episodes and display the correct titles too.

![](bbox=[0.22, 0.77, 0.53, 0.92])