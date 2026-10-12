
- Mounting Samba Shares .............................. 602
- Configuring Samba Using SWAT ........................ 603
- Network and Remote Printing with Fedora ............... 608
    - Creating Network Printers ........................... 608
    - Enabling Network Printing on a LAN ................. 608
    - Session Message Block Printing ...................... 611
    - Network-Attached Printer Configuration and Printing .. 612
    - Console Print Control .............................. 613
        - Console-Based Printer Configuration ................ 613
        - Using Basic Print Commands ....................... 614
        - Managing Print Jobs .............................. 615
    - Using the Common UNIX Printing System GUI ............ 616
        - Creating a CUPS Printer Entry ...................... 618
    - Avoiding Printer Support Problems .................... 621
    - All-in-One (Print/Fax/Scan) Devices .................. 621
    - Using USB and Legacy Printers ........................ 622
- Reference ............................ 623

## 24 Remote File Serving with FTP ............................ 625

- Using FTP Clients .................................. 625
    - The FTP Client Interface ........................... 626
        - Using the Text-Based FTP Client Interface .......... 626
        - Using Graphical FTP Clients ........................ 633
- FTP Servers .......................................... 636
    - Choosing an Authenticated or Anonymous Server ........ 637
    - Fedora FTP Server Packages ......................... 637
    - Other FTP Servers .................................. 637
- Installing FTP Software .............................. 638
- The FTP User ....................................... 639
- xinetd Configuration for wu-ftpd ..................... 641
    - Configuring xinetd for the wu-ftpd Server ........... 641
- Starting the Very Secure FTP Server (vsftpd) Package ... 642
- Configuring the Very Secure FTP Server ............... 643
    - Controlling Anonymous Access ....................... 643
    - Other vsftpd Server Configuration Files ............. 644
- Configuring the wu-ftpd Server ....................... 646
- Using Commands in the ftpaccess File to Configure wu-ftpd . 647
    - Configure Access Control ......................... 647
    - Configure User Information ....................... 650
    - Configure System Logging ....................... 654
    - Configure Permission Control ....................... 655
- Configure Commands Directed Toward the cdpath 657
- Structure of the shutdown File 658
- Configure FTP Server File-Conversion Actions 658
    - Strip Prefix 659
    - Strip Postfix 659
    - Add-On Prefix 659
    - Add-On Postfix 659
    - External Command 660
    - Types 660
    - Options 660
    - Description 660
    - An Example of Conversions in Action 660
- Using Commands in the ftphosts File to Allow or Deny FTP Server Connection 661
- Server Administration 662
    - Display Information About Connected Users 662
    - Count the Number of Connections 664
    - Use /usr/sbin/ftpsutsh to Schedule FTP Server Downtime 664
    - Use /var/log/xferlog to View a Log of Server Transactions 666
    - Reference 667

## 25 Handling Electronic Mail 669

- How Email Is Sent and Received 669
- The Mail Transport Agent 670
- Choosing an MTA 672
- The Mail Delivery Agent 673
- The Mail User Agent 673
- Basic Sendmail Configuration and Operation 674
- Configuring Masquerading 675
- Using Smart Hosts 675
- Setting Message Delivery Intervals 676
- Building the sendmail.cf File 676
- Mail Relaying 677
- Forwarding Email with Aliases 677
- Rejecting Email from Specified Sites 678
- Introducing Postfix 679
- Making the Switch 679
- Using Fetchmail to Retrieve Mail 680
- Installing Fetchmail 681
- Configuring Fetchmail 681
- Choosing a Mail Delivery Agent 684
- Proxmail ... 685
- Spamassassin ... 685
- Squirrelmail ... 685
- Virus Scanners ... 686
- Special Mail Delivery Agents ... 686
- Mail Daemons ... 686
- Alternatives to Microsoft Exchange Server ... 687
    - Microsoft Exchange Server/Outlook Client ... 687
    - CommuniGate Pro ... 688
    - Samsung Contact (Formerly Known As HP OpenMail) ... 688
    - Bynari ... 688
    - SuSE OpenExchange ... 688
    - Kroupware ... 688
    - OpenGroupware (Formerly SKYRIX 4.1) ... 689
    - phpgroupware ... 689
    - PHPprojekt ... 689
    - IMP/Horde ... 689
- Conclusion ... 689
- Reference ... 690
- Web Resources ... 690
- Books ... 691

## 26 Setting Up a Proxy Server 693

- What Is a Proxy Server? ... 693
- Installing Squid ... 694
- Configuring Clients ... 694
- Access Control Lists ... 695
- Specifying Client IP Addresses ... 700
- Sample Configurations ... 701
- Reference ... 702

## 27 Managing DNS 703

- Configuring DNS for Clients ... 704
- Understanding the /etc/host.conf File ... 705
- Understanding the /etc/nsswitch.conf File ... 705
- Understanding the /etc/hosts File ... 706
- Understanding the /etc/resolv.conf File ... 707
- Understanding the Changes Made by DHCP ... 707
- Essential DNS Concepts ... 708
    - How Nameservers Store DNS Structure Information ... 709
    - How DNS Provides Name Service Information to Users ... 709
    - Name Resolution in Practice ... 710
- Using DNS Tools 710
    - dig 711
    - host 712
    - nslookup 713
    - whois 713
- Configuring a Local Caching Nameserver 715
- Your Own Domain Name and Third-Party DNS 716
- Providing DNS for a Real Domain with BIND 717
    - rndc.conf 719
    - named.conf 719
    - Logging 724
    - Resolver Configuration 725
    - Running the named Nameserver Daemon 726
- Providing DNS for a Real Domain 727
    - Forward Zone 727
    - Reverse Zone 729
- Registering the Domain 730
- Troubleshooting DNS 730
    - Delegation Problems 731
    - Reverse Lookup Problems 731
    - Maintaining Accurate Serial Numbers 732
    - Troubleshooting Problems in Zone Files 732
    - Tools for Troubleshooting 733
- Using Fedora's BIND Configuration Tool 733
- Managing DNS Security 735
    - UNIX Security Considerations 735
    - DNS Security Considerations 736
- Using DNS Security Extensions 739
- Using Split DNS 740
- Reference 741

## 28 LDAP 743

- Configuring the Server 744
- Populating Your Directory 746
- Configuring Clients 749
    - Evolution 749
    - Thunderbird 750
- Administration 750
- Reference 751

## 29 News Servers 753

- Types of News Servers 753
    - Full Newsfeed Servers 754
    - Leaf Node Servers 754
    - Local News Servers 755
- The INN Package and Configuration Files 755
    - Installing the INN Package 757
    - Configuring innd 757
        - The inn.conf File 757
        - The incoming.conf File 759
        - The storage.conf File 759
        - The readers.conf File 760
        - The active and newsgroups Files 762
        - The history Files 763
        - Running innd 764
    - Reference 765

# Part V Programming Linux

## 30 Using Perl 769

- Using Perl with Linux 769
- Perl Versions 770
- A Simple Perl Program 770
- Perl Variables and Data Structures 772
    - Perl Variable Types 772
    - Special Variables 773
    - Operators 774
        - Comparison Operators 774
        - Compound Operators 775
        - Arithmetic Operators 775
        - Other Operators 775
        - Special String Constants 776
- Conditional Statements: if/else and unless
    - if ... 777
    - unless 777
- Looping 778
    - for 778
    - foreach 778
    - while 779
    - until 779
    - last and next 779
    - do ... while and do ... until 780
- Regular Expressions 780
- Access to the Shell 781
- Modules and CPAN 782
- Code Examples 783
    - Sending Mail 783
    - Purging Logs 785
    - Posting to Usenet 786
    - One-Liners 786
    - Command-Line Processing 787
- Reference 788
- Books 788
- Usenet 789
- WWW 789
- Other 790

## 31 Working with Python 791

- Python on Linux 791
- Getting Interactive 792
- The Basics of Python 793
    - Numbers 793
    - More on Strings 794
    - Lists 797
    - Dictionaries 799
    - Conditionals and Looping 800
    - Functions 802
    - Object Orientation 803
    - Class and Object Variables 804
    - Constructors and Destructors 805
    - Class Inheritance 806
    - Multiple Inheritance 807
- The Standard Library and the Vaults of Parnassus 808
- Reference 809

## 32 Writing PHP Scripts 811

- Introduction to PHP 812
- Entering and Exiting PHP Mode 812
- Variables 812
- Arrays 814
- Constants 815
- References 816
- Comments 817
- Escape Sequences 817
