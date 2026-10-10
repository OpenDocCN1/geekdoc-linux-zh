
## Acknowledgments

A special acknowledgment goes to the people at Red Hat, Inc. and members of the Fedora Project. In particular, Max Spevack (Fedora Project leader) and Greg DeKoenigsberg (Fedora Community leader) deserve praise for their leadership in producing a consistently high-quality Linux distribution. Special thanks to Jesse Keating (Red Hat release engineer for Fedora) for helping me use his excellent Pungi tools to produce the 8GB Fedora DVD that comes with this book. Also special thanks to the members of the Fedora-marketing-list and Fedora-advisory-board mailing lists who have provided me with insights into the goals and direction of the Fedora project.

At Wiley, I’d like to thank Jenny Watson, Colleen Hauser, and Laura Atkinson for helping work out issues related to the publicity, media, and covers for this book. Thanks to Sara Shlaer for her continued great editing and production work on this book, and for keeping me on schedule so we could bring this book to you on schedule. Tim Boronczyk provided a thorough technical editing pass. Thanks also to Margot Maley Hutchison and the others at Waterside Productions for bringing me this project.

Thanks, as always, to my dear family for helping me through this project. It’s time to party!

Finally, a special thanks goes to those of you who bought this and earlier editions of *Red Hat Linux Bible*. Go out and become a force for Linux in your work, home, and community. If you feel like expanding your Linux horizons, try some of these other books I’ve written:

- *Linux Bible 2008 Edition* — Contains 16 different bootable and installable Linux distributions on DVD and CD, along with descriptions characterizing those and other popular and interesting Linux distributions.
- *Fedora Linux Toolbox* with François Cazen — Includes 1000+ command lines to help Fedora, RHEL, and CentOS power users get the most out of Linux. To try other Linux distributions, check out *Ubuntu Linux Toolbox* and *SUSE Linux Toolbox* by the same authors.
- *Linux Troubleshooting Bible* with Thomas Weeks — Goes beyond this book to help you safely deploy and troubleshoot Linux systems.
- *Linux Toys II* — If you’re looking for something fun to do with Linux, this book contains nine fun projects you can build with a PC and open source software.

## Contents

### Part I: Getting Started in Fedora and RHEL

**Chapter 1: An Overview of Fedora and Red Hat Enterprise Linux** .................................................................3
- Introducing Fedora 8 and Red Hat Enterprise Linux 4
- What Is Linux? 5
- Linux's Roots in UNIX 6
- Common Linux Features 8
- Primary Advantages of Linux 10
- What Are Red Hat Enterprise Linux and Fedora? 11
  - Red Hat forms the Fedora Project 11
  - Red Hat shifts to Red Hat Enterprise Linux 14
  - Choosing between Fedora and Enterprise 14
- Why Choose Fedora or Red Hat Enterprise Linux? 15
- New Features in Fedora 8 17
  - Getting custom Fedora spins 18
  - Creating your own spins 19
  - The GNOME Online Desktop 19
  - Infinity look-and-feel and Nodoka theme 19
  - PulseAudio sound system 20
  - Codeina utility for getting codecs 20
  - Package Manager 20
  - IcedTea Java environment 20
  - Firewall Configuration 20
- The Culture of Free Software 20

**Chapter 2: Installing Fedora** ...............................................................................................23
- Understanding Fedora Installation Media 24
- Using the Fedora 8 Live CD 24
- Quick Installation 26
- Detailed Installation Instructions 28
  - Installing Fedora 8 29
  - Choosing an installation method 29
  - Choosing computer hardware 31
  - Installing Fedora on a Laptop 33
- Preparing for installation using the live CD 33
- Beginning the installation 36
- Running Fedora Setup Agent 45
- Going forward after installation 48
- Special Installation Procedures 49
  - Alternatives for starting installation 49
  - Installing from other media 52
  - Starting a VNC install 55
  - Performing a kickstart installation 56
  - Special Installation Topics 61
    - Setting up to dual-boot Linux and Windows 62
    - Partitioning your disks 67
    - Using the GRUB boot loader 75
  - Troubleshooting Installation 81
  - Spinning Your Own Fedora Install or Live Media 83

**Chapter 3: Getting Started with the Desktop** ... 85
- Logging in to Fedora or RHEL 86
- Getting Familiar with the Desktop 88
- Using the GNOME Desktop 97
- Using the Metacity window manager 99
- Using the GNOME panels 101
- Using the Nautilus file manager 106
- Changing GNOME preferences 109
- Managing removable media (CDs, DVD, and cameras) 110
- Trying other GNOME applications 112
- Switching to another user 114
- Exiting GNOME 114
- Setting Up an Online Desktop 115
- Switching Desktop Environments 118
- Using the KDE Desktop 119
  - Starting with KDE 120
  - KDE desktop described 120
  - Managing files with the Konqueror File Manager 123
  - Configuring Konqueror options 128
  - Managing windows 132
  - Configuring the desktop 133
  - Adding application launchers and MIME types 136
- Running 3D Accelerated Desktop Effects 137
- Troubleshooting Your Desktop 140
  - GUI doesn't work at start-up 141
  - Tuning your video card and monitor 142
  - Configuring video cards for gaming 144
  - Getting more information 144

**Chapter 4: Using Linux Commands** ... 147
- The Shell Interface 147
  - Checking your login session 148
  - Checking directories and permissions 149
  - Checking system activity 151
  - Exiting the shell 152
- Understanding the Shell 152
  - Using the Shell in Linux 153
  - Locating commands 154
  - Re-running commands 157
  - Connecting and expanding commands 163
  - Using shell environment variables 166
  - Managing background and foreground processes 169
  - Configuring your shell 172
- Working with the Linux File System 175
  - Creating files and directories 177
  - Moving, copying, and deleting files 184
- Using the vi Text Editor 184
  - Starting with vi 185
  - Moving around the file 188
  - Searching for text 188
  - Using numbers with commands 189

### Part II: Using Fedora and RHEL

**Chapter 5: Accessing and Running Applications** ... 191
- Getting and Installing Software Packages 192
  - Downloading and installing applications with yum 194
  - Getting Fedora and RHEL software updates 201
  - Getting updates with Package Updater 202
- Managing RPM Packages 203
  - Using the Package Manager window 203
  - Using the rpm command 204
- Using Software in Different Formats 215
  - Understanding software package names and formats 215
  - Using different archive and document formats 217
  - Building and installing from source code 219
- Using Fedora or RHEL to Run Applications 222
  - Finding common desktop applications in Linux 224
  - Investigating your desktop 225
  - Starting applications from a menu 226
  - Starting applications from a Run Application window 226
  - Starting applications from a Terminal window 227
  - Running remote X applications 229
- Running Microsoft Windows, DOS, and Macintosh Applications 232
  - Running DOS applications 234
  - Running Microsoft Windows applications in Linux 236
  - Running Macintosh applications with ARDI Executor 242
- Running Applications in Virtual Environments 242
  - Running applications virtually with Xen 243
  - Running applications virtually with KVM and QEMU 247

**Chapter 6: Publishing with Fedora and RHEL** ...251
- Using OpenOffice.org 252
- Other Word Processors 254
  - Using StarOffice 255
  - AbiWord 256
  - Using KOffice 257
- Using Traditional Linux Publishing Tools 258
  - Creating Documents in Groff or LaTeX 259
    - Text processing with Groff 259
    - Text processing with TeX/LaTeX 269
    - Converting documents 272
    - Creating DocBook documents 273
    - Understanding SGML and XML 274
- Printing Documents with Fedora and RHEL 277
  - Printing to the default printer 278
  - Printing from the shell 278
  - Checking the print queues 279
  - Removing print jobs 279
  - Checking printer status 280
- Displaying PDF Files with Adobe Acrobat Reader 280
- Working with Graphics 281
  - Manipulating images with GIMP 282
  - Taking screen captures 283
  - Using Scanners Driven by SANE 284

**Chapter 7: Gaming in Fedora and RHEL** ...287
- Basic Linux Gaming Information 288
  - Where to get information on Linux gaming 288
  - Choosing a video card for gaming 289
- Running Open Source Linux Games 291
  - GNOME games 292
  - KDE games 293
  - Adding more games from Fedora repository 294
- Commercial Linux Games 304
  - Getting Started with commercial games in Linux 305
  - Playing commercial Linux games 305
  - id Software Games 306
  - Gaming with Cedega 308
