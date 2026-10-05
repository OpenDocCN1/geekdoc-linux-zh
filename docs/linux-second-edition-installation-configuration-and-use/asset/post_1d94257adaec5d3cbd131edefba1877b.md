
CONTENTS ix
HOWTO – how does that work? 77
DP – the Linux Documentation Project 79
Kernel documentation 79
KDE and GNOME help 79
Documentation on individual software packages 80
Distribution-dependent documentation 81

## Part II Configuration 83

### 5 Linux fundamentals 85
#### 5.1 Fundamentals of file management 86
- Files and directories 86
- Wildcards 87
- Complications using wildcards 88
- Wildcards for advanced users 89
- Hidden files 90
- Directories 90
- Linux directory structure (file system hierarchy standard) 91
- Ownership and access privileges 91
- Special rights and privileges 96
- User and group administration 96
- Hard links and symbolic links 98
- Links to programs 99

#### 5.2 File systems and partitions 100
- Access to several hard disks (partitions) 100
- Access to CD-ROM drives 102
- Access to floppy disk drives 104
- Access to streamers 105

#### 5.3 File system types 105

#### 5.4 File system internals 107
- Internals of the ext2 file system 107
- RAID 112
- Devices 114
- Information about process administration in /proc directory 116

#### 5.5 Process administration 117
- Background processes 118
- Distribution of CPU time 118
- Daemons 119
- Pipes 120

#### 5.6 Libraries 120

#### 5.7 System start (Init-V) 124

## Configuration and administration

### 6.1 Survival rules 134
#### 6.2 Elementary configuration steps 135
- Keyboard 135
- Input and display of foreign language characters 137
- Time of day 138
- Setting the default editor 139
- Setting the input prompt 139
- Configuration of less 139

#### 6.3 Text console configuration 141
- Additional keyboard shortcuts 141
- Mouse support 141
- Inverse or colored text display 142
- Text mode with 80x50 characters 143
- Character sets 143

#### 6.4 Registering users and passwords 144
- Defining a password for root 144
- Registering new users 145
- Access privileges 147

#### 6.5 File system administration 147
- The fstab file 147
- Distributing Linux file systems across several partitions 150
- Mounting DOS, Windows, and OS/2 partitions 153
- Mounting a CD-ROM drive 154
- Mounting swap partitions 154
- Mounting a swap file 155

#### 6.6 Hard disk tuning 155
- Bus master DMA mode 156
- Striping (RAID-0) 157

#### 6.7 Printer configuration 162
- The printer daemon lpd 163
- Spooler management 164
- Automatic conversion into printer format 165

#### 6.8 Modern configuration 166

#### 6.9 Network configuration 171
- Basics 171
- Configuration files 175
- Configuring a small network with ftp and NFS 177

#### 6.10 Boot diskettes/LILO 180
- Kernel boot diskette 181
- Using LILO 182
- LILO internals 183
- LILO configuration 185
- LILO boot diskette 189
- LILO installation in the boot sector of the hard disk
- Installing LILO in a DOS partition (1024-cylinder limit)
- Starting LILO with the Windows NT boot manager
- Starting Linux from DOS LOADLIN

#### 6.11 Recompiling the kernel
- Modules
- Installing/updating the kernel code
- Configuring the kernel
- Compiling and installing the kernel
- Update to kernel 2.2

#### 6.12 Package management (RPM)
- RPM bases
- The rpm command
- rpm user interfaces
- Manual installation of additional programs with tar

## 7 XFree6

### 7.1 Configuring the X Server
- A minimalist X Glossary
- Monitor and graphics card fundamentals
- The configuration process
- Xf86setup configuration program
- The configuration program xf86config
- The vt program
- The structure of xf86config
- Testing X

#### 7.2 Mouse and keyboard under X
- Keyboard configuration
- Global key combinations
- Input focus
- Using the mouse

#### 7.3 Resources
- Resource files

#### 7.4 fonts
- Font management
- Font server
- TrueType fonts
- Setting the dpi value

#### 7.5 X in multiuser operation

#### 7.6 Screen savers

## 8 user interfaces (fvwm, KDE, and GNOME) 261
### 8.1 Introduction 261
#### 8.2 Selecting your window manager or desktop environment 266
- The X start-up process 267

#### 8.3 fvwm (Virtual Window Manager) 272
- fvwm 1.2 274
- fvwm 2.0 277
- fvwm 9.5–2 278

#### 8.4 KDE 279
- Installation and start 280
- Survival rules 281
- Configuration 282
- The KDE panel 286
- Disk Navigator 287
- The KDE display manager (kdm) 289
- Mouse and keyboard shortcuts of the KDE window manager 290

#### 8.5 GNOME 290
- Survival rules 291
- Configuration 292
- The GNOME Panel 294
- Internals 297
- Mouse and keyboard shortcuts of Enlightenment 297

## Part III 9 Internet with Linux 301
### 9.1 Internet basics 301
- Internet via telephone 302
- TCP/IP 303

#### 9.2 PPP basics 304
- Glossary
- Kernel and network requirements 307

#### 9.3 PPP configuration 309
- Manual configuration
- Establishing the connection (ppp-on, ppp-off) 313
- Menu-driven PPP configuration 317

#### 9.4 SLIP configuration 323

#### 9.5 World Wide Web (WWW) 324
- Introduction
- Netscape 326
- kfm (KDE file manager) 330
- Lynx 331
- Surfing offline (WWW) 332

#### 9.6 File transfer protocol (FTP) 335
- The ftp command 336

#### 9.7 telnet and rlogin 339

## 10 Email 341
### 10.1 Basics 341
- Internals of mail management 342
- Glossary, working techniques 345

#### 10.2 Netscape Messenger 348

#### 10.3 KDE Mail 350
#### 10.4 pine 351
- Configuration 351
- Usage 353
- Alternatives to pine (elm, mail, Emacs) 357

#### 10.5 sendmail and fetchmail configuration 359
- Sending mail (sendmail) 359
- Fetching mail via POP (fetchmail) 363
- Script for automatic mail delivery via PPP 365

## 11 News 367
### 11.1 Basics 367
- Introduction 367
- Glossary, working techniques 368
- Linux-specific newsgroups 371

#### 11.2 News clients 371
- Netscape Messenger 372
- slrn 374
- tin 377

#### 11.3 Offline news configuration (Leafnode) 380
- Installation and configuration 381
- Operation 382
- Deleting old news articles 384

## Part IV 385

## 12 The bash – a modern command interpreter 387
### 12.1 What is a shell? 387
- Changing to a different shell 388
- Changing the default shell 389

#### 12.2 Command input 389
- Expansion of command and file names 389
- Important keyboard shortcuts 391
- Alias abbreviations 391

#### 12.3 Input and output redirection 392
- Pipes 393
- Output multiplication using tee 393

#### 12.4 Command execution 394
- Background processes 394
- Execution of several commands 395

#### 12.5 Substitution mechanisms 396
- File name generation using wildcards 396
- Character string generation using braces 397
- Calculation of arithmetic expressions in square brackets 398
- Command substitution 398
- Special characters in character strings 399

#### 12.6 Shell variables 400
- Local and global variables (environment variables) 401
- Important shell variables 402

## 13 bash programming 405
### 13.1 Introduction 405
#### 13.2 Variable management in shell programs 410
- Scope of variables 410
- Variables predefined by the shell 411
- Parameter substitution 412
- Reading in variables with read 414

#### 13.3 Branches 415
- if branches 415
- Formulation of conditions with test 416
- case branches 417

#### 13.4 Loops 418
- for loops 418
- while loops 419
- until loops 419

#### 13.5 Shell program samples 420
- Text conversion filters 420
- mv and cp for regular expressions 421
- Endless loop for starting TeX automatically 424

#### 13.6 Shell programming reference 425
#### 13.7 Special characters reference 435

## Command reference 437
### 14.1 Command overview by subject 438
#### 14.2 Alphabetical command reference 441

## Tools and utilities 491
### 15.1 X utilities 492
- xterm and other terminal programs 492
- X standard tools (xclock, xcalc) 493
- Text display, text editors 495
- System and process control, CPU monitoring 495

### 15.2 File managers 496
- Midnight Commander (mc) 496
- Tcl/Tk file manager (tkdesk) 497
- The GNOME file manager (gmc) 499
- The KDE file manager (kfm) 500

### 15.3 Document and graphics conversion 501
- Text conversion DOS $\rightarrow$ Linux (fromdos, todos) 503
- ASCI $\rightarrow$ PostScript conversion (a2ps, mpage) 505
- DVI $\rightarrow$ PostScript conversion (dvips) 507
- PostScript $\rightarrow$ printer format conversion (gs) 509
- PostScript tools (psutil) 510
- Formatting man texts (groff) 511
- Formatting info texts (Textinfo) 512
- HTML conversion 513
- PDF conversion 515
- Graphics conversion 515

### 15.4 Displaying documents and graphics 518
- Displaying PostScript files (ghostview, kghostview,v) 518
- Viewing DVI files (xdvi, kdvi) 520
- Viewing PDF files (acroread) 522
- Viewing graphics files 523

### 15.5 Creating screenshots 523
- xv 523
- xgrab 524
- knapshot 525

### 15.6 Terminal emulators 525
- minicom 526
- seyon 529
