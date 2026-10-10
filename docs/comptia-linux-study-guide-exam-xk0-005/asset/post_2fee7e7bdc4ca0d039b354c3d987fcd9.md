
## Contents at a Glance

### Part V Troubleshooting Your System 571

- Chapter 20 Analyzing System Properties and Remediation 573
- Chapter 21 Optimizing Performance 607
- Chapter 22 Investigating User Issues 623
- Chapter 23 Dealing with Linux Devices 643
- Chapter 24 Troubleshooting Application and Hardware Issues 667

### Part VI Automating Your System 697

- Chapter 25 Deploying Bash Scripts 699
- Chapter 26 Automating Jobs 727
- Chapter 27 Controlling Versions with Git 749

### Part VII Realizing Virtual and Cloud Environments 771

- Chapter 28 Understanding Cloud and Virtualization Concepts 773
- Chapter 29 Inspecting Cloud and Virtualization Services 791
- Chapter 30 Orchestrating the Environment 813

- Appendix Answers to the Review Questions 829

Index 897

## Contents

Introduction | xxxi

Assessment Test | xlv

Answers to Assessment Test | lv

### Part I
Gathering Your Tools 1

#### Chapter 1
Preparing Your Environment 3

- Setting a Learning Space 4
- Using That Old Laptop 4
- Creating a Virtualized Environment 5
- Jumping to the Cloud 7
- Exploring Linux Distributions 8
  - Looking at Red Hat Enterprise Linux 9
  - Looking at Ubuntu 10
  - Looking at openSUSE 11
  - Looking at Fedora 12
- Locating a Terminal 14
- Summary 15

#### Chapter 2
Introduction to Services 17

- What Is a Linux Server? 18
- Launching Services 19
- Listening for Clients 20
- Serving the Basics 22
  - Web Servers 22
  - Database Servers 23
  - Mail Servers 25
- Serving Local Networks 27
  - File Servers 27
  - Print Servers 28
  - Network Resource Servers 29
- Implementing Security 31
  - Authentication Server 31
  - Certificate Authority 33
  - Access Server (SSH) 33
  - Virtual Private Networks 34
  - Proxy Server 34
  - Monitoring 34
- Improving Performance 35
  - Clustering 35
  - Load Balancing 35
  - Containers 35
- Summary 36
- Exam Essentials 37
- Review Questions 38

#### Chapter 3 Managing Files, Directories, and Text 43

- Handling Files and Directories 44
  - Viewing and Creating Files 44
  - Copying and Moving Files 50
  - Removing Files 56
  - Linking Files and Directories 60
    - Establishing a Hard Link 60
    - Constructing a Soft Link 62
- Reading Files 63
  - Reading Entire Text Files 64
  - Reading Text File Portions 66
  - Reading Text File Pages 70
- Finding Information 71
  - Viewing File Information 72
  - Exploring File Differences 72
  - Using Simple Pinpoint Commands 75
  - Using Intricate Pinpoint Commands 79
- Summary 82
- Exam Essentials 83
- Review Questions 84

#### Chapter 4 Searching and Analyzing Text 89

- Processing Text Files 90
  - Filtering Text 90
  - Formatting Text 95
  - Determining Word Count 99
- Redirecting Input and Output 101
  - Handling Standard Output 101
  - Redirecting Standard Error 102
  - Regulating Standard Input 104
  - Piping Commands 106
  - Creating Here Documents 108
  - Creating Command Lines 109
- Editing Text Files 111
  - Appreciating Text Editors 111
  - Learning about Stream Editors 116
  - Summary 123
- Exam Essentials 124
- Review Questions 125

### Part II
Starting Up and Configuring Your System 131

#### Chapter 5 Explaining the Boot Process 133

- The Linux Boot Process 134
  - Following the Boot Process 134
    - Viewing the Boot Process 135
  - The Firmware Startup 136
    - The BIOS Startup 136
    - The UEFI Startup 137
  - Linux Bootloaders 138
    - GRUB Legacy 139
    - GRUB2 143
    - Alternative Bootloaders 145
  - System Recovery 146
    - Kernel Failures 146
    - Root Drive Failure 148
  - Summary 150
  - Exam Essentials 150
  - Review Questions 152

#### Chapter 6 Maintaining System Startup and Services 157

- Looking at init 158
- Managing systemd Systems 159
  - Exploring Unit Files 160
    - Focusing on Service Unit Files 162
    - Focusing on Target Unit Files 167
    - Looking at systemctl 168
    - Examining Special systemd Commands 172
- Managing SysV init Systems 178
  - Understanding Runlevels 178
    - Investigating SysV init Commands 182
- Digging Deeper into systemd 187
  - Looking at systemd Mount Units 187
  - Exploring Automount Units 189
  - Focusing on Timer Unit Files 190
- Summary 191
- Exam Essentials 191
- Review Questions 194

#### Chapter 7 Configuring Network Connections 199

- Configuring Network Features 200
  - Network Configuration Files 201
  - Graphical Tools 203
  - Command-Line Tools 205
  - Command-Line Networking Tool 214
  - Basic Network Troubleshooting 217
    - Sending Test Packets 217
    - Finding Host Information 219
  - Advanced Network Troubleshooting 222
    - The netstat Command 222
    - Examining Sockets 226
    - Monitoring the Network 226
    - Monitoring the Nis... 226
  - Summary 228
  - Exam Essentials 229
  - Review Questions 231

#### Chapter 8 Comparing GUIs 235

- Focusing on the GUI 236
- Getting to Know GNOME 237
- Probing KDE Plasma 239
- Considering Cinnamon 241
- Making Acquaintance with MATE 243
- Setting Up Accessibility 245
- Serving Up the GUI 247
- Figuring Out Wayland 248
- Examining X11 250
- Using Remote Desktops 252
  - Viewing VNC 252
  - Grasping Xrdp 254
  - Exploring NX 256
  - Studying SPICE 257
- Forwarding 257
  - Local 259
  - Remote 260
- Tunneling Your X11 Connection 261
- Summary 262
- Exam Essentials 262
- Review Questions 264

#### Chapter 9 Adjusting Localization Options 269

- Understanding Localization 270
  - Character Sets 270
  - Environment Variables 271
  - Setting Your Locale 272
    - Installation Locale Decisions 272
    - Changing Your Locale 272
- Looking at Time 275
  - Working with Time Zones 275
  - Setting the Time and Date 276
  - Watching System Time 280
- Summary 281
- Exam Essentials 282
- Review Questions 284

### Part III Managing Your System 289

#### Chapter 10 Administering Users and Groups 291

- Managing User Accounts 292
  - Adding Accounts 292
  - Maintaining Passwords 304
  - Modifying Accounts 306
  - Deleting Accounts 308
- Managing Groups 309
- Setting Up the Environment 313
  - Perusing Bash Parameters 313
  - Understanding User Entries 314
  - Grasping Global Entries 316
- Querying Users 316
  - Exploring the whoami Utility 316
  - Understanding the who Utility 317
  - Identifying with the id Program 318
  - Displaying Access History with the last Utility 319
- Managing Disk Space Usage 320
- Summary 323
- Exam Essentials 324
- Review Questions 325

#### Chapter 11 Handling Storage 329

- Storage Basics 330
  - Drive Connections 330
  - Partitioning Drives 331
    - Automatic Drive Detection 331
    - Partitioning Tools 332
      - Working with fdisk 332
      - Working with gdisk 334
      - The GNU parted Command 336
    - Graphical Tools 337
- Understanding Filesystems 337
  - The Virtual Directory 338
  - Maneuvering around the Filesystem 341
  - Formatting Filesystems 341
    - Common Filesystem Types 341
    - Creating Filesystems 343
  - Mounting Filesystems 344
    - Manually Mounting Devices 344
    - Automatically Mounting Devices 345
  - Managing Filesystems 346
    - Retrieving Filesystem Stats 346
    - Filesystem Tools 348
  - Storage Alternatives 349
    - Multipath 350
    - Logical Volume Manager 350
    - Using RAID Technology 354
    - Encrypting Partitions 355
  - Summary 358
  - Exam Essentials 358
  - Review Questions 360

#### Chapter 12 Protecting Files 363

- Understanding Backup Types 364
- Looking at Compression Methods 366
- Comparing Archive and Restore Utilities 368
  - Copying with cpio 369
  - Archiving with tar 372
  - Duplicating with dd 377
  - Replicating with rsync 380
- Securing Offsite/Off-System Backups 382
  - Copying Securely via scp 382
  - Transferring Securely via sftp 384
- Checking Backup Integrity 387
  - Digesting an MD5 Algorithm 387
  - Securing Hash Algorithms 388
- Summary 389
- Exam Essentials 389
- Review Questions 390

#### Chapter 13 Governing Software 393

- Working with Source Code 394
  - Downloading Source Code 394
  - Bundling Source Code Packages 395
  - Compiling Source Code 399
- Packaging Applications 400
  - Installing and Managing Packages 401
  - Understanding Repositories 405
