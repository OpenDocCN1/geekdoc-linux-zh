
## Immediate Solutions

- Setting Up A Local Printer In The Control Panel 225
- Setting Up A Local Printer At The Command Line 228
- Setting Up A Network Printer In The Control Panel 231
- Setting Up A Network Printer At The Command Line 233
- Setting Up A Machine To Host A Network Printer 233
- Setting Up Remote Printers To Print Over A Network 234
- Setting Up Popular Print Filters 235
- Testing The Printer 236
- Printing A File 236
- Viewing A Print Queue 237
- Cancelling A Print Job 237
- Checking A Printer's Status 238
- Disabling And Enabling A Print Queue 238

# Chapter 9
## System Security Basics 239

### In Depth

- Leaving The Door Wide Open 240
- Online Security Resources 245
- Available Tools 247
- Attacks And Intrusions 254
- Firewalls And You 256

### Immediate Solutions

- Activating And Deactivating The Shadow Suite 264
- Shutting Off Unnecessary Daemons And Background Processes 264
- Shutting Off Unnecessary Non-Daemon Network Services 267
- Restricting Network Access With tcp_wrappers 267
- Obtaining And Installing ssh 269
- Setting Up ssh On A Server 270
- Setting Up ssh On A Client 276
- Removing Unnecessary Packages 279
- Creating And Using A Named Pipe 280
- Logging 280
- Installing swatch 281
- Analyzing Logs 281
- Preparing For A Breach 282
- Recovering From A Breach 282
- Becoming The Superuser 283
- Installing The Crack Password Checker 283
- Securing Passwords With Crack 284
- Setting Password Rules 285
- Fighting Denial-Of-Service Attacks 285
- Getting And Installing PGP 285
- Setting Up An IP Firewall 287
- Setting Up A Proxy Firewall 289
- Refusing Login Access To All But Root 290

# Chapter 10
## KickStart For Repeat Installations 293

### In Depth

- Introduction To KickStart 294
- The Structure Of A KickStart Script 295
- The Test-Edit Cycle 304

### Immediate Solutions

- Installing The First Machine 306
- Building The Initial KickStart File 307
- Scripting Tips For KickStart 308
- Making A KickStart Boot Disk 308
- Booting Directly To KickStart 309
- Setting Up An NFS Installation Export 310
- Adding KickStart Data To Your DHCP Server 311
- Installing With KickStart 311
- Upgrading With KickStart 312
- Cloning Machine Configurations 313

# Chapter 11
## DNS With BIND 315

### In Depth

- The Domain Name System 316
- Name Service Under Linux 317
- Introduction To /etc/named.conf 319
- The Zone Files 328
- Name Service-Related Programs 333

### Immediate Solutions

- Installing The Name Server 336
- Configuring The Master Name Server 336
- Configuring The Slave Name Server 338
- Configuring A Forwarding-Only Server 340
- Creating The Initial Cache 342
- Creating The Reverse Local Zone File 343
- Creating Your Domain Zone 344
- Creating Your Reverse Domain Zone 346
- Creating Encrypted Keys 347
- Installing And Running `dnswalk` 348

# Chapter 12
## Internet Email: sendmail + IDA 351

### In Depth

- How Email Gets To Its Destination 352
- Introduction To `sendmail` 357
- Mailing Lists 369

### Immediate Solutions

- Installing All Of The Pieces 370
- Configuring Your `sendmail` Server At The Command Line 370
- Building `sendmail.cf` At The Command Line 372
- Tweaking Your `/etc/sendmail.cf` 372
- Adding Additional Mail Server Hostnames 372
- Centralizing Your Outgoing Mail Addresses 373
- Adding Configuration File Version Information 373
- Setting Your Log Level 374
- Reducing Server Load 375
- Configuring Your `sendmail` Server In `Linuxconf` 376
- Basic `sendmail` Configuration In `Linuxconf` 376
- Configuring Mail Routing In `Linuxconf` 380
- Configuring Email Masquerading In `Linuxconf` 383
- Configuring Email-To-Fax Service In `Linuxconf` 384
- Configuring Virtual Email Service In `Linuxconf` 389
- Configuring Your Anti-Spam Settings Under `Linuxconf` 391
- Setting Up Mail Aliases By Hand 393
- Protecting Yourself From Spam 394
- Building A CW File 397
- Building A Mailer Table 397
- Building A Virtual Addressing Table 398
- Building An Access Database 398
- Removing Mail From The Queue Under `Linuxconf` 399
- Configuring `procmail` 400

# Chapter 13
## The Apache Web Server 407

### In Depth

- Introduction To Apache 408
- The Configuration File 410
- Other Linux Web Servers 437

### Immediate Solutions

- Installing Apache 439
- Configuring Apache 439
- Configuring Apache Access 440
- Configuring **httpd** 443
- Setting Up Virtual Web Service 446
- Configuring What Web Browsers See 448
- Customizing Your Logs 451
- Setting Up .htaccess 452

# Chapter 14
## The Squid Internet Object Cache 453

### In Depth

- Introduction To Web Caching 454
- An Introduction To The Squid 454

### Immediate Solutions

- Installing The Squid 458
- Configuring The Squid 458
- Setting Up Parent And Sibling Caches 466
- Setting Up Web Server Acceleration 469
- Setting Up Multicasting 470
- Configuring A Client To Utilize Caching 470

# Chapter 15
## FTP And Telnet 475

### In Depth

- FTP Issues 476
- Telnet Issues 482

### Immediate Solutions

- Securing FTP 483
- Installing Anonymous FTP 487
- Securing Telnet 488
- Creating A **shutdown** Message 488

# Chapter 16
## NIS And NIS+ 491

### In Depth

- Introduction To NIS And NIS+ 492
- Using An NIS System 494

### Immediate Solutions

- Installing The NIS Server 496
- Installing The NIS Client 496
- Setting Up An NIS Server 497
- Setting Up An NIS Client 499

# Chapter 17
## NFS

### In Depth

- Introduction To NFS 502
- The NFS Configuration File 502

### Immediate Solutions

- Setting Up NFS Exports 505
- Mounting Remote File Systems With NFS 505
- Making And Mounting A Central /usr Directory 506
  - Creating The /usr Export 506
  - Mounting The /usr Export 508
- Setting Up An NFS Installation Server 509

# Chapter 18
## Samba

### In Depth

- Introduction To Samba 512
- The Samba Configuration File 513

### Immediate Solutions

- Installing Samba 527
- Configuring Samba 527
- Offering Linux Partitions 537
- Building A File Share Statement 541
- Mounting Windows Shares Under Linux 546
- Offering Windows Shares 546
- Offering Linux Printers 550
- Building A Print Share Statement 551
- Utilizing Windows Printers Under Linux 554
- Implementing Encrypted Passwords Over Samba 555
- Creating A User Map 556
- Creating A Host Map 557
- Creating Login Scripts 558

# Chapter 19
## Text Processing Tools

### In Depth

- The vi Editor 562
- Pattern Matching 568
- The sed Editor 570
- Additional Tools 574

### Immediate Solutions

- Maneuvering In **vi** 578
- Filtering Text In **vi** 579
- Copying And Pasting Text In **vi** 581
- Indenting Text In **vi** 581
- Using Regular Expressions 583
- Running `sed` With Multiple Commands 584
- Building A `sed` Script File 586
- Running `sed` With External File Scripts 588
- Using The `cut` Command 588
- Using The `join` Command 589
- Checking Spelling With `ispell` 590
- Building `ispell` Dictionaries 592
- Reducing `ispell` Dictionary Sizes 594
- Using The `tr` Command 595

# Chapter 20
## Shell Scripting 597

### In Depth

- The Shell 598
- Bash Shell Scripting 599

### Immediate Solutions

- Changing The Active Shell 609
- Installing The Public Domain Korn Shell 609
- Changing Your Bash Login Prompt 610
- Writing Your Own Package Update Script 611
- Writing Your Own User Creation Script 615
- Writing A Script To Find A File In Your RPMs 620
- Writing A Script To Monitor System Load 623

# Chapter 21
## Perl Scripting 627

### In Depth

- Introduction To Perl 628
- Perl Programming 628

### Immediate Solutions

- Installing Perl 636
- Getting And Installing A Perl Library Module 636
- Running A Perl Program 638
- Writing A CGI Script With Perl 639
- Processing A Web Form 639
