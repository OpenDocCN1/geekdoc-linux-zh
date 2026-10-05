
# WHAT IS LINUX?

(the C compiler), the quality of the installation and configuration tools, the available support, accompanying manuals, and so on.

All distributions can be used internationally (assuming a basic knowledge of the English language). Some distributions, however, excel through particular consideration of national language peculiarities, thus saving the user a lot of configuration effort and hassle. Also, the value of a language manual should not be under-estimated.

Competition between many distributions may provide a push to their further development, but it also creates upheaval with the installation of programs not supplied together with the distribution (and, in particular, with commercial programs). A missing or obsolete program library is often the cause of a program not running. For Linux novices it is practically impossible to remedy such problems. Some software manufacturers even go far as to offer support of their products only when it is used together with a specific distribution (Obviously, each manufacturer chooses a different distribution ...)

To eliminate problems, the Linux Standard Base (LSB) was called into existence, which is supposed to define the smallest common denominator for future LSB-conformant distributions:

```
http://www.linuxbase.org
```

Servers on CD-ROM, which are released by many Linux vendors every two or three months, should not be confused with distributions. A server mirror is a copy of all Linux-specific files from Internet servers with Linux software. Server mirrors do not contain distributions; instead, you will find the most-to-date versions of all sorts of Linux application programs (normally as single archive files with their source code).

But don't be hoodwink by the low cost of server mirrors: installing the programs requires manual work and presumes a certain knowledge of Linux. Beginners are better off with distributions where installation is easily carried out by preconfigured packages. Server mirrors are addressed to experienced Linux users who need the latest versions of Linux programs and online documentation, but have no access to the Internet (or are reluctant to pay all those Telecom charges).

# Some current Linux distributions

The following overview of the most available distributions (in alphabetical order and without claiming to be exhaustive) sets out to provide a general orientation in the field.

## Caldera

Caldera Open Linux is a successful attempt to create a Linux distribution for professional users. (Meanwhile, however, many competitors make the same claim.) Depending on the distribution variation, Caldera excels through various commercial add-ons, in particular excellent support of Novell network functions.

## Debian

While most distributions are put together by companies whose main aim is to make financial gains out of their distributions, Debian is a true exception; this distribution is put together by committed Linux users who put great emphasis on stability and adherence to the rules of ‘free' software. Several concepts of this distribution – such as the professional package administration – have set standards for other distributions and are still at the forefront in several aspects (Just try to update your distribution without restarting your computer!). During the past years, Debian has become increasingly more user-friendly; however, for Linux novices this distribution is still not suitable because of its difficult package administration program.

## RedHat

The RedHat distribution is among the best maintained distributions currently available. This distribution dominates the American market especially. The package administration on the basis of the rpm format (a proprietary development of Red-Hat) has now been adopted by many other distributions. RedHat Linux is available, in largely uniform outfit, for several processor platforms (Intel, DEC Alpha, Sun Sparc). Besides the RedHat distribution, there are a number of derived distributions providing various improvements, language adaptations (such as a Spanish distribution), additional components (KDE), and so on.

## Slackware

Slackware was (after the SLS distribution which is currently no longer up to date) one of the first available Linux distributions. With regard to maintenance and ease of installation, however, the currently up-to-date Slackware can no longer keep pace with many other distributions.

## SuSE

Thanks to its high topicality, the huge number of preconfigured packages, the comprehensive manual, and the excellent maintenance, SuSE Linux (Gesellschaft für Software Systementwicklung) has become the most widely used Linux distribution in Europe. However, SuSE Linux is also available with English-language menus and manuals. The vast administration tool not only helps with (nearly) all configuration problems (including ISDN configuration) but, similarly to Debian, also automatically solves dependency problems which may occur during package installation.

## TurboLinux

This distribution, put together by Pacific HighTech (PHT), has been specially optimized for use in Japan and has the market leader there. The distribution is also available in an English version.

## Minimal distributions

Besides these large distributions, you will find some collections of miniature systems (down to a complete Linux system on a single diskette!) on the Internet. These distributions are mostly based on (and therefore smaller) kernel versions, which are particularly designed for special tasks, such as maintenance work (emergency system) or to be able to use a Linux system without a proper installation (straight from one or more diskettes). This is if you need to run Linux regularly on a foreign computer whose hard disk you do not wish (or are not allowed) to repartition.

![](img/b30873dd3d753687a59253fb9ad26a0b_41_0.png)

A reasonably complete list of the most varied Linux distributions (no matter whether of commercial or other origin) can be found on the Internet:

```
http://www.linuxqh.com/dist-index.html
```

However, you should also browse through the various computer magazines which frequently carry out comparative tests between distributions and which are obviously more detailed and up to date than this book could hope to be. An overview of some current distributions can also be found in the HOWTO text on distributions – see page 77.

After working on this book, however, I stick to my previous conclusion that life would be wonderful if one could only combine the advantages of all distributions without having to cope with their disadvantages!

# The origin of Linux

This section is concerned not with further details on Linux, but with questions such as: does Linux exist at all? How has the system been developed? Why is it free? In this, GNU (GNU is not Unix) and the FSF (Free Software Foundation) play an important role.

Linux is a very young operating system. The very first kernel parts (version 0.01) were developed by Linux Torvalds (Helsinki) on his own. He released the program code in September 1991 over the Internet. Within a very short time, programmers worldwide became interested in the idea and started programming extensions for it: a better file management system, drivers for various hardware components, additional programs, such as the DOS emulator, and so on. All of these components were also made available free of charge, and the entire system grew with breathtaking speed. A new operating system would never have been produced in this way without worldwide communication between programmers via the Internet.

One of the main reasons why Linux, although not containing items by the big software houses, could nevertheless be developed so quickly, lies in the software which was freely available at that point in time. Linux has not emerged from nowhere, as is times wrongly argued, but is based on a platform of free software. Minix provided the practical base for the first steps, software which was free though fairly limited in its functionality. Thus, the first Linux versions still used the Minix file system.

Even more important was (and still is) the great number of GNU programs. GNU programs have been around for much longer than Linux. On many Unix systems, GNU programs were already used as better substitutes for original components – for example, the GNU C compiler, the GNU Emacs (text editor), var-
