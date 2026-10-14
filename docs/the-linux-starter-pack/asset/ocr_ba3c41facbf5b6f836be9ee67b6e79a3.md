# Extras

# Codecs and extras

Convert your Linux installation into a multimedia powerhouse, and add extras for a better internet experience.

Out of the box, Ubuntu Linux provides a fine computing experience for general internet and office jobs. However, it’s missing a handful of features to make it an all-round desktop OS – but we can soon fix that. Why is it missing these? Well, Ubuntu Linux is a free operating system, built with components that anybody can modify and share. Consequently it doesn’t include software packages which are non-redistributable or commercially limited, such as Adobe Flash Player. This is a bit annoying at first, as you’ll have seen if you’ve tried to go YouTube, but it doesn’t take long to rectify.

Another aspect to this is multimedia playback. Unfortunately, many of the codecs (file format reading programs) which we use on a day-to-day basis are encumbered with copyright and software patent issues. To avoid getting on the wrong side of media companies, Ubuntu Linux (and the DVD with this magazine) doesn’t include MP3 and DVD playback as standard, but again, these facilities are just a few mouse clicks and commands away. Over the next few pages we’ll show you how to spruce up your Linux machine so that it plays all the media you use every day.

# Playing video DVDs

As mentioned before, DVD playback support is hindered on Ubuntu Linux straight after installation. There are various issues with copyright and software patents surrounding the technology to decode encrypted video DVDs (that is, right on every video DVD around), so the Ubuntu Linux team errs on the side of caution and doesn’t include it. However, if you want

> VLC is arguably the best media player in the world, and it handles DVDs with ease.

![](bbox=[0.1, 0.63, 0.63, 0.92])

to add support to play back DVDs, here’s what you need to do (internet connection required).

First, open a command-line window by clicking Applications, Accessories and Terminal. Don’t worry – we’re not going to do anything complicated! In fact, it’s easiest this way, instead of faffing around in the Synaptic package manager. Enter this command exactly (it’s case-sensitive):

```
sudo apt-get install libdvdread3
```

You will be prompted to enter your password; then the libdvdread3 package, which provides access to encrypted DVDs, will be downloaded and installed. The whole process will take a minute or two. Next we need to enter a second command to activate the decoder:

```
sudo /usr/share/doc/libdvdread3/install-css.sh
```

Lastly, we want to install the VLC media player, an excellent program that’s much better than the default Totem media player for watching DVDs. Enter:

```
sudo apt-get install vlc
```

This will download about 7MB of files, so you’ll have to be patient if you’re on a slow connection. When it’s done, you can enter a movie DVD, and close Totem if it automatically appears. Then click on the Applications menu, and go to Sound & Video > VLC Media Player. Click the Play button at the top, which will open a dialog box to choose the movie you want to play. Click on the Disc tab at the top of the window, then click on OK.

All being well, you’ll now be able to watch your film! Any time you want to watch a movie in future, follow the same process: launch VLC, click the Play button, open the disc and you’re off. Also note that VLC is capable of playing many other types of video file, so if you have problems loading anything in Totem, give it a go.

![](bbox=[0.545, 0.25, 0.89, 0.46])