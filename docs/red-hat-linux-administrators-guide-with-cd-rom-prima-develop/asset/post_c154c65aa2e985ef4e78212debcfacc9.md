
## Contents

### Backing Up
- Backing Up to Writable and Rewritable CDs . . . 261
- Backing Up to Internal Hard Drives . . . 263
- Using RAID Arrays . . . 264
- Organizing Backups . . . 265
- Alternating Strategies . . . 265
- Working with the at Command and cron Files . . . 266
- Comparing Archival Programs . . . 269
- Using the tar Command . . . 269
- Optimizing cpio for Older Backups . . . 272
- Backing Up Mobile Media Using dd . . . 274
- Dumping Data to Backup Media . . . 274
- Remotely Dumping Files . . . 278
- Burning Data or Audio Files to CDs . . . 281
- Choosing Commercial Archival Programs . . . 285
- Using Compression Utilities . . . 288
- Zipping Up Files . . . 288
- Using a More Complete Compression Utility, bzip2 . . . 290
- Restoring Backups . . . 292
- Restoring tarred Files . . . 292
- Bringing Dumps Back to Life . . . 293
- Remotely Controlling Multiple Backup Tapes . . . 297
- Conclusion . . . 299

### Chapter 10 Logging Errors . . . 301
- Monitoring System Use . . . 302
- Tracking Logging Levels . . . 303
- Discarding All Logs . . . 305
- Periodically Clearing and Restarting Logs . . . 306
- Rotating Log Files . . . 309
- Using grep to Locate Errors . . . 309
- Customizing the Rotation . . . 311
- Manually Rotating Logs . . . 313
- Recognizing Untouchable Log Files . . . 315
- Saving Log Files to Backup . . . 315
- Finding Logs . . . 316
- Locating Standard Log Files . . . 316
- Working with Nonsystem Log Files . . . 320
- Conclusion . . . 321

## PART III CUSTOMIZING THE SYSTEM . . . 323

### Chapter 11 Installing Additional Programs . . . 325
- Compiling Source . . . 326
- Open-Sourcing the Code . . . 327
- Finding the Local Binaries . . . 329
- Running the Latest Versions . . . 330
- Obtaining the Source Code . . . 333
- Creating Directories for New Code . . . 335
- Compiling Code . . . 339
- Configuring Dependent Libraries Beforehand . . . 340
- Running the Configure Routine . . . 342
- Running the make Command . . . 344
- Installing the Compiled Source . . . 345
- Checking for Debugging Symbols . . . 346
- Installing Binaries . . . 348
- Defining RPM Packages . . . 348
- Differences between RPMs and Source . . . 349
- Advantages of Using RPMs . . . 350
- Using RPMs . . . 351
- The Composition of an RPM File . . . 351
- Dynamic Package Installation . . . 353
- Uninstalling RPMs . . . 354
- Performing RPM Upgrades . . . 356
- Querying the Package Database . . . 356
- Verifying the Integrity of Installed Packages . . . 358
- Creating RPM Packages from Source . . . 359
- Staying Current with Update Agent . . . 360
- Running Update Agent in an X Window Environment . . . 364
- Updating Packages from the Command Line . . . 367
- Using alien to Convert Packages . . . 368
- Running Gnome-RPM . . . 370
- Conclusion . . . 378

### Chapter 12 Configuring Applications under the X Window System . . . 379
- Customization of the X Window Interface . . . 380
- Distinguishing GUIs . . . 381
- Specifying Video Settings . . . 382
- Running Xconfigurator . . . 386
- Editing the XF86Config File . . . 387
- Setting Up the Mouse . . . 387
- Manually Editing the Default Resolution . . . 390
- Starting X . . . 393
- Windows Managers versus Desktops Environments . . . 394
- Examining the Default Manager for Red Hat . . . 396
- Installing and Upgrading Gnome . . . 400
- Discussing the Features of KDE . . . 401
- Theming the Desktop . . . 404
- Discussing the KDE Packages . . . 406
- Installing KDE RPMs . . . 409
- Compiling KDE Source Code . . . 410
- Performing Postinstallation Procedures . . . 411
- Using Window Maker . . . 412
- Installing Window Maker . . . 416
- Suites for Home and Office . . . 416
- Using StarOffice . . . 417
- Downloading and Installing StarOffice . . . 418
- Perfecting WordPerfect for Linux . . . 420
- Exploring Newcomers to the Linux Scene . . . 422
- Graphics . . . 423
- Designing with the GIMP . . . 423
- Viewing through Electric Eyes . . . 425
- Using TrueType and Adobe Fonts under Linux . . . 425
- Dynamic Linux Databases . . . 428
- Setting the Standard for Free Databases . . . 428
- Making MySQL Your SQL Database . . . 429
- Using PostgreSQL . . . 431
- Conclusion . . . 432

### Chapter 13 Linux Print Serving . . . 433
- Printing on the Local Linux Box . . . 434
- Connecting via Serial Devices . . . 435
- Preparing Linux for Print Jobs . . . 436
- Configuring the Printer Variables . . . 438
- Using the PrintTool Utility . . . 439
- Testing the Printer Configurations . . . 445
- Restarting the lpd Daemon . . . 446
- Printing Directly to the Port . . . 446
- Conclusion . . . 448

### Chapter 14 Building a Custom Kernel . . . 449
- Defining the Linux Kernel . . . 450
- Distinguishing Default Kernels from Customized Kernels . . . 451
- Obtaining the Latest Kernel Version . . . 452
- Distinguishing Stable Source Code from Developmental Source Code . . . 455
- Properly Compiling a Kernel . . . 456
- Preparing for the Install . . . 456
- Determining Source Code for the Kernel . . . 459
- Initiating the Configuration . . . 460
- Choosing the Settings . . . 464
- Compiling the Kernel . . . 466
- Building and Installing Modules . . . 467
- Editing the lilo Configuration . . . 468
- Placing the New Kernel on Boot Media . . . 471
- Troubleshooting the Kernel . . . 473
  - Storing Golden Kernels . . . 473
  - Patching Kernels . . . 474
- Conclusion . . . 476

## PART IV THINKING OUTSIDE THE BOX . . . 477

### Chapter 15 Networking Linux . . . 479
- Creating an Internet Presence . . . 480
- Understanding Networking Basics . . . 481
- Packaging Data into Packets . . . 482
- Routing through Networks . . . 484
- Preparing Linux for Networking . . . 484
- Starting Network Installation . . . 487
- Configuring Network Settings after Installation . . . 490
- Defining Your Computer's Hostname . . . 491
- Configuring the Host File . . . 492
- Setting Up Services . . . 493
- Selecting Entries for the inetd.conf File . . . 494
- Resolving Domains and Name Servers . . . 495
- Configuring Hosts . . . 496
- Setting Up the Main Networking File . . . 497
- Configuring Networking Capabilities from the Command Line . . . 497
- Using a GUI to Edit Network Variables . . . 499
- Running linuxconfg for Networking . . . 502
- Testing the Connection . . . 504
- Using the ifconfig Command . . . 505
- Configuring Additional Network Devices . . . 507
