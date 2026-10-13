
- Testing /etc/mail/* database files ................. 209
- Using sendmail to see the SMTP transaction verbosely ........ 210
- Using the sendmail debug flag ................. 211
- Using a test configuration file ................. 212
- Securing Sendmail ................. 212
- Securing your configuration files ................. 213
- Ensuring a stricter mode of operating and privacy ................. 214
- Taking Antispam Measures ................. 215
- Confronting third-party mail relay vulnerability ................. 215
- Sending spammers to the black hole ................. 216
- Setting Up POP Mail Service ................. 218
- Configuring SMTP/POP Mail Clients ................. 219

## Chapter 10: FTP Service ................. 221
- Using wu-ftpd: The Default FTP Server ................. 221
- Installing the wu-ftpd server ................. 222
- Configuring FTP server ................. 223
- Creating an anonymous FTP site ................. 239
- Creating a guest FTP account ................. 244
- Creating virtual FTP sites ................. 247
- Using a Commercial FTP Server ................. 252
- Using a Trivial File Transfer Protocol Server ................. 252

## Chapter 11: Sharing Files and Printers with Samba ................. 255
- Installing Samba ................. 255
- Configuring Samba ................. 256
- Setting the [global] parameters ................. 266
- Setting the [homes] parameters ................. 270
- Setting the [printers] parameters ................. 271
- Managing Samba via Web ................. 272
- Testing the /etc/smb.conf configuration ................. 273
- Starting, stopping, and restarting the Samba service ................. 273
- Using a Linux File Server on Windows ................. 274
- Using a Windows File Server on Your Linux System ................. 275
- Sharing printers between Linux and Windows ................. 277
- Using an interactive Samba client ................. 280
- Securing Your Samba Server ................. 282

## Chapter 12: Web Service Using Apache ................. 285
- Getting Apache from the Internet ................. 285
- Creating a Custom Apache Server ................. 286
- Configuring Apache source using APACI ................. 286
- Compiling and installing Apache ............ 292
- Compiling and installing Apache support tools ............ 292
- Customizing Apache with optional or third-party modules ............ 295
- Getting Apache Up and Running ............ 299
- Running Apache as a standalone or inetd server ............ 300
- Configuring common directives ............ 303
- Configuring directives for a standalone server ............ 315
- Controlling the Apache server ............ 317
- Testing the Apache server ............ 320
- Managing Your Apache Server ............ 321
- Configuring Apache for CGI scripts ............ 321
- Configuring Apache for server-side includes ............ 327
- Hosting virtual Web sites ............ 338
- Using Apache as a proxy server ............ 341
- Authenticating Web users ............ 351
- Monitoring server status ............ 361
- Logging hits and errors ............ 362
- Enhancing Web server security ............ 370
- Using SSL for secured transactions ............ 380

## Chapter 13: Using NFS File Servers
- Installing an NFS Server ............ 389
- Configuring an NFS Server ............ 389
- Granting read-only access to the exported directory ............ 391
- Granting read and write access to the exported directory ............ 391
- Disabling access to a certain directory ............ 392
- Mapping users between the NFS server and the clients ............ 392
- Installing an NFS Client ............ 394
- Configuring an NFS Client ............ 394
- Securing Your NFS Server ............ 396
- Distributing Files Using rdist ............ 397

## Chapter 14: Configuring X Window
- Installing XFree86 ............ 403
- Configuring XFree86 ............ 403
- Using Xconfigurator to create the XF86Config file ............ 404
- Understanding the XF86Config file ............ 406
- Using X Windows ............ 416
- Configuring .xinitrc ............ 417
- Customizing the look and feel of window managers ............ 419
- Customizing the look and feel of client applications ............ 420
- Using xdm, the X Display Manager ............ 421

### Using XFree86 with MS Windows 9x/2000 .................... 422
### Getting Micro X-Win32 ........................... 422

## Part III: Troubleshooting ....................... 425

## Chapter 15: Security .............................. 427
### Securing User Access .............................. 427
- Restricting physical access ....................... 427
- Restricting normal user access .................... 428
- Restricting superuser access ...................... 429
- Restricting all access in an emergency or attack. 431
### Using Shadow Passwords ............................ 431
- Installing the shadow utility package ............ 432
- Converting /etc/passwd and /etc/group to shadow format. 433
- Managing user accounts ............................ 433
### Using Pluggable Authentication Modules (PAM) .... 434
- Working with a PAM configuration file ............ 436
- Using PAM to fine-tune the authentication process. 438
### Securing Services ................................. 440
- Removing unnecessary services during OS installation. 441
- Securing inetd-run services ...................... 442
### Protecting Your Files and File System ............ 445
- Mounting file systems as read-only ............... 456
- Taking advantage of ext2 file system ............. 457
- Using Tripwire to ensure file integrity .......... 458
### Playing Devil's Advocate .......................... 464
- Cracking your own passwords ....................... 465
- Having COPS around ............................... 468
### Back Up and Backtrack Everything ................. 471
### Get the Latest Security News ..................... 472
- CERT .............................................. 472
- BUGTRAQ@NETSPACE.ORG ............................. 472

## Chapter 16: Network Security ...................... 473
### Designing a Secure Network ....................... 473
- Using private IP addresses ....................... 473
- Masquerading IP addresses ....................... 474
### What Is a Firewall? .............................. 476
### Packet filters ................................... 477
- Using a basic packet-filtering firewall: ipchains. 478
- Using an application-level firewall .............. 480
### Using the Squid Proxy Server ................................ 481
- Getting and installing Squid ................................ 481
- Making Squid work for the first time ........................ 482
- Tweaking Squid to fit your needs ............................ 483
### Getting Help from SATAN .................................... 486
- Installing SATAN ........................................... 487
- Working with SATAN ......................................... 488

## Chapter 17: Customizing the Kernel .......................... 491
### What Linux Kernel Do You Have? .............................. 491
### Preparing for a Kernel Upgrade .............................. 493
### Installing the New Kernel .................................. 494
- Creating the initial ramdisk ............................... 495
- Configuring LILO ........................................... 495
- Booting with the new kernel ............................... 496
### Customizing the Kernel ..................................... 497
- Installing Linux kernel source ............................. 497
- Configuring the kernel the old-fashioned way ............... 498
- Configuring the kernel using make menuconfig ............... 519
- Configuring the kernel using make xconfig .................. 519
- Compiling, installing, and booting the new kernel .......... 520
### Patching a Kernel .......................................... 521
- Using kernelcfg ............................................ 522

## Appendix A: Common Commands ............................... 523
## Appendix B: Linux Resources ............................... 605
## Index ...................................................... 611
