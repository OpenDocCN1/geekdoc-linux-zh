
## Session 23–Installing Software Packages 263
Using Gnome RPM to Install and Remove Packages 263
Using the rpm Command to Install and Remove Packages 266
Understanding RPM filenames 267
Querying RPMs with the rpm command 268
Installing RPMs with the rpm command 269
Removing RPMs with the rpm command 270
Upgrading RPMs with the rpm command 271
Verifying RPMs with the rpm command 272

## Session 24–Building a New Kernel 275
Installing the Source Files and Rebuilding the Kernel 276
Installing kernel source files 277
Creating a monolithic versus a modular kernel 277
Configuring the Kernel 278
Building and Installing the Kernel and Modules 280
Building the kernel 280
Building and installing the modules 281
Installing the new kernel and setting up LILO 282
Rebooting the System 284

## Session 25–Scheduling Jobs in Red Hat Linux 287
Scheduling One-time Jobs 288
Submitting a one-time job 288
Verifying scheduled one-time jobs 289
Canceling one-time jobs and receiving the output 290
Scheduling Recurring Jobs 290
Submitting a cron job 291
Verifying the cron job is scheduled 292
Setting up cron jobs for any user 292

## Session 26–Backing Up and Restoring Files 297
Selecting a Backup Strategy and Storage Media 297
Backing Up and Restoring Files with the Tape Archiver — tar — Program 299
Backing up and restoring a single volume archive 300
Backing up and restoring a multivolume archive 301
Backing up on Tapes 302
Performing incremental backups 303
Performing automated-full and incremental backups 304

## Part VI — Sunday Afternoon 308

## Session 27–Building Software Packages from Source Files 309
Downloading and Unpacking the Software 309
Downloading the software 310
Unpacking the software 312

Building the Software from Source Files and Installing It 312
Building the software 313
Installing the software 314
Running the software 314
An overview of the basic building steps 315

## Session 28–Monitoring System Performance 317
Using the top Utility 318
Using the GNOME System Monitor 319
Using the vmstat Utility 320
Checking Disk Performance and Disk Usage 322
Exploring the /proc File System 323

## Session 29–Maintaining System Security 329
Establishing a Security Policy 330
Securing the System 331
Securing passwords 332
Securing Internet services 334
Monitoring System Security 336
Log files 337
Security news and updates 338

## Session 30–Getting Help from Available Resources 341
Using the Help Viewers 341
GNOME Help Browser 342
KDE Help 342
Using the Linux Commands to Get Help 343
man command 343
whatis command 344
apropos command 345
Looking Up Online HOWTO Files 345
Accessing Other Linux Resources 347
Web pages 348
Internet newsgroups 348
FTP archive sites 350
Magazines 350

Appendix A–Answers to Part Reviews 355
Appendix B–What’s on CD-ROM? 369
Index 371
GNU General Public License 401
CD-ROM Installation Instructions 410

## ☑ Friday

## Part I–Friday Evening
Session 1
Getting Ready to Install Red Hat Linux
Session 2
Making Room for Red Hat Linux
Session 3
Finishing the Red Hat Linux Installation
Session 4
Troubleshooting the Red Hat Linux Installation

## PART
## I
## Friday
Evening

- **Session 1**
  *Getting Ready to Install Red Hat Linux*
- **Session 2**
  *Making Room for Red Hat Linux*
- **Session 3**
  *Finishing the Red Hat Linux Installation*
- **Session 4**
  *Troubleshooting the Red Hat Linux Installation*

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_27_0.png)
![](img/eef64cc01382a4448bc55a2ee7dcc4ca_27_1.png)

## SESSION
![](img/eef64cc01382a4448bc55a2ee7dcc4ca_28_0.png)
![](img/eef64cc01382a4448bc55a2ee7dcc4ca_28_1.png)

## Getting Ready to Install
Red Hat Linux

## Session Checklist
- ✓ Taking stock of your PC's components
- ✓ Creating a Red Hat boot disk

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_28_2.png)

30 Min.
To Go

After installing Red Hat Linux on a PC, the best way to learn it is interactively, using the Linux commands and applications. To that end, this evening's sessions guide you through the steps needed to install Red Hat Linux from this book's companion CD-ROMs. Assuming that the installation program recognizes most of the hardware installed in your PC, you should finish the installation in an hour or so. By the time you get to the third session of this evening, you should have Red Hat Linux installed on your PC. In this session, I guide you through the basic steps of gathering information about your PC's hardware and preparing the Red Hat boot disk needed to start the installation in Session 2.

## Taking Stock of Your PC's Components

You have to gather information about your PC's hardware before you install Red Hat Linux. Like many other operating systems, Linux supports various types of hardware through software components called device drivers. For each type of peripheral
