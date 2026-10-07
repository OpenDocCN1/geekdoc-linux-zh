
# Post-Installation Configuration

- Pointer and Keyboard Configuration .................................................... 89
    - Configuring Keyboards with Linux ............................................................ 89
    - Configuring Pointing Devices in Red Hat Linux ................................ 93
- Configuring Display Graphics ................................................................... 98
    - Configuring Sound Devices ....................................................................... 100
    - Using Loadable Kernel Modules to Start Sound Device ... 101
    - Configuring a New Sound Card ................................................................ 102
- Detecting and Configuring a Modem ........................................................ 104
    - Configuring a Serial-Port Modem ..................................................... 104
    - Configuring a Fax Modem ........................................................................ 107
    - Configuring minicom for Modem Use ................................................... 107
    - Configuring Controllerless Modems for Laptops ............................... 108
- Configuring Power-Management in Red Hat Linux ................................ 108
    - Resetting the Data and Time ....................................................................... 111
    - Using the Date Command ........................................................................ 112
    - Using the hwclock Command ................................................................ 112
    - Using the redhat-config-date Client ................................................ 113
- Managing PCMCIA ................................................................................. 114
    - Using PCMCIA ....................................................................................... 114
    - Controlling PCMCIA Service ................................................................ 116
- Configuring and Using CD, DVD, and CDRW Drives ............................ 116
    - Checking Drive Assignment ................................................................... 116
    - Initializing IEEE 1394 CD Drives ................................................ 118
- Troubleshooting Post-Installation Configuration Problems ................... 121
- Reference .............................................................................................. 123

- First Steps with Linux ................................................................ 125
- Working with the Red Hat Linux File System ........................................ 126
    - Viewing the Red Hat Linux File System ......................................... 127
    - Use Essential Commands from the /bin and /sbin Directories ................... 129
    - Store the Booted Kernel and View Stored Devices in the /boot and /dev Directories ................................................................... 129
    - Use and Edit Files in the /etc Directory ................................................... 130
    - Protect the Contents of User Directories—/home ................................... 133
    - Use the Contents of the /proc Directory to Interact with the Kernel ..................................................................................... 134
    - Work with Shared Data in the /usr Directory ................................... 135
- Temporary File Storage in the /tmp Directory ................................................................ 135
- Access Variable Data Files in the /var Directory ....................................................... 136
- Logging into and Working with Linux .......................................................................... 136
- Text-based Console Login ...................................................................................... 136
- Working with Virtual Consoles ............................................................................ 137
- Using Simple Keyboard and Mouse Techniques in the Linux .....................................
- Console Session ................................................................................................... 138
- Logging Out ....................................................................................................... 139
- Logging In and Out from a Remote Console ................................................... 140
- Changing Your User Information ....................................................................... 142
- Reading Documentation ....................................................................................... 143
- Using man Pages ................................................................................................ 144
- Finding and Reading Software Packages Documentation ................................ 144
- Using the Shell ................................................................................................ 145
- Using Environment Variables ................................................................... 146
- Navigating and Searching with the Shell ................................................... 149
- Managing Files with the Shell ....................................................................... 150
- Compressing and Decompressing Files Through the Shell ........................ 151
- Using the Text Editors ....................................................................... 152
- Working with vi .................................................................................. 153
- Working with emacs .................................................................................. 154
- Working with Permissions ................................................................... 156
- Assigning Permissions ...................................................................... 157
- Directory Permissions ................................................................... 158
- Understanding Set User ID (SUID) and Set Group ID (GUID) .....................
- Permissions ................................................................................... 160
- Working as root ............................................................................ 161
- Creating Users .......................................................................... 162
- Deleting Users ....................................................... 163
- Shutting Down the System ..................................................... 164
- Rebooting the System ................................................................... 165
- Reference .................................................................................. 165

# 6 The X Window System ........................................................ 167

- Basic X Concepts .......................................................................... 168
- Using XFree86 ................................................................ 169
- Elements of the XF86Config File ................................ 170
- Configuring X ................................................................... 175

# Contents

# Starting X

- Using a Display Manager ................................................... 192
- Starting X from the Console by Using startx ................. 195
- Selecting and Using X Window Managers ................................ 196
- Using Red Hat's switchdesk ....................................................... 197
- The Tab Window Manager (twm) ......................................... 198
- The Motif Window Manager (mwm) ........................................ 199
- The sawfish Window Manager ............................................ 199
- The Window Maker Window Manager (wmaker) ................... 201
- GNOME and KDE Desktop Environments ................................ 202
- GNOME: The GNU Network Object Model Environment ........... 202
- KDE: The K Desktop Environment ....................................... 204
- References ..................................................................... 206

# II System Administration

## 7 Managing Services ............................................................ 209
- Understanding the Red Hat Linux Boot Process ................... 210
- Beginning the Boot Loading Process ...................................... 210
- Loading the Linux Kernel ....................................................... 211
- Red Hat Runlevels ................................................................ 212
    - Runlevel Definitions ........................................................ 212
    - Booting into the Default Runlevel ....................................... 213
    - Booting to a Non-Default Runlevel with GRUB ................... 216
- Init Scripts and the Final Stage of Initialization ............... 217
- Controlling Services at Boot with Administrative Tools ... 218
- Using the chconfig-1q Text-Based Command-Line Tool ........ 219
- Using the GUI-Based Service Configuration Tool ............ 221
- Starting and Stopping Services Manually ................... 222
- Changing Runlevels ............................................................ 223
- Using Service Management to Troubleshoot Problems in ... 224
Red Hat Linux ................................................................... 226

## 8 Managing Software and System Resources ........... 227

- Using RPM for Software Management ...................... 227
    - Command-Line and Graphical RPM Clients ................. 229
    - Using RPM on the Command Line ................................ 231
    - Package Organization with rpm ................................... 234
