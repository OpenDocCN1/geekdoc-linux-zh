
## 3 Installing the X Window System 63
- History 64
- Installing the X Window System 64
- Configuring the X Window System 66
- SaX 66
- XF86Setup 71
- xf86config 76
- Setting Up XDM/KDM 79
- Setting Up Frame Buffer Device
- X Server 80
- X Display Tips 81
- Tip #1: Adding Hosts to the Access Control List 81
- Tip #2: Exporting the DISPLAY Environment Variable 82
- Tip #3: Starting X Programs on Other Servers and Exporting the DISPLAY Variable to Your X Server 82
- Troubleshooting the X Window System 82

## II System Administration 85

## 4 Managing Users and Groups 87
- Linux: A Multiuser Operating System 88
- What Is an Account? 88
- Working with Users 89
- Adding New Users 89
- Modifying a User 91
- Deleting a User 91
- Disabling a User's Account 92
- Working with Groups 92
- Creating a Group 93
- Modifying a Group 94
- Deleting a Group 95
- Managing Home Directories 95
- Setting Global Preferences for Your Users 95
- Protecting Home Directories 96
- Controlling Your Users 96
- Controlling the System Resources Available to Users 97
- Controlling How Much Hard Disk Space Your Users Are Allowed to Have (Quota) 99
- Troubleshooting 104

## 5 Managing Filesystems 107
- Understanding Filesystems 108
- Mounting and Unmounting Filesystems 109
- Understanding /etc/fstab 111
- Creating and Formatting Filesystems 113
- Formatting a New Drive or Partition 113
- Creating a New Swap Partition 114
- Checking Your Filesystem 115
- Understanding the Network Filesystem 116
- Preparing to Use NFS 116
- Using NFS (Client-Side) 117
- Using NFS (Server-Side) 118
- Troubleshooting 118

## 6 Backing Up the System 121
- Backup, Backup, Backup 122
- Software Requirements 122
- What You Should Back Up 122
- Planning a Backup Strategy 123
- The Backup Drawing Board 124
- Back Up Using YaST 124
- Invoking the YaST Backup Module 125
- Selecting Directories 125
- Restoring Files 127
- Using cpio to Back Up Your Files 128
- Out Mode 128
- In Mode 128
- Other Backup Software 128

## 7 System Upgrade 131
Upgrading Your Linux 132
Precautions Prior to Package Installations 132
Upgrading SuSE Linux 133
Installing New Packages from Your Hard Disk 133
Updating SuSE Using the Internet 135
Upgrading Your X Window System 136
Obtaining the Latest Version of X Windows from SuSE 137
Obtaining X Windows and Installing It 137
Installing X Windows from Source 138
Upgrading Your KDE 140
Checking Your KDE Version 140
Checking for a New Version of KDE 140
Getting the Latest KDE from kde.org 142
Compiling KDE 144
Upgrading GNOME 145
Checking Your Version of GNOME 145
Obtaining the Latest Version of GNOME 146
Upgrading GNOME from Source 150
Installing a New Library 151
Upgrading an Existing Library 152
Upgrading Your glibc 153
Upgrading Your GCC 154
Troubleshooting 155

## 8 Installing a New Kernel 157
Defining the Kernel 158
Why Should I Install a New Kernel? 158
Installing a Precompiled Kernel Versus Compiling Your Own 158
Installing a Precompiled Kernel 159
Installing from SuSE CDs 159
Downloading a Precompiled Kernel from the Internet 160
Installing a Kernel from Source Code 162
Reading Kernel Versions 162
Checking Your Kernel's Version 163
Checking for the Latest Version of the Kernel 163
Kernel Compilation Checklist 164
Downloading and Unpacking a New Kernel 164
Unpacking the Kernel Source 165
Upgrading the Kernel Using a Patch 166
SuSE Specific Changes 167
Configuring Your Kernel 167
Kernel Configuration/ Compilation Quick Start 167
Running the Graphical Kernel Configuration Utility 168
Running the Text Menu-Based Kernel Configuration Utility 170
Running the Text-Based Kernel Configuration Utility 172
Testing a Kernel Before Installing It 173
Getting to Know the Various Important Configuration Parameters 175
Code Maturity Level Options 175
Processor Type and Features 175
Loadable Modules Support 176
General Setup 176
Plug-and-Play Support 177
Block Devices 177
Networking Options 177
SCSI Support 178
Network Device Support 178
Amateur Radio Support 178
IrDA Subsystem Support 178
ISDN Subsystem 178
Old CD-ROM Drivers (not SCSI, not IDE) 178
Character Devices 179
Video for Linux 179
Joystick Support 179
Filesystems 179
Network Filesystems 180
Sound 181
Kernel Hacking 181
Behind the Scenes 181
Troubleshooting 182

## 9 Configuring the System Boot Up Sequence 185
Understanding the Boot Up Process 186
The Linux Loader 186
Configuring LILO 186
Using YaST to Configure LILO 187
Advanced LILO 191
Uninstalling and Reinstalling LILO 193
LILO Error Interpretation 194
init and Runlevels 195
init Scripts 195
Runlevels 196
Booting to a Different Runlevel Using LILO 198
Modifying the Runlevels 198
Adding Your Own Script to the init Scripts 198
Troubleshooting 200

## 10 Sound Card Configuration 201
Linux and Sound: A Brief History 202
What SuSE Linux Offers 202
Software Requirements 203
Setting Up Hardware 204
Searching for the Proper Resources 204
Configuring Your Card to Use the Proper Resources 205
Configuration of OSS/Lite 210
Kernel Configuration and Sound Cards 210
What Kernel Configuration Do I Need For My Sound Card? 210
Editing the Modules Configuration File 211
Testing the Sound Configuration 213
Troubleshooting OSS/Lite 214
Configuration of OSS 215
Software Requirements 215
Installing OSS 215
The Modules Configuration Problem 217
Activating OSS on Boot-Up 218
Troubleshooting OSS 218
Configuration of ALSA 218
What Do You Need to Install ALSA? 218
Installing ALSA Using the Sources 218
Configuring ALSA Using alsaconf 219
Checking if ALSA Works 221
Configuring ALSA to Start on System Boot Up 221
Some Useful ALSA Utilities 221
Troubleshooting ALSA 222
Enlightenment Sound Daemon (ESD) 222
Installing ESD 223
Other Programs to Control ESD 223
Environment Variables That Can Be Used with ESD 224

## 11 Printing 225
Selecting a Printer for Linux 226
Printing from Linux 226
Printing to a Printer Connected to Your Machine 226
Printing to a Remote UNIX Printer 230
Printing to a Remote Microsoft Windows Printer 232
Printing to a Remote Printer Over a Novell Network 233
Allowing Others to Share Your Local Printer 234
Allowing Other UNIX/Linux Machines to Use Your Printer 235
Allowing Other Microsoft Machines to Use Your Printer 235
Crash Course on Using the Linux Printing Commands 236
Troubleshooting 238

## 12 Configuring Peripherals 241
CD-ROM, CR-R, CD-RW, and DVD 242
CD-ROM Drives 242
Zip/Jaz Drives 250
Zip Drive 250
SCSI Zip and Jaz Drives 253
Crash Course in Zip/Jaz Tools 254
Joysticks and Gamepads 255
Fax 256
Configuring HylaFax 257
Configuring SuseFax 258
Scanners 261
TV Cards 263
Troubleshooting 264

## III Network Configuration 267

## 13 Configuring a TCP/IP Network 269
Networking in SuSE Linux 270
Understanding TCP/IP Networking 270
What You Need to Know to Get Connected 271
Using YaST to Configure Your Network 272
Upgrading or Changing Your Network Card 277
Network-Related Configuration Files 278
Securing Your Network Using a Firewall 278
Installing the Firewall 279
Configuring the Firewall 280
Saving Your Firewall Rules 283
Crash Course in iptables Command-Line Arguments 283
Troubleshooting 284

## 14 Configuring Domain Name Service 285
A Briefing on Domain Name Service 286
Internet History 286
DNS History 286
Configuring the Resolver 288
What the Configuration Files Are 289
Setting Up the Domain Name Server 291
Software Requirements 291
BIND Configuration 291
Configuration Files 292
Setting Up a Caching Only Name Server 295
Setting Up the Server 295
Using the Caching Only Name Server 296
A Simple Domain Configuration 297
Your Role 299
Troubleshooting BIND 299
