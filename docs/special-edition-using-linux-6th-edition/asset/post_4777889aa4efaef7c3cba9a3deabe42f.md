
- Stopping KDE 39
- KDE Capabilities 40
- Configuring KDE with the Control Center 41
  - Information 43
  - Look & Feel 43
  - Personalizing KDE 48
  - Configuring Email 50
- Configuring the Panel 51
  - Panel Configuration Dialog Box 51
  - Adjusting Items on the Panel 53
  - Adding Items to the Panel 53
  - Using the Menu Editor 54
  - Restart Option 56
- Manipulating Files and Directories 56
  - Introduction to the File Manager 56
  - Navigating the Filesystem with Konqueror 57
  - Performing Management Tasks 60
  - Navigating the Web 63
  - Looking Inside Archives 64
  - Special Features or Tips 64
- Project: Setting Up a Development Environment 65

### 4 GNOME 67

- What Is GNOME? 68
  - GNOME Is a Graphical Desktop 68
  - GNOME Applications and gtk+ 68
  - GNOME Is a Philosophy 69
- Installing GNOME 70
- Selecting GNOME 73
  - Using the Display Manager 73
  - Using switchdesk 73
  - Selecting GNOME Manually 74
- Basic Desktop Elements 75
  - The Desktop 75
  - The Panel 76
- Running Programs 76
  - Launching an Application 76
  - Essential Programs 77
- Logging Out of GNOME 77
- GNOME Capabilities 77
- Configuring GNOME with the Control Center 78
  - Desktop 79
  - Configuring the Window Manager 81
- Configuring the Panel 83
  - Global Panel Configuration 83
  - Adjusting Items on a Panel 86
  - Adding Items to the Panel 86
  - Using the Menu Editor 88
  - Configuring a Panel 89
  - Creating and Removing Panels 91
- Updating Helix GNOME 91
- Project: Installing Enlightenment 92

## II Sight and Sound

### 5 Configuring X 99

- What Is the X Window System? 100
- Understanding the X Window System 100
  - What Is a Client/Server System? 102
  - Output Capabilities 103
  - User Interface Capabilities 103
  - Input Capabilities 104
- Installing the XFree86 System 104
  - Choosing a Version of XFree86 104
  - Ensuring Hardware Support for XFree86 104
  - Installing from RPMs 106
  - Installing from deb Packages 108
  - Installing from tgz Packages 109
- Configuring XFree86 110
  - Using XF86Configurator 111
  - Using XF86Setup 111
  - Using LIZARD 111
  - Running the SuperProbe Program 113
  - Using xf86config 113
  - Using xvidtune 114
- Dissecting the XF86Config File 115
  - The Modules Section 115
  - The Files Section 116
  - The ServerFlags Section 116
  - The InputDevice Sections 116
  - The Monitor Section 116
  - The Device Section 117
  - The Screen Section 117
  - The ServerLayout Section 117
- X Window System Startup 118
  - Example: X Window System Startup on OpenLinux 118
  - Exploring Startup of the X Window System 119
  - The Display Manager 120
  - Xsession 122
  - Desktop or Window Manager Startup 123
  - Variation: startx 123
- Troubleshooting 123
- Case Study: The X Window System Across a Network 125

### 6 Customizing X and Controlling X Resources 127

- Navigating the X Window System 128
  - Getting Focus 128
  - Using Menus 129
  - Using Virtual Terminals in XFree86 129
- Using Window Managers for Linux 129
  - twm 130
  - fvwm2 131
  - AfterStep 132
  - Window Maker 133
  - Blackbox 133
- Enlightenment 133
- Sawfish 133
- kwin 133
- Choosing a Window Manager 134
- Themes 134
- X Resources 135
  - Nodes and Values 136
  - Loose Binding 136
  - Classes 136
  - Other Resource File Issues 137
  - Font Definitions 137
  - Loading and Querying Resources 140
- Project: Auto-Shrinking xterm 140

### 7 Multimedia 143

- Open Sound System for Linux 144
  - Getting and Installing Open Sound System for Linux 145
- RealPlayer 148
  - Getting and Installing RealPlayer 148
  - Using RealPlayer 149
- Adobe Acrobat Reader 157
  - Using Acrobat Reader 158
  - Creating PDF Files 160
- Troubleshooting 160

## III Linux System Administration

### 8 System Administration Tools 165

- Differences in Linux Distributions 166
- Caldera OpenLinux/COAS 167
  - Kernel Modules 167
  - Peripherals Administration 168
  - Network Administration 168
  - System Administration 170
  - Install/Remove Software Packages 171
- Autonomous LIZARD Modules 171
- Debian System Administration Tools 173
- Red Hat System Administration Tools 174
  - Config 175
  - Control 179
  - Quitting and Applying Your Changes 181
  - Accessing Linuxconf Remotely 181
- Project: Familiarize Yourself 181

### 9 Disk Drives and Filesystems 183

- Hard Drive Installation 184
- Partitioning the Hard Drive 185
  - Step 1 187
  - Step 2 187
  - Step 3 188
  - Step 4 188
  - Step 5 188
  - Step 6 188
  - Step 7 189
  - Step 8 189
  - Step 9 190
- Linux Filesystems 190
- Mounting Filesystems 193
  - Manually Mounting Filesystems 194
- Unmounting Filesystems 194
- Automating the Mounting Process 195
- Troubleshooting 196

### 10 Understanding the Linux Filesystem 199

- The Linux Filesystem Structure 200
- The Linux Filesystem Standard (FHS) 201
  - FHS Overview 201
  - FHS Specifications for the Root Directory 202
- Default Directory Layout 202
  - /NetWare 202
  - /auto 203
  - /bin 203
  - /boot 203
  - /bru 203
  - /dev 203
  - /etc 204
  - /home 204
  - /initrd 204
  - install@ 204
  - /lib 204
  - /lost+found 205
  - /mnt 205
  - /opt 205
  - /proc 205
  - /root 205
  - /sbin 206
  - /tmp 206
  - /usr 206
  - /var 206
  - /dev/shm 206
- Distribution Differences 207
- Examining Key Directories 207
  - The /etc Directory 208
  - The /dev Directory 212
  - The /devfs Directory 218
  - The /proc Directory 218
- Checking Filesystems 221
- Projects 223
  - Creating a Swap File 223
  - Using the file Command 224

### 11 Users, Groups, and Permissions 227

- User Accounts 228
  - Root User/Superuser 228
  - Normal Users 229
  - Virtual Consoles 229
  - Serial Connections 230
  - Network Logins 230
