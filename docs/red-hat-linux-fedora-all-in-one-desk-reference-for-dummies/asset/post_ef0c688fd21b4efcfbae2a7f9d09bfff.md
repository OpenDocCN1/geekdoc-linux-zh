
Understanding How Red Hat Linux Boots ....403
Understanding the init process ....403
Examining the /etc/inittab file ....405
Trying a new run level with the init command ....406
Understanding the Red Hat Linux startup scripts ....407
Manually starting and stopping servers ....408
Automatically starting servers at system startup ....409
Taking Stock of Red Hat Linux System Configuration Files ....409

## Monitoring System Performance
- Using the top utility ....412
- Using the GNOME system monitor ....414
- Using the uptime command ....414
- Using the vmstat utility ....416
- Checking disk performance and disk usage ....417
- Viewing System Information via the /proc File System ....418
- Scheduling Jobs in Red Hat Linux ....421
- Scheduling one-time jobs ....422
- Scheduling recurring jobs ....423

### Chapter 2: Managing Users ....427
- Adding User Accounts ....427
- Using Red Hat User Manager to add user accounts ....428
- Using commands to manage user accounts ....430
- Understanding the /etc/passwd File ....431
- Managing Groups ....432
- Exploring the User Environment ....434
- Changing User and Group Ownership of Files ....436

### Chapter 3: Managing the File System ....439
- Learning the Red Hat Linux File System ....439
- Understanding the file system hierarchy ....440
- Mounting a device on the file system ....442
- Examining the /etc/fstab file ....444
- Sharing Files with NFS ....445
- Exporting a file system with NFS ....446
- Mounting an NFS file system ....447
- Backing Up and Restoring Files ....447
- Selecting a backup strategy and media ....447
- Commercial backup utilities for Linux ....449
- Using the tape archiver --- tar ....449
- Accessing a DOS File System ....454
- Mounting a DOS disk partition ....454
- Mounting DOS floppy disks ....455
- Using mtools ....457
- Formatting a DOS floppy ....460

Table of Contents
xix

### Chapter 4: Managing Applications . . . 463
- Working with Red Hat Package Manager 463
- Using the RPM commands 463
- Understanding RPM filenames 464
- Finding out about RPMs 465
- Installing an RPM 467
- Removing an RPM 468
- Upgrading an RPM 469
- Verifying an RPM 469
- Building Software Packages from Source Files 470
  - Downloading and unpacking the software 470
  - Building the software from source files 472
  - Installing SRPMS 475
- Updating Red Hat Linux Applications with the Update Agent 476
- Registering with Red Hat Network 476
- Updating Red Hat Linux packages 477

### Chapter 5: Managing Devices and Printers . . . 479
- Understanding Device Drivers 479
  - Device files 480
- Managing Loadable Driver Modules 481
  - Loading and unloading modules 482
  - Using the /etc/modules.conf file 484
- Managing USB Devices 485
- Managing Print Queues in Red Hat Linux 487
  - Spooling and print jobs 487
  - Printing with the lp command 488
  - Checking the print queue using lpc 489
  - Canceling the print job using cancel 489
  - Checking the printer status using lptest 489
  - Controlling the print queue 490

### Chapter 6: Upgrading and Customizing the Kernel . . . 491
- Upgrading with a Red Hat Kernel RPM 492
  - Downloading new kernel RPMs 492
  - Installing the kernel RPMs 492
  - Trying out the new kernel 493
- Rebuilding the Kernel 493
  - Creating a monolithic vs. a modular kernel 495
  - Configuring the kernel 496
  - Running the kernel configuration tool 497
- Building the Kernel 512
- Building and Installing the Modules 513
- Installing the New Kernel and Setting Up GRUB 513
- Rebooting the System 516

## Book VII: Security
### Chapter 1: Understanding Network and Host Security . . . 519
- Why Worry About Security? . . . 519
- Establishing a Security Framework . . . 520
  - Determine business requirements for security . . . 521
  - Perform risk analysis . . . 522
  - Establish security policy . . . 523
  - Implement security solutions (mitigation) . . . 524
  - Manage security . . . 524
- Securing Red Hat Linux . . . 525
- Understanding the host security issues . . . 526
  - Understanding network security issues . . . 526
- Learning Computer Security Terminology . . . 527
- Keeping Up with Security News and Updates . . . 530

### Chapter 2: Securing the Host . . . 531
- Installing Operating System Updates . . . 531
- Securing Passwords . . . 532
  - Shadow passwords . . . 532
  - Pluggable authentication modules (PAMs) . . . 533
- Protecting Files and Directories . . . 536
  - Viewing ownerships and permissions . . . 537
  - Changing file ownerships . . . 537
  - Changing file permissions . . . 537
  - Setting default permission . . . 538
  - Checking for set user ID permission . . . 539
- Using exec-shield . . . 540
- Encrypting and Signing Files with GnuPG . . . 541
  - Understanding public key encryption . . . 542
  - Understanding digital signatures . . . 543
- Using GPG . . . 544
- Monitoring System Security . . . 549

### Chapter 3: Securing the Network . . . 551
- Securing Internet Services . . . 551
  - Using chkconfig to disable standalone services . . . 551
  - Configuring the xinetd server to disable services . . . 552
- Using Secure Shell (SSH) for Remote Logins . . . 555
- Setting Up Simple Firewalls . . . 557
  - Screening the router with packet filtering . . . 559
  - Dual-homed host . . . 561
  - Perimeter network with bastion host . . . 562
  - Application gateway . . . 564

- Enabling Packet Filtering on Your Red Hat Linux System ... 565
  - Using the security level configuration tool ... 566
  - Using the iptables command ... 567

### Chapter 4: Performing Security Audits ... 571
- Understanding Security Audits ... 571
- Nontechnical aspects of security audits ... 572
- Technical aspects of security audits ... 573
- Learning a Security Test Methodology ... 573
- Some common computer vulnerabilities ... 574
  - Host security review ... 576
  - Network security review ... 580
- Exploring Security Testing Tools ... 583
  - nmap ... 584
  - Nessus ... 585
  - SAINT ... 588
  - SARA ... 589

## Book VIII: Internet Servers ... 591
### Chapter 1: Managing the Servers ... 593
- Understanding Internet Services ... 593
- TCP/IP and sockets ... 594
- Internet services and port numbers ... 597
- Using the xinetd Super Server ... 599
- Running Standalone Servers ... 602
  - Starting and stopping servers manually ... 602
  - Starting servers automatically at boot time ... 603

### Chapter 2: Running the Apache Web Server ... 611
- Exploring HTTP ... 611
- Exploring the Apache Web Server ... 614
  - Installing the Apache Web server ... 615
  - Starting the Apache Web server ... 615
  - Configuring the Apache Web Server ... 617
- Using Apache configuration tools ... 618
  - Apache configuration files ... 619
  - The httpd.conf configuration file ... 620
  - Virtual host setup ... 629
