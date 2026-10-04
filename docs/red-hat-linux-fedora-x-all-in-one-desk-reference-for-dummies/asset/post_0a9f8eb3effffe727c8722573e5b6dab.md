
+ 7. When you're done downloading the photos, right-click the camera icon on the GNOME desktop and choose Unmount Volume from the pop-up menu.

Linux unmounts the camera from the /mnt/camera directory, removes the /mnt/camera directory, and removes the line that was added to the /etc/fstab file.

+ 8. Power off the camera and disconnect the USB cable from the PC.

Who needs gtcam when you can access the camera just like any other storage device!

# Playing audio CDs

Both GNOME and KDE come with CD player applications. To play an audio CD, you need a sound card, and that sound card must be configured to work in Linux.

If you are using the GNOME desktop, you can play audio CDs by using the GNOME CD Player application. Launch the GNOME CD Player by selecting Main Menu→Sound & Video→CD Player. Figure 4-2 shows this CD player playing a track from an audio CD.

![](img/d9230b719dc0efd80851f363d8c6f571_212_0.png)

The GNOME CD Player displays the title of the CD and the name of the current track. freedb.org. The GNOME CD Player gets the songs from freedb.org — a free-source CD database on the Internet (freedb.freed.org at port 888). You need an active Internet connection for the CD Player to download song information from the CD database. After the CD Player downloads information about a particular CD, it caches that information in a local database for future use. The CD Player's user interface is intuitive, and you can learn it easily. One nice feature is that you can select a track by title, as shown in Figure 4-3.

If you use KDE as your desktop, you find a similar audio CD player in KDE. Start the CD player by selecting Main Menu→Sound & Video→KsCD.

# Multimedia Applications 187

![](img/d9230b719dc0efd80851f363d8c6f571_213_0.png)

Figure 4-3:
In the
GNOME CD
Player, you
select
a specific
audio track
to play.

Book II
Chapter 4
Core Applications
Exploring Fedora

# Playing sound files

You can use Rhythmbox or XMMS to open and play a sound file. Users with large MP3 music libraries like Rhythmbox, but the version that comes with Fedora Core does not include the MP3 capability. XMMS is not installed by default, but you can install it from the companion DVD by following these steps while logged in root:

+ 1. Mount this book's companion DVD.

Insert the DVD into the DVD drive and type mount /mnt/cdrom in a terminal window (you may have to change cdrom to cdrom1, if the DVD drive is the second CD/DVD drive on your system).

+ 2. Install the XMMS RPM.

Type the following commands from a terminal window (these commands assume that the DVD drive is mounted on /mnt/cdrom):

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh xmms*
```

XMMS can play many types of sound files, including Ogg Vorbis, FLAC (Free Lossless Audio Codec, an audio format that is similar to MP3), and Windows WAV. You can play many WAV sound files — which usually have names that end with the .wav extension — in the /usr/share/sounds directory of your Linux system.

# 188 Multimedia Applications

You can also create WAV sound files from audio CD tracks by using the cda2wav command-line audio. For example, to convert the second track from an audio CD into a WAV file, type the following:

```
cda2wav -D /dev/cdrom -t2 -Owav
```

cda2wav saves the track in a WAV file named audio.wav. You can play the WAV file in XMMS. Watch out though—each of an audio CD typically takes about 60MB of disk space in wav format.

Because of legal reasons, the version of XMMS in Fedora Core does not include the code to play MP3 files, so you must translate MP3s into a supported format such as WAV before you play them. You can use the Ogg Vorbis format for compressed audio files because Ogg Vorbis is a patent-and royalty-free format.

To start XMMS from the GNOME or KDE desktop, choose Main Menu:Sound:Audio Player. XMMS has a simple user interface. To open a sound file, choose Window Menu:Play or press L to select a .wav or .ogg file from the Load dialog box. Select a file and click OK. XMMS plays the sound file. Figure 4-4 shows a typical XMMS window when it's playing a sound file.

Media Player
You can play different types of sound files in XMMS.

![](img/d9230b719dc0efd80851f363d8c6f571_214_0.png)

If you get an error message from XMMS, choose Window Menu:Options:Preferences and select ALSA as the Output Plugin.

Of course, many music files are in MP3 format. Getting to XMMS to play MP3 music would be nice? Well, to play MP3 files in XMMS, you have to download the source code for XMMS and build it from scratch. I provide the instructions in Book VI, Chapter 4.

# Burning a CD

Fedora Core includes X-CD-Roast, a graphical CD burner application with a lot of features. It can create both data CDs and audio CDs. You can also rip

(copy) music from audio CDs to files on the hard drive and burn them onto a new audio CD. In the next sections, I briefly explain how to use X-CDRoast. If you want to find out more, visit www.xdcroast.org.

X-CDRoast is on this book's companion DVD, but it is not installed by default. To install X-CDRoast, follow these steps while you are logged in as root:

# 1. Mount this book's companion DVD.

Insert the DVD into the DVD drive and type /mnt/cdrom in a terminal window (you may have to change cdrom to cdrom1, if the drive is the second CD/DVD drive on your system).

# 2. Install the xcdroast RPM.

Type the following commands from a terminal window (assume that the drive is mounted on /mnt/cdrom):

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh xcdroast*
```

X-CDRoast depends on many external programs to do its job. If these programs do not exist, some X-CDRoast features don't work. Although most programs are used by X-CDRoast with Fedora Core, a few are not part of the Fedora Core distribution. For example, X-CDRoast needs the mpg123 program to convert MP3 audio files into a form suitable for recording on CD. Fedora Core does not come with the mpg123 program, so you can't create audio CDs that include MP3 songs.

Before you can burn a CD, you need a CD-R or CD-RW drive (CD burner) connected to your PC. It can be an internal or external CD burner. Internal CD burners are usually IDE (also known as ATAPI) devices connected to the same card that powers the PC's hard disk and any other CD drive.

If you have an external CD/DVD drive, probably connects to your PC's USB port. When you connect a burner to the USB port and power it up, Linux automatically recognizes the device. If you use a CD-R/RW drive, X-Roast automatically detects CD/DVD drives. You can, however, manually identify CD/DVD drives that X-Roast fails to detect.

To start X-CDRoast, choose Main Menu;System;CD Writer from the GNOME or KDE desktop (the KDE menu appears only after you install the xcdroast RPM). If you aren't logged in as root, you're prompted for the root password. X-Roast scans for CD/DVD devices and displays the results in a dialog box. Click OK to proceed. X-Roast gives you an opportunity to configure the software so that

![](img/d9230b719dc0efd80851f363d8c6f571_215_0.png)

![](img/d9230b719dc0efd80851f363d8c6f571_215_1.png)

Book II
Chapter 4
Core Applications
Exploring Fedora

# 190 Multimedia Applications

any user can activate it (this feature is called Non-Root Mode). If you want to get right on burning CDs, click Launch X-Roast and the main window appears, as shown in Figure 4-5. You can do everything — configure X-Roast and burn audio and data CDs — from the main window.

**Figure 4-5:** You can burn CDs from the X-Roast main window.

![](img/d9230b719dc0efd80851f363d8c6f571_216_0.png)

# Exploring the Setup window

If this is your first time with X-Roast, click Setup from the main menu (refer to Figure 4-5). X-Roast displays the Setup window (shown in Figure 4-6) with six tabs.

Initially, X-Roast displays the Device-Scan tab with list of CD/DVD devices it detects (shown in Figure 4-6). You also have to set up other parameters through the remaining tabs:

- CD: Enables you to specify the CD reading and writing speeds, the default CD writer device, the primary and secondary CD device (if you have multiple CD drives). You can also specify the CD writing mode. The default CD writing mode is Disk-At-Once (DAO). If this mode fails, try Track-At-Once (TAO) that puts a 2-second pause after each track, but that's supported by every CD writer.
- HD Settings: Specify the directory for temporary storage of CD images. Click the Browse button and select the directory you want. You could, for example, select the /tmp directory for temporary storage. After selecting the directory, click the Add button.
