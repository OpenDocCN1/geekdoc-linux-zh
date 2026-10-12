
## B
BIND (Berkeley Internet Name Domain) DNS server. See also DNS server
- chroot jail for, 490
- configuring with bindconf, 450–455
- DNSSEC (signed zones), 491–492
- hiding version number, 487
- installing, 438–439
- limiting queries, 488–489
- obtaining latest version, 476
- running as non-root user, 487
- securing, 482–492
- Transaction Signatures (TSIG), 482–487
- turning off glue fetching, 490

bindconf, 450–455
- /etc/named.conf file and, 450
- forward master zone creation, 451–454
- reverse master zone configuration, 454–455

bind-utils distribution, 463

BIOS, of laptops, 8

/boot directory, partition size for, 19

boot disk
- for crash recovery, 597–598
- creating, 32–33, 51, 241–242

boot loader
- GRUB as, 56, 58, 64
- LILO as, 56, 57–60
- NTLoader as, 57, 60–63

bootable partition, 17–18, 21–22

booting. See also dual-booting Linux with Windows
- boot process overview, 67–69
- defined, 67
- new kernel, 243–244, 274–275
- passing kernel options, 20–21
- rc.sysinit script and, 69–70
- rebooting, 53, 62, 69, 72, 74–75
  - in rescue mode, 58, 70–71
- run levels, 69
- selecting OS to boot, 22, 23
- to single-user mode, 70
- starting eth0 upon, 119–121
- viewing boot messages, 68
- Windows within Linux, 64–65

boot.ini file, 63

BOOTP protocol, 23

## C
cal command, 580

canceling. See also disabling
- shutdown, 73
- terminating programs, 200–204

cat command, 527

cd command, 169–170

CD-ROM drives, kernel configuration for, 259

CD-ROMs, 172–173. See also Red Hat CD-ROM

chattr command, 186

chfn command, 156

chgrp command, 179

chkconfig utility, 83–84

chmod command, 184–185, 527–528

chown command, 178–179, 528–529

chroot command, 58, 490

chsh command, 154, 421

Class A, B, and C IP networks, 585–587

clear command, 529

cmp command, 529–530

color mode, 108–109, 110–111

command-line FTP client, 430–433
- aborting file transfer, 433
- closing FTP connection, 433
- connecting to FTP server, 430
- downloading files and directories, 431–432
- escaping to shell, 433
- navigating the FTP site, 431
- restarting failed download, 432
- setting transfer mode, 431
- uploading files, 432

command-line RPM tool. See rpm command

command-line syntax, 195–196

commands
- DOS-compatible, 558–560
- file- and directory-specific, 527–548
- file compression and archive-specific, 548–554
- file system-specific, 554–558
- network administrator, 569–577
- network services access, 565–569
- online manuals for, 525–526
- printing-specific, 583–584
- process management, 577–579
- productivity, 579–581
- redirecting output of, 200
- regular expressions with, 198–199
- running in background, 200
- shell, 581–583
- system status-specific, 560–562
- for task automation, 579
- terminating, 200–204
- user administration, 562–565
- wildcards with, 196–197

compatibility issues, 8, 117

compilers, Apache, 282

compiling, 52, 244–275

compress command, 548–549

copying files, 175

cp command, 175, 176, 530

CPU requirements, 5, 6, 248

crash recovery, 597–598

cron facility, 218–221

crond daemon, 219

cut command, 531

## D
dd command, 61–62, 554

default gateway, 123, 128–129, 130–131

delayed reboot, 74–75

delayed shutdown, 72–73

deleting. See also canceling; disabling
- anonftp package, 424–425
- files and directories, 176
- Linux boot loader from MBR, 58
- network interface, 130
- partitions using fdisk, 15
- services from run levels, 84
- user accounts, 157
- user's home directory, 157

desktop workstations, 5–6, 12

df command, 555

DHCP (Dynamic Host Configuration Protocol), 23

diff command, 532–534

dig command, 463, 477

directories
- Apache, 290–293
- changing ownership, 178–179
- changing with cd, 169–170
- copying, 175
- creating with mkdir, 170–171
- deleting, 176
- FHS overview, 167–169
- finding, 171–172
- home directory, 155
- incoming or dropbox, 417–419
- init directory structure, 79–80
- moving, 175–176
- permissions, 185
- on removable devices, 172–174
- top, in FHS system, 168
- /usr directory structure, 169
- viewing access statistics, 174

disabling
- Ctrl+Alt+Backspace, 100
- Ctrl+Alt+Keypad-Plus or -Minus, 100–101
- glue fetching, 490
- GNOME splash screens and prompts, 229–231
- user accounts, 157

Disk Druid, 13

disk quotas, 161–166, 266

dividing a network into subnetworks, 132–140

Dlint, 477–482
- installing, 477–478
- obtaining, 477
- overview, 477
- running, 478–482
- sample output, 478–482

dmesg program, 68, 118–119, 560

DNS (Domain Name Service) configuration
- A record, 24, 448, 452–453, 457, 477, 480, 490
- for cache-only slave server, 460
- checking using Dlint, 477–482
- CNAME record, 449, 472, 475, 481
- for DNS client, 435–438
- domain- or zone-specific, 443–450
- /etc/hosts file, 437–438
- /etc/named.conf file, 439–443, 444
- /etc/resolv.conf file, 122, 436
- forward master zone creation, 451–454
- installing BIND DNS server, 438–439
- for mail service, 357–359
- manual server configuration, 455–460
- for master server, 455–457
- MX record, 357–358, 449–450, 456
- NS record, 448, 452, 456, 490
- PTR record, 449, 458–459, 477, 480–481
- reloading, 462
- resource record (RR), 444–445
- reverse master zone configuration, 454–455
- for reverse server, 458–460
- round robin DNS, 475
- securing BIND, 482–492
- for slave server, 457–458
- SOA record, 445–447, 456
- using bindconf, 450–455

DNS Security Extension (DNSSEC), 491–492

DNS server. See also BIND (Berkeley Internet Name Domain) DNS server
- for balancing server load, 474–475

DNS server. (continued)
- bindconf for configuring, 450–455
- cache-only slave server, 460
- installing BIND, 438–439
- limiting queries, 488–489
- manual configuration, 455–460
- master server, 455–457
- reloading configuration, 462
- reverse server, 458–460
- slave server, 457–458
- spoofing, 476, 483–487
- starting, 461
- stopping, 462
- testing, 462–463
- turning off glue fetching, 490
- viewing statistics, 462
- virtual domains, 464–474

DNS spoofing, 476, 483–487

DNSSEC (signed zones), 491–492

DOS-compatible commands, 558–560

DSO (Dynamic Shared Object) support, 282

du command, 534

dual-booting Linux with Windows, 55–65
- booting Windows within Linux, 64–65
- LILO installation and, 22
- prerequisites, 56–57
- using GRUB, 56, 58, 64
- using LILO, 56, 57–60, 64
- using NTLoader, 57, 60–63
- Windows 98, 63–64
- Windows NT/2000, 55–63
- Windows XP Professional, 56

Dynamic Host Configuration Protocol (DHCP), 23

Dynamic Shared Object (DSO) support, 282

## E
eduquota command, 164–165, 556

e-mail services, 357–393. See also sendmail
- configuring clients, 393
- DNS setup for, 357–359
- POP service setup, 390–393
- securing sendmail, 387–390
- SMTP service setup, 359–380
- testing, 381–387

/etc/default/useradd file, 158–159

/etc/fstab file, 162

/etc/ftpaccess file, 399–412
- access configuration, 401–404
- default file, 400
- email directive, 405
- format, 399
- informational configuration, 405–407
- logging configuration, 407
- miscellaneous configuration, 410–412
- permission configuration, 407–409

/etc/ftpconversions file, 412

/etc/ftpgroups file, 413

/etc/ftphosts file, 314

/etc/ftpusers file, 414

/etc/hosts file, 437–438

/etc/inittab file, 69–70, 74, 76–80

/etc/lilo.conf file, 52–53, 54, 58–60

/etc/login.defs file, 159–161

/etc/logrotate.d/apache file, 351–353

/etc/mail/* files, 371–380
- /etc/mail/access, 372–373
- /etc/mail/aliases, 373–374
- /etc/mail/domaintable, 374-375
- /etc/mail/mailertable, 375-376
- /etc/mail/relay-domains, 376-377
- /etc/mail/sendmail.cw, 377
- /etc/mail/virtualtable, 377-380
- securing, 387-389
- testing, 383-384

/etc/named.conf file, 439-443
- bindconf and, 450
- for cache-only slave DNS server, 460
- comment lines, 440-441
- for master (primary) DNS server, 456
- options statement, 440-441
- for reverse DNS server, 458-459
- for slave (secondary) DNS server, 457
- for virtual domain, 469-470
- zone statement, 442-443, 444, 456-460, 469-470

/etc/nologin file, 73

/etc/passwd file, 30, 71, 144-145, 147

/etc/rc.d/init.d subdirectory, 80-81, 85-88, 461

/etc/rc.d/rc[0-6].d subdirectories, 82

/etc/rc.d/rc scripts, 81-82

/etc/rc.d/rc.local script, 82, 163

/etc/rc.d/rc.serial script, 83

/etc/rc.d/rc.sysinit script, 80

/etc/resolv.conf file, 122, 436

/etc/Samba/smb.conf file, 494-509
- for encrypted passwords, 522
- [global] parameters, 503-508
- [homes] parameters, 408
- listing, 494-502
- [printers] parameters, 508-509
- for sharing Linux printer with Windows, 517-518
- testing, 510
- for using Linux file server on Windows, 511-512
- for Windows NT/2000 password server, 521

/etc/sendmail.cf file, 363-371
- C and F: define classes, 365
- D: define macro, 364-365
- H: define header, 366
- K: file declaration, 371
- M: define mailer, 365-366
- O: set options, 366-371
- overview, 363-364
- P: Precedence definitions, 371
- S and R: address rewrite rules, 364
- securing, 387-389
- test file, 386-387
- V: version level, 371

/etc/services file, 398

/etc/shadow file, 30

/etc/sudoers files, 147-150

/etc/sysconfig/network file, 119-120, 137, 138

/etc/sysconfig/network-scripts files, 120-121, 124-125, 137, 138, 139
