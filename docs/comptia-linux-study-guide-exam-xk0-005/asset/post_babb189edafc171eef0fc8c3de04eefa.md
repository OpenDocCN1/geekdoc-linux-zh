
## Part IV Securing Your System 437

## Chapter 15 Applying Ownership and Permissions 439

- Looking at File and Directory Permissions 440
  - Understanding Ownership 440
  - Controlling Access Permissions 442
    - Exploring Special Permissions 445
    - Managing Default Permissions 446
- Access Control Lists 448
- Context-Based Permissions 450
  - Using SELinux 451
  - Using AppArmor 455
- Understanding Linux User Types 457
  - Types of User Accounts 458
  - Escalating Privileges 458
- Restricting Users and Files 459
- Summary 464
- Exam Essentials 465
- Review Questions 466

## Chapter 16 Looking at Access and Authentication Methods 469

- Getting to Know PAM 470
- Exploring PAM Configuration Files 471
  - Enforcing Strong Passwords 474
  - Locking Out Accounts 477
  - Limiting Root Access 481
- Exploring PKI Concepts 483
  - Getting Certificates 483
  - Discovering Key Concepts 483
- Securing Data 484
- Signing Transmissions 485
- Using SSH 486
  - Exploring Basic SSH Concepts 486
  - Configuring SSH 488
  - Generating SSH Keys 490
  - Authenticating with SSH Keys 492
  - Authenticating with the Authentication Agent 494
  - Using SSH Securely 496
- Using VPN as a Client 498
- Summary 499
- Exam Essentials 499
- Review Questions 501

## Chapter 17 Implementing Logging Services 503

- Understanding the Importance of Logging 504
- The syslog Protocol 504
- The History of Linux Logging 506
- Basic Logging Using *rsyslog* 507
  - Configuration 507
  - Making Log Entries 509
  - Finding Event Messages 509
- Journaling with *systemd-journal* 510
  - Configuration 510
  - Viewing Logs 511
- Summary 513
- Exam Essentials 514
- Review Questions 515

## Chapter 18 Overseeing Linux Firewalls 517

- Providing Access Control 518
- Looking at Firewall Technologies 520
- Familiarizing Yourself with *firewall* 521
- Investigating *iptables* 525
- Exploring *nftables* 530
- Understanding UFW 533
- Forwarding IP Packets 539
- Dynamically Setting Rules 539
- DenyHosts 539
- Fail2Ban 540
- IPset 540
- Summary 542
- Exam Essentials 542
- Review Questions 544

## Chapter 19 Embracing Best Security Practices 547

- User Security 548
- Authentication Methods 548
- Multifactor Authentication 550
- Unique User Accounts 551
- Enforce Strong Passwords 551
- Restricting the Root Account 553
- Separation of Data 555
- Disk Encryption 556
- Restricting Applications 556
- Preventing Unauthorized Rebooting 557
- Restricting Unapproved Jobs 559
- Banners and Messages 559
- Restricting USB Devices 559
- Looking for Trouble 560
- Auditing 561
- Network Security 561
- Denying Hosts 561
- Disabling Unused Services 562
- Changing Default Ports 562
- Using Encryption on the Network 563
- Summary 564
- Exam Essentials 565
- Review Questions 567

## Part V Troubleshooting Your System 571

## Chapter 20 Analyzing System Properties and Remediation 573

- Troubleshooting the Network 574
  - Exploring Network Issues 574
  - Viewing Network Performance 578
  - Reviewing the Network’s Configuration 584
- Troubleshooting Storage Issues 587
  - Running Out of Filesystem Space 587
  - Waiting on Disk I/O 588
  - Measuring Disk Performance 591
  - Failing Disks 593
- Troubleshooting the CPU 594
- Troubleshooting Memory 595
  - Swapping 596
  - Running Out of Memory 599
- Surviving a Lost Root Password 600
- Summary 601
- Exam Essentials 601
- Review Questions 603

## Chapter 21 Optimizing Performance 607

- Looking at Processes 608
- Monitoring Processes in Real Time 610
- Managing Processes 614
  - Setting Priorities 614
  - Stopping Processes 615
- Summary 618
- Exam Essentials 619
- Review Questions 620

## Chapter 22 Investigating User Issues 623

- Troubleshooting Access 624
  - Local 624
  - Remote 629
- Authentication 630
- Examining File Obstacles 631
  - File Permissions 631
  - Directory Permissions 632
  - Working with Advanced Permissions 633
- File Creation 635
- Exploring Environment and Shell Issues 636
- Summary 638
- Exam Essentials 638
- Review Questions 639

## Chapter 23 Dealing with Linux Devices 643

- Communicating with Linux Devices 644
  - Device Interfaces 644
  - The /dev Directory 647
  - The /proc Directory 648
  - The /sys Directory 650
- Working with Devices 651
  - Finding Devices 651
  - Working with PCI Devices 654
  - Working with USB Devices 655
  - Supporting Monitors 656
  - Using Printers 658
  - Using Hot-Pluggable Devices 659
  - Detecting Dynamic Devices 660
  - Working with Dynamic Devices 660
- Summary 662
- Exam Essentials 662
- Review Questions 664

## Chapter 24 Troubleshooting Application and Hardware Issues 667

- Dealing with Storage Problems 668
- Exploring Common Issues 668
- Dealing with Specialized Issues 670
- Uncovering Application Permission Issues 674
- Analyzing Application Dependencies 677
  - Versioning 677
  - Updating Issues 677
  - Patching 678
  - Dealing with Libraries 679
- Exploring Environment Variable Issues 679
- Gaining GCC Compatibility 680
- Pursuing Reposity Problems 680
- Looking at SELinux Context Violations 681
- Exploring Firewall Blockages 682
- Unrestricting ACLs 682
- Unblocking Ports 683
- Unblocking Protocols 683
- Troubleshooting Additional Hardware Issues 684
  - Looking at Helpful Hardware Commands 684
  - Investigating Other Hardware Problems 688
- Summary 692
- Exam Essentials 692
- Review Questions 694

## Part VI Automating Your System 697

## Chapter 25 Deploying Bash Scripts 699

- The Basics of Shell Scripting 700
- Running Multiple Commands 700
- Redirecting Output 701
- Piping Data 702
- The Shell Script Format 703
- Running the Shell Script 704
- Advanced Shell Scripting 705
- Displaying Messages 706
- Using Variables 706
- Command-Line Arguments 709
- The Exit Status 710
- Writing Script Programs 711
- Command Substitution 711
- Performing Math 712
- Logic Statements 714
- Loops 717
- Text Manipulation 720
- Summary 721
- Exam Essentials 722
- Review Questions 724

## Chapter 26 Automating Jobs 727

- Running Scripts in Background Mode 728
  - Running in the Background 728
  - Running Multiple Background Jobs 729
  - Running Scripts without a Console 730
- Sending Signals 732
  - Interrupting a Process 732
  - Pausing a Process 732
- Job Control 734
  - Viewing Jobs 734
  - Restarting Stopped Jobs 736
- Running Like Clockwork 737
  - Scheduling a Job Using the at Command 737
  - Scheduling Regular Scripts 740
- Summary 744
- Exam Essentials 744
- Review Questions 746

## Chapter 27 Controlling Versions with Git 749

- Understanding Version Control 750
- Setting Up Your Git Environment 752
- Committing with Git 755
- Tags 762
- Merging Versions 763
- Summary 766
- Exam Essentials 766
- Review Questions 768

## Part VII Realizing Virtual and Cloud Environments 771

## Chapter 28 Understanding Cloud and Virtualization Concepts 773

- Considering Cloud Services 774
  - What Is Cloud Computing? 774
  - What Are the Cloud Services? 775
- Understanding Virtualization 777
  - Hypervisors 778
  - Types of Hypervisors 779
