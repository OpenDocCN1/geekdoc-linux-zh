
### Playing Sound Files
- **Playing sound files:** Use Rhythmbox or XMMS multimedia audio players. (You have to download some additional software to play MP3 files with Rhythmbox or XMMS.) You can also download other players from the Internet.
- **Burning a CD:** Use a CD burner, such as K3b, to burn audio and data CDs.

## Using a Digital Camera

Most Linux distributions come with a digital camera application that you can use to download pictures from digital cameras. For example, MEPIS, SUSE, and Xandros come with digiKam, which works with many different makes and models of digital cameras. Depending on the model, the cameras can connect to the serial port or the Universal Serial Bus (USB) port.

To use digiKam with your digital camera, follow these steps:

1. **Connect your digital camera to the serial port or USB port (whichever interface the camera supports) and turn on the camera.**
    Look for it in the Main Menu under graphics or images.
2. **Start digiKam.**
3. **From the digiKam menu, choose Settings→Configure digiKam.**
    A configuration dialog box appears.
4. **Click the Cameras tab in the dialog box and click Auto Detect.**
    If your camera is supported and the camera is configured to be in PTP (Picture Transfer Protocol) mode, the camera is detected. If not, you can get the photos from your camera by using an alternate method that I describe after these steps.
5. **Choose your camera model from the Camera menu.**
    A new window appears, and after a short while, displays the photos in the camera.
6. **Click the thumbnails to select the images you want to download; then choose Camera→Download to download the images.**

digiKam then downloads the images. You can save the file in a folder and edit the photos in The GIMP or your favorite photo editor.

![](img/11709a8f88c8cd03868a929dc94c0e2b_254_0.png)

Don’t despair if digiKam doesn’t recognize your digital camera. You can still access the digital camera’s storage media (compact flash card, for example) as a USB mass storage device, provided your camera supports USB Mass Storage. To access the images on your USB digital camera, use the following steps. (I tested these steps on SUSE Linux, but they should work on most Linux distributions.)

1. Read the camera manual and use the menu options of the camera to set the USB mode to Mass Storage.
    If the camera doesn't support USB Mass Storage, you cannot use this procedure to access the photos. If the camera supports the Picture Transfer Protocol mode, you can use digiKam to download the pictures.
2. Connect your digital camera to the USB port by using the cable that came with the camera and then turn on the camera.
    This causes Linux to detect the camera and open the contents of the camera in a file manager window (see Figure 4-6).

![](img/11709a8f88c8cd03868a929dc94c0e2b_255_0.png)

3. Click to select photos and copy them to your hard drive by dragging and dropping them into a selected folder.
4. Close the file manager window, disconnect the USB cable from the PC, and turn off the camera.

Who needs a digital camera tool when you can access the camera just like any other storage device!

## Playing Audio CDs

All Linux distributions come with either the GNOME or KDE CD player applications. To play an audio CD, you need a sound card, and that sound card must be configured to work in Linux.

In some distributions, you can insert an audio CD into the drive, and a dialog box appears and asks whether you want to play the CD player. For example, Figure 4-7 shows the KDE CD player (KsCD) playing a track from an audio CD in SUSE Linux.

![](img/11709a8f88c8cd03868a929dc94c0e2b_256_0.png)

The KDE CD player displays the title of the CD and the name of the current track. The CD player gets the song titles from http://freedb.org — a free, open source CD database on the Internet (freedb.freedb.org at port 888). You need an active Internet connection for the CD player to download song information from the CD database. After the CD player downloads information about a particular CD, it caches that information in a local database for future use. The CD player user interface is intuitive, and you can figure it out easily. One nice feature is that you can select a track by title.

## Playing Sound Files

You can use Rhythmbox or XMMS to open and play sound files (for example, MP3 files). Users with large MP3 music libraries like Rhythmbox because it can help organize the music files. You can start Rhythmbox by choosing the music player application from the Main Menu in several distributions, including Debian and Fedora Core. When you first start Rhythmbox, it displays an assistant that prompts you (see Figure 4-8) for the location of your music files so that Rhythmbox can manage your music library.

![](img/11709a8f88c8cd03868a929dc94c0e2b_256_1.png)

After you identify the locations of music files, Rhythmbox starts and displays the library in an organized manner. You can then select music and play it, as shown in Figure 4-9. (Here you see Rhythmbox running on Debian.)

# 232 Multimedia Applications

![](img/11709a8f88c8cd03868a929dc94c0e2b_257_0.png)

**Figure 4-9**: You can play music from your library in Rhythmbox.

XMMS is another music player that can play many types of sound files, including Ogg Vorbis, FLAC (Free Lossless Audio Codec, an audio file format that is similar to MP3), and Windows WAV.

You can start XMMS by choosing the audio player application from the Main Menu (look under Multimedia or Sound & Video). After XMMS starts, you can open a sound file (such as an MP3 file) by choosing Window Menu->Play File or by pressing L. Then select one or more music files from the Load File dialog box. Click the Play button, and XMMS starts playing the sound file. Figure 4-10 shows the XMMS window (in SUSE Linux) when it's playing a sound file.

![](img/11709a8f88c8cd03868a929dc94c0e2b_257_1.png)

**Figure 4-10**: You can play many different types of sound files in XMMS.

## Burning a CD

Nowadays, GUI file managers often have the capability to burn CDs. For example, Nautilus and Xandros File Manager have built-in features to burn CDs. Linux distributions also come with standalone GUI programs that enable you to easily burn CDs and DVDs. For example, K3b is a popular CD/DVD burning application for KDE that's available in Knoppix and SUSE.

Most CD burning applications are simple to use. You basically gather up the files that you want to burn to the CD or DVD and then start the burning process. Of course, for this to work, your PC must have a CD or DVD burner installed.

Figure 4-11 shows the initial window of the K3b CD/DVD burning application in SUSE Linux. The upper part of the K3b window is for browsing the file system to select what you want to burn onto a CD or DVD. The upper-left corner shows the CD writer device installed; in this example, it's a DVD/CD-RW drive so that the drive can read DVDs and CDs, but burn CDs only.

![](img/11709a8f88c8cd03868a929dc94c0e2b_258_0.png)

**Figure 4-11:** You can burn CDs and DVDs with the K3b application.

To burn a CD, you start with one of the projects shown in the lower part of the K3b window — New Audio CD Project, for example, or New Data DVD Project. Then you have to add files and finally, burn the project to the CD or DVD by choosing Project->Burn or pressing Ctrl-B. For an audio CD, you can drag and drop MP3 files as well as audio tracks.

![](img/11709a8f88c8cd03868a929dc94c0e2b_259_0.png)

K3b needs the external command-line programs cdrecord and cdrdao to burn CDs. K3b also needs the growisofs program to burn DVDs.

![](img/11709a8f88c8cd03868a929dc94c0e2b_259_1.png)

If you get an error about missing cdrdao in Debian, make sure that your Debian system is connected to the Internet and then type `apt-get install cdrdao` to install it.

# Graphics and Imaging

You can use graphics and imaging applications to work with images and graphics (line drawings and shapes). I discuss two applications:

- The GIMP (GNU Image Manipulation Program) is a program for viewing and performing image-manipulation tasks, such as photo retouching, image compositing, and image creation.
- Gnome Ghostview (GGV) is a graphical application capable of displaying PostScript files.

## The GIMP

The GIMP is an image-manipulation program written by Peter Mattis and Spencer Kimball and released under the GNU General Public License (GPL). Most Linux distributions come with this program, although you may have to specifically select a package to install it. The GIMP is comparable to other image-manipulation programs, such as Adobe Photoshop and Corel PHOTO-PAINT.

To try out The GIMP, look for it under the Graphics category in the Main Menu. When you start it, The GIMP displays a window with copyright and license information. Click the Continue button to proceed with the installation. The next screen shows the directories to be created when you proceed with a personal installation of The GIMP.

The GIMP installation involves creating a directory in your home directory and placing a number of files in that directory. This directory essentially holds information about any changes to user preferences you may make to The GIMP. Go ahead and click the Continue button at the bottom of the
