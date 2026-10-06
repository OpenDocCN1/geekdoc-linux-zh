
![](img/d35fa962e6f9664d66dc83916f426418_296_0.png)

![](img/d35fa962e6f9664d66dc83916f426418_296_1.png)

## Amping Up with PLUG

The guitar players among you, particularly those of you with Fender Mustang amplifiers (I–IV), will be disappointed to learn that Fender’s software normally comes with your amp is not compatible with Linux. The good news is an answer in the form of the application PLUG (Figure 14-16). Like Fuse, PLUG can be used to create and edit amplifier presets and upload them to your amplifier. Using PLUG is like creating and modifying your own pedal, just virtually rather than on the floor in front of you. You can also apply firmware updates for your amplifier via PLUG.

![](img/d35fa962e6f9664d66dc83916f426418_297_0.png)

Figure 14-14: Editing and creating Mustang presets with PLUG

PLUG is not available via the Ubuntu Software Center, but it is easily downloadable as a binary that you just found. Get PLUG from the project website at http://piplank.org/plug/download/ and download the Generic package for 32-bit systems. This is a binary tarball, so you won't be installing it but rather extracting and running it from your Home folder, as you did with some of the apps you worked with in Chapter 8. Once the tarball is downloaded, extract it to the LocalApps folder you created in Chapter 8 (or wherever you prefer). To run it, double-click the PLUG file within the folder it came in and then click RUN in the dialog that appears.

Before PLUG can recognize your amplifier, you'll have to do a little work to get around the fact that Ubuntu allows only root users to access unknown USB devices, which your amp will be. The instructions on how to do this can be found in the README file in the PLUG folder.

## Hydrogen & Mix

Before wrapping things up, I'll briefly mention a couple of applications that deserve mention if for no reason other than are pretty cool at what they do. One is Hydrogen (Figure 14-17), which is a digital drum machine for Linux. It aims to provide, as the project page puts it, "professional yet simple and intuitive pattern-based drum programming." The other is Mixx (Figure 14-18), a cross-platform, full-featured digital dual-deck mixer.

![](img/d35fa962e6f9664d66dc83916f426418_298_0.png)

Figure 14-17: Hydrogen, a digital drum machine

![](img/d35fa962e6f9664d66dc83916f426418_298_1.png)

Figure 14-18: Mixx, a cross-platform DJ mixer

# 15

## PLUGGIN' IN THE PENGUIN

*Working with Your iPod, iPhone, and Other Digital Media Devices*

![](img/d35fa962e6f9664d66dc83916f426418_300_0.png)

With all the talk in the previous chapter about ripping, encoding, and playing back audio files, you may be wondering whether Ubuntu will allow you to transfer any of those files to your digital media devices, such as your MP3 player, cell phone, or iPad. Well, you will be happy to know that using your device with your Ubuntu system is quite easy—easier than ever, in fact. No longer do you have to mess around with mount and unmount commands or edit system tables, and if you don't know what I'm talking about, consider yourself lucky. Just plug in your device, and Ubuntu will do the rest.

## Knowing Your Limits

Assuming Ubuntu helped you download and install all the audio codecs and support files for the applications mentioned in Chapter 14, you shouldn't encounter any problems handling any media files on your digital media device. Even if you didn't install those codecs and files, Ubuntu will automatically help you find the necessary items if you try to play a file it hasn't installed for. Not all formats will work with equal degrees of comfort or success—it depends on your device and the file format compatibility with Ubuntu. As a general rule of thumb, most players will be able to handle MP3 files and unlocked AAC (.m4a). Check your device's manual for specifics about other file formats (or give them a try).

As far Ubuntu goes, it can work with all the files mentioned—with the exception of locked AAC files. And you will learn a way to deal with them later in the chapter.

> Although working with your digital media devices in Ubuntu has becoming increasingly simple, it's always worth a bit of caution. Make sure to have backups of the device before working with it on Ubuntu.

## Mounting and Ejecting Your iPod, iPhone, or iPad

Working with your iPod, iPhone, or iPad is extremely simple. Basically, just connect the device to your computer via a USB connector, and Ubuntu will mount the device so you can access it. An icon for your device and another for Documents will then appear in the left pane of any file manager you have happened to open. Ubuntu will also place icons for your device and Documents in the Launcher.

In addition, two of those-do-you-want-to-do-with-this-stuff types of displays will appear. (These are the same kind of displays that show up when you insert a music CD or DVD into your drive or connect a digital camera to your machine via USB cable.) You'll see one for music and podcasts and one for photos (Figure 15-1), and they'll usually be stacked directly above the other. You can select Rhythmbox for music-handling chords in the other and Shotwell for photo handling in the other. Then click OK in each window to work with your device through these two applications. Or you can just close both of those windows for now and then open Rhythmbox or Shotwell, or both, later on clicking the icon for your device in the left pane and then clicking either of the two buttons that appear in the file manager window for your device

To “eject” your iPhone or other “i” device, click the eject button next to the icon for your device.

![](img/d35fa962e6f9664d66dc83916f426418_302_0.png)

![](img/d35fa962e6f9664d66dc83916f426418_302_1.png)

![](img/d35fa962e6f9664d66dc83916f426418_302_2.png)

Figure 15-1: Ubuntu instantly recognizes your iPod, iPhone

Figure 15-2: Launching Rhythmbox and Shotwell for working with audio and image files

Figure 15-3: Disabling the auto-update function on your device

## (Not) Auto-updating your iPod or iPhone

With the simple instructions as how to use your iPod or iPhone out of the way, it's worth thinking about a couple of other things. Most important of these is the device's auto-updating settings. When you enable auto-update on your iPod or iPhone via iTunes, the function is set up within the device. You can use your iPod on Windows, Mac, or Linux—or all of them interchangeably. If you set up your iPod to auto-update songs and playlists, however, you are leaving yourself open for trouble unless you have exactly the same music collection on all of your machines.

Here’s why: iTunes allows you to add files to your iPod, it does not allow you to copy files from it. The auto-update feature is strictly a one-way street. This means that whenever you hook up your auto-update-enabled iPod to an iTunes-enabled computer, iTunes will automatically add the tracks in your library to your iPod—so far, More frighteningly, it will remove any tracks from your iPod that are not present in that's iTunes library. I learned this hard way when I took my ex wife's loaded iPod to work and plugged it into my office Windows with its empty iTunes library. I brought the Podster back to her with nothing at all, well... what wasn't pretty.

Make sure to disable your iPod's auto-update function before bringing the device into the Linux world. To do this, connect your iPod to your Mac or Windows machine and open iTunes. In the left pane of the iTunes in the Devices section, and then the right pane, check the box to Manually manage music (Manually manage music and videos in video-capable iPods), as shown in Figure 15-3. Next, if you have a photo-capable device, repeat nearly the same process for your photos by clicking the Photos tab in the right pane and unchecking the box to Sync photos.

## Working with Android-Based Devices

Although the iPhone continues to be the king of the smartphone hill, phones and tablets running Google’s Android operating system are starting to give Apple a run for its money. Fortunately, working with any
