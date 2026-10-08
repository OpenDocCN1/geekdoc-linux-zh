
## Table of Contents (Continuation)

- GNOME Power Manager . . . 595
- GKrellM . . . 596
- KDE Task Manager and Performance Monitor (KSysguard) . . . 597
- Grand Unified Bootloader (GRUB) . . . 597

### 28 Managing Users
. . . 601

- User Configuration Files . . . 601
- The Password Files . . . 601
  - */etc/passwd* . . . 602
  - */etc/shadow and /etc/gshadow* . . . 603
- Password Tools . . . 603
- Managing User Environments . . . 604
  - Profile Scripts . . . 604
  - */etc/skel* . . . 604
  - */etc/login.defs* . . . 604
  - */etc/login.access* . . . 605
- Controlling User Passwords . . . 605
- Adding and Removing Users with useradd, usermod, and userdel . . . 606
  - useradd . . . 607
  - usermod . . . 608
  - userdel . . . 609
- Managing Groups . . . 609
  - */etc/group and /etc/gshadow* . . . 609
- User Private Groups . . . 609
- Group Directories . . . 610
- Managing Groups with the system-config-users . . . 610
- Managing Groups Using groupadd, groupmod, and groupdel . . . 610
- Controlling Access to Directories and Files: chmod . . . 611
  - Permissions . . . 611
    - chmod . . . 612
  - Ownership . . . 614
  - Changing a File’s Owner or Group: chown and chgrp . . . 614
  - Setting Permissions: Permission Symbols . . . 615
  - Absolute Permissions: Binary Masks . . . 616
- Directory Permissions . . . 617
  - Ownership Permissions . . . 618
  - Sticky Bit Permissions . . . 619
  - Permission Defaults: umask . . . 619
- Disk Quotas . . . 620
  - Quota Tools . . . 620
    - edquota . . . 621
    - quotacheck, quotaon, and quotaoff . . . 621
    - repquota and quota . . . 622
- Lightweight Directory Access Protocol . . . 622
  - LDAP Clients and Servers . . . 622
  - LDAP Configuration Files . . . 623
    - Configuring the LDAP server: /etc/slapd.conf . . . 623
  - LDAP Directory Database: ldif . . . 624
  - LDAP Tools . . . 629
  - LDAP and PAM . . . 629
- LDAP and the Name Service Switch Service . . . 629
- Pluggable Authentication Modules . . . 630
- PAM Configuration Files . . . 630
- PAM Modules . . . 630

### 29 Software Management
. . . 633

- Software Repositories . . . 634
- Software Package Types . . . 635
- Downloading ISO and DVD Distribution Images with BitTorrent . . . 635
- Updating Using yum and PUP . . . 636
- PUP . . . 637
- Update with the yum Command . . . 637
- Automatic Yum Update . . . 637
- Installing Fedora Packages with YUM . . . 638
- Yum Configuration . . . 638
  - /etc/yum.conf . . . 639
  - Repository Files: /etc/yum.repos.d . . . 639
    - Fedora . . . 640
    - Livna . . . 640
    - Freshrpms . . . 641
    - jpackage . . . 641
- Creating Local Yum Repositories . . . 642
- Managing YUM Caches . . . 642
- APT . . . 642
- Red Hat Package Manager (RPM) . . . 643
- RPM Tools . . . 643
- RPM Packages . . . 644
- Installing from the Desktop: rpm . . . 644
- Command Line Installation: rpm . . . 644
- The rpm Command . . . 644
- Querying Information from RPM Packages and Installed Software . . . 647
- Installing and Updating Packages with rpm . . . 648
- Installation Example . . . 649
- Removing RPM Software Packages . . . 650
- RPM: Verifying an RPM Installation . . . 650
- Rebuilding the RPM Database . . . 651
- Installing Software from RPM Source Code Files: SRPMs . . . 651
  - Source Code RPM Directories . . . 651
  - Building the Source Code . . . 651
- Installing Software from Compressed Archives: .tar.gz . . . 652
  - Decompressing and Extracting Software in One Step . . . 652
  - Decompressing Software . . . 652
  - Selecting an Install Directory . . . 653
  - Extracting Software . . . 653
  - Compiling Software . . . 654
  - Configure Command Options . . . 655
  - Development Libraries . . . 655
  - Shared and Static Libraries . . . 656
  - Makefile File . . . 656
