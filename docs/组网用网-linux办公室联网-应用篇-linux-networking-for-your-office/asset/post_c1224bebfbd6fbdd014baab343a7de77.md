
## 13 USING LINUX TO BACK UP CLIENT MACHINES 315

- Mounting Macintosh Volumes in Linux ................................ 312
- Summary ....................................................... 313
- Backing Up the Server ........................................... 317
- Backing Up to Tape .............................................. 317
- Backing Up to CD-R or CD-RW ..................................... 323
- Server-Initiated Backups ........................................ 326
- Using tar to Back Up Mounted Filesystems .......................... 327
- Creating cron Jobs to Back Up Regularly ........................... 329
- Security Considerations .......................................... 333
- Client-Initiated Backups ......................................... 333
- Backing Up to Disk ............................................... 334
- Security Considerations .......................................... 336
- Restoring Files ................................................. 336
- Partial Restores ................................................ 336
- Complete Restores and Disaster Recovery ........................... 339
- Backup Pitfalls .................................................. 343
- Lost Filesystem Attributes ....................................... 343
- The Windows Registry ............................................. 344
- OS/2 Extended Attributes ......................................... 345
- Macintosh Resource Forks ......................................... 345
- Effective Backup Schedules and Strategies ......................... 345
- Summary ......................................................... 346

## PART IV PRINTER SHARING 349

## 14 PREPARING TO SHARE A PRINTER 351

- Understanding Linux Printer Queues ............................... 352
- Printer Queues: Waiting Areas for Printing Files ................. 352
- Queues and Filters ............................................... 354
- Using Several Queues for One Printer .............................. 354
- Printer Escape Codes and PDLs .................................... 355
- The Tradition of PostScript in UNIX and Linux ..................... 356
- Using Ghostscript ................................................ 357
- Converting PostScript to Other Printer Formats by Using Ghostscript 358
- Obtaining and Installing the Latest Ghostscript ................... 359
- Ghostscript Files and Configuration ............................... 360
- Using Ghostscript Versus Printing Directly ........................ 362
- Advantages of Using Ghostscript .................................. 363
- Advantages of Printing Directly .................................. 364
- PostScript Printers .............................................. 365
- Configuring a Printer in Linux ................................... 366
- Using printtool to Set Up a Printer ............................... 367
- Testing Your Printer Setup......................................... 370
- Tweaking the Configuration Manually .............................. 371
- Managing Printer Queues ........................................... 375
- Viewing Print Jobs by Using lpq .................................. 375
- Removing Print Jobs by Using lprm ................................ 376
- Printing a File by Using lpr ...................................... 376
- Managing the Print System by Using lpc ........................... 376
- Printer Sharing Security Considerations.......................... 377
- Summary ........................................................... 378

## 15 SHARING PRINTERS WITH OTHER UNIXes 379

- Using lpd to Share Printers ....................................... 380
- Configuring Linux to Accept Remote Print Jobs .................... 380
- Controlling Access to Your Printers .............................. 382
- Printing to a Remote UNIX Printer from Linux ..................... 384
- Using printtool to Configure Printing ............................ 384
- Configuring /etc/printcap Manually ............................... 385
- Chaining Printer Queues ........................................... 386
- Summary ........................................................... 387

## 16 SAMBA: SHARING PRINTERS WITH DOS, WINDOWS, AND OS/2 389

- Setting Samba Printer Options ..................................... 390
- Sharing Some or All Printers...................................... 391
- Setting Printer Names ............................................. 392
- Making Printers Browsable ......................................... 392
- Additional Printer Options ........................................ 393
- Printing Permissions .............................................. 394
- Using Passwords to Control Printer Access ........................ 395
- Using Linux /etc/printcap Group Controls ......................... 396
- Using the hosts allow and hosts deny Parameters .................. 397
- Configuring Windows for Printing ................................. 398
- Installing an Appropriate Driver ................................. 398
- Printing Files ................................................... 401
- Printing from Linux to a Remote SMB/CIFS Printer ................. 403
- Configuring a Print Queue by Using printtool ..................... 403
- Configuring a Queue Manually ..................................... 405
- Summary ........................................................... 406

## 17 NETATALK: SHARING PRINTERS WITH MACINTOSHES 407

- An Overview of Macintosh-Style Printer Sharing ................... 408
- Macintosh Printing Protocols ..................................... 409
- Understanding PPD Files .......................................... 409
