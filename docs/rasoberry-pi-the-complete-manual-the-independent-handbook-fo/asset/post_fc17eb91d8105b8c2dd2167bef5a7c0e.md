
## Top four add-on boards

### Getting started

**HiFiBerry DAC+ €30**

As a high-quality audio device, even at a mid price, this is a strong contender. It lacks due to the fact it only has a 4.5mm headphone jack that doesn't sound to be particularly robust, with two RCA ports on the back. The good news is that the clever folk at the HiFiBerry Pi Foundation have provided access to the USB port, which is also handy for powering the device. It features a DAC chip which can output digital audio via an RCA port, and it has a volume control.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_38_0.png)

**Energenie Pi-mote €20**

Home automation is all the rage at the moment, so automating tasks like flicking the lights before you go to bed or turning on our heating makes our lives even easier.

One thing that we've all found is that it's so easy to just turn off devices at the plug rather than leaving them on standby, so they're a bit of an electrocution when we're not using them. That's where the Energenie Pi-mote control starter kit comes in. It contains two remote-controlled plug sockets which can be turned on and off with an RF remote.

What does this have to do with our Raspberry Pi? Well, you can also get an add-on board to enable you to control the sockets via software on the Raspberry Pi, which unleashes some new possibilities – and you could set your lamps to turn on and off automatically at specified times when you are away to deter burglars, or create a basic web app to control your power sockets remotely using your browser.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_38_1.png)

> “The Energenie Pi-mote control starter kit contains two remote-controlled plug sockets which can be turned on and off”

## Back up your Pi

Take the initiative and back up your Raspberry Pi to make sure you never lose files again

While the Raspberry Pi is a very solid piece of kit, failure can happen, so it's best to be well prepared and keep your files safe

The good news is that the Pi's files are all kept externally on the SD card. If your Pi breaks, everything will still be available on the SD card and accessible from elsewhere. The SD card is still susceptible to problems, though. There are a number of ways to back up a Pi. The methods can be broken down into two main categories: saving the important files and creating an exact copy of the state of the SD card. The former involves having copies of files elsewhere, while the latter has you create the same kind of image that you'd normally write to the SD card when installing Raspbian or other Pi operating systems.

### Important files

To save important files, we need to create a copy on an external source, such as external hard drive or another PC. One of the best methods to do this doesn't even involve a Pi: all you need is a PC or laptop with a card reader and you're good to go. Turn off your Pi, unplug it and remove the SD card from the slot. Find the SD card reader on your PC and slot it in. The main file system of the SD card can be read by Linux PCs by default, and a Windows or Mac computer once you have installed a program that lets it read the ext4 file system, such as Ext2Fsd. On Windows, the SD card will be listed with the rest of the drives under My Computer (Fig 1). On Linux and Mac, it will be listed wherever storage is shown on the menus and file managers. Once you've found the SD card on here, open it up and navigate to home and then pi. This is where the Documents, Downloads, Desktop and other directories can be found. All you need to do is select the files you want to copy and move them to a secure directory on your PC or a connected external hard drive.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_39_0.png)

**What you'll need...**
- A second computer
- External storage

> **Did you know...**
>
> SD card controllers (or ‘write-protects’) can be found on some laptops and PCs. This allows you to create a backup on your own files which nobody can delete.

If you want to keep the files on another computer, that's fine, but it will be prone to the exact same problems as the Pi in the long run. Keeping them on an external hard drive is a good idea, and putting them on a cloud storage service is better yet, enabling you to access them from anywhere with an internet connection (Fig 2).

### Cloning

Creating a clone depends on what operating system you're using on your main computer. For Macs and Linux, you can use a simple command-line tool called `dd` to create an exact copy of the SD card (Fig 3). This is done in the terminal emulator or command line, so bring that up first. Make sure the SD card is plugged in and enter:

```
$ ls /dev/sd*
```

This lists all connected storage devices. The SD card will have 2.4 or 8GB of space, depending on its size. It'll likely be listed as something like /dev/sdb, where x is the letter the computer attaches to the SD card. To copy it using dd, enter the following into the terminal:

```
$ dd if=/dev/sdX of=/backup.img bs=512
```

You can also add a path to the image you're creating to put it in a specific folder. The process will take some time, and will produce a multi-gigabyte file which you can then write onto the SD by reversing the previous command:

```
$ dd if=/backup.img of=/dev/sdX bs=512
```

While this is useful as a backup, you can also use the image to mass-produce SD cards to give to friends or keep in the various places where you use your Raspberry Pi.

### Windows

To create a clone on Windows, we can use the Win32 Disk Imager (Fig 4). Download it from here to install it: bit.ly/LBJdYG.

Once installed, insert the SD card and launch the software. Choose a name for the backup file and select the SD card from the list of devices. Now press Read and it will create the backup file. Again, this might take a while; however, this time you can at least shown a progress bar.

Storing your cloned image is a little more difficult than your Important files – the size of the image being in the gigabytes means it will fill up a lot of cloud-storage services. If you have the space, definitely keep it on there; however, you may need to put it on an external hard drive.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_40_0.png)

Fig 1: Accessing the SD card from another PC. It's an easy alternative to transferring files between machines via a USB stick.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_40_1.png)

Fig 2: Cloud storage services make backing up files easy and secure, as they're a lot less prone to problems.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_40_2.png)

Fig 3: The dd tool is what you'll use on a Linux and Mac computer, and it's available by default in the terminal emulator.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_40_3.png)

Fig 4: Win32 Disk Imager makes backing up the entire OS easy, and you can even use it to write the image back to the SD card.

## Projects

### Beginner’s guide to nano

What you’ll need
- **Full nano manual**
- www.nano-editor.org/dist/v1.2nano.1.html

Learn how to edit text on the command line and in a terminal with one of Linux’s best tools

> ### Did you know . . .

If you have the itch to do more with your Pi, one of the skills you’ll need to learn to pull off many projects is the ability to edit system files. The command line text editor nano is definitely one of the best tools for the job. Text editors are very basic tools; the clue is in the name in this case. There’s no formatting or colouring or anything of the sort you would get in a word processor, but that’s the point. The kind of files you’ll be creating or editing will generally contain code – code which doesn’t require to be made bold or bulleted. nano removes all of these distractions, but still has a few of the more handy features you’d find in a graphical text editor. We’ll teach you how to make the most out of nano to make your projects run quickly and efficiently.

![](img/fd3f4a582cf5250916d8b8e1d4ccd045_41_0.png)

- ### Writing
  Create plain text files in the command line, even write some code for a program

- ### Editing
  Edit system files to suit your needs and projects without digging through a file manager

- ### Advanced functions
  Search, copy, paste and insert text from another file using some of the built-in nano functions
