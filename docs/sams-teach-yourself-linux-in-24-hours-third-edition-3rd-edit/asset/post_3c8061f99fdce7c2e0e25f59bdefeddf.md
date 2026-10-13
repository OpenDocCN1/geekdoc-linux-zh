
Another fun way to waste some time is to play one of the xemacs text adventure games. Dungeon is shown in Figure 23.9 (the menu choice is Dunnet). To play these games, the computer will tell you part of a story and then you need to tell the computer what you want to do next. In Dungeon, you need to navigate around an angry bear.

Tell the computer where to go.

### Figure 23.9
Text adventure games can be more challenging than their video counterparts.

![](img/782ecfdc0b083a767896cc983e10427f_363_0.png)

## Play DOS and Windows Games on Linux

It's not an easy job to get a DOS or Windows program to work on an unfamiliar operating system, but there is some help. Linux can use two different emulators to run some of your games. For your DOS games, try dosemu (the DOS emulator); for your Windows games, try wine (the Windows emulator).

To run dosemu on a Linux system, a version of DOS must be installed (it does not have to be MS-DOS, if you prefer). This emulator is only designed for DOS programs; Windows-compatible programs might not run under dosemu. To learn more about dosemu, visit www.dosemu.org. You might first want to start with the dosemu FAQ (located at www.dosemu.org/docs/HOWTO).

The Wine Development Headquarters (at www.winehq.com) lists a number of resources that you can use to find out how to run a program developed for the Windows operating system under Linux. To find out whether an application will run under wine, check out the wine application database at www.winehq.com/Apps/query.cgi. To read some success stories from people who have had success running Windows-compatible games under Linux, head over to www.linuxgames.com/wine.

## Summary

Every Linux distribution includes an assortment of games. The source for many of the games is X.org, the originators of the X Window System. There are also other games available from other UNIX distributions. The BSD games collection is included with the Slackware and Debian distributions. The Linux-Mandrake distribution uses the collection distributed with Red Hat Linux. Of course, it's all Linux and, no matter which distribution you have, you can obtain the games from any distribution's CD-ROM or Web site.

## Q&A

Q Could you recommend some good Linux gaming sites on the Internet?

A Here's our best list:

If you're looking for strict downloads, try the MetaLab Linux Archives at metalab.unc.edu/pub/Linux/games/INDEX.html.

The Linux Game Tome at www.happypenguin.org, has hundreds of games available for download. There's also news about new games and a database that can be searched by game name, type, or release date.

The Linux Portal site at www.linuxlinks.com/Software/Games also has hundreds of games available for download. Games are organized by categories and you'll find links to a game's Web site.

If commercial games are your gig, there are quite a few of your favorite Windows-compatible games that are now running on the Linux operating system and benefiting from the increased performance advantages of Linux. If your interest leans toward the popular Quake and Doom games, head over to www.linuxgames.com.

This site keeps current on the daily Linux game news and contains links to other gaming sites. You can download game packages as RPM files that can be installed easily with Gnome-RPM or KPackage. You'll also find information on wine, an ongoing Windows emulator development which may enable you to run your Windows games under Linux. The Turbolinux distribution includes vmware, which seems to work well with Windows applications.

Of course, you can always go to the FTP site for your favorite Linux distribution and see what is offered. Don't forget to give your favorite Internet search engine a task and do some prospecting on your own.

Q I have a joystick attached to my Windows machine and I'd like to use it on my Linux system. Where can I find out whether my game hardware will work with Linux?

A You'll find information about joysticks in the Linux Hardware HOWTO at www.linuxdoc.org/HOWTO/Hardware-HOWTO.html. If you have any USB peripherals, you'll find information about using USB devices at www.linux-usb.org.

## Workshop

Test your knowledge of the material covered in this hour by answering the following questions and working through the exercises.

## Quiz

+   1. Where should you look if you want to find out which games are installed on your system?
+   The easiest place to look is in the menu system for the various desktop environments. In KDE and GNOME, games are found in the Amusements menu. Another place to look is in the /usr/games directory. This directory contains mostly console games. To do a complete search of the installed games, use a package manager (such as KPackage or Gnome-RPM) to list the installed programs.
+   
+   2. If you install additional games on the system, in which directory should they be located?
+   User-installed games should be placed in the /usr/local/games directory. The /usr/games directory is only for the BSD games and other games that are installed when you installed the Linux operating system.
+   
+   3. If you don't know how a program operates, how can you find out?
+   The first place to look is the manual pages. If there isn't a manual page for a game, open the game and see whether there is a Help menu.
+   
+   4. Is it possible to play DOS games and games designed for the Windows operating system on a Linux system?
+   Yes, it is possible but not always easy. There are two different emulators that enable you to play some of these games on Linux. DOS games might be able to run under dosemu and Windows-compatible games might run under wine. A third option is the vmware package bundled with TurboLinux.

## Exercises

+   1. Get on the Internet and hunt for more educational games. Don't worry, your brain is a big place and it will take you a long time to fill it up. There is no such thing as too much education.
+   2. For some additional fun and enjoyment, get out and enjoy the sunshine. Outdoor activities are as good for the brain and body as the educational games.

![](img/782ecfdc0b083a767896cc983e10427f_368_0.png)

## Hour 24

## The Home Entertainment System

You've made it to the final hour and now it's time to sit back, relax, and enjoy some entertainment. Besides some cool games, Linux also has quite a multimedia lineup. You'll find everything from music players to video players to graphics programs.

In this hour, you will
- Play music CDs on your computer
- Watch a video
- Find some fun drawing and graphics programs

## Playing Music CDs

One way to drown out the background noise while you are trying to work is to pop a music CD into the CD-ROM drive of your Linux system and play some of your favorite albums. You'll find several CD players in each Linux distribution. Table 24.1 lists a number of CD players that may be installed on your system and the command to execute the player.

### Table 24.1 Select a CD Player

| CD Player | Execution Command |
|---|---|
| GNOME CD player | gtcd |
| Grip CD player and ripper | grip |
| KDE CD player | kscd |
| X window CD player | xplaycd |
| Text mode CD player | cdp |

Probably the easiest CD players to use and the ones installed with most every distribution are the GNOME CD player and the KDE CD player. The GNOME CD player (shown in Figure 24.1) is the electronic version of the CD player on your home stereo system, with a few added attractions.

### Figure 24.1
Use the GNOME CD player to play your favorite music CDs.

![](img/782ecfdc0b083a767896cc983e10427f_369_0.png)

The KDE CD player (shown in Figure 24.2) works in much the same way as the GNOME CD player with a few added bells and whistles. To play a CD in either of these players, start the CD player, pop a music CD into the CD-ROM drive, and press the Play button. You'll hear the first song on the CD and the track number will appear in the LED display.

### Figure 24.2
The KDE CD player is another easy-to-use CD player.

![](img/782ecfdc0b083a767896cc983e10427f_369_1.png)
