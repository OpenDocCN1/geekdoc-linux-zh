
## 11.3 Relocation Methods

- 11.3.1 Relocation Methods . 602
- 11.3.2 Relocation Precautions . 603
- 11.3.3 Assessing the Effect of Relocation. 603
- 11.3.4 Relocating the Entire Data Directory . 604
- 11.3.5 Relocating Individual Databases . 604
- 11.3.6 Relocating Individual Tables. 606
- 11.3.7 Relocating the InnoDB Shared Tablespace . 606
- 11.3.8 Relocating Status and Log Files. 607

## 12 General MySQL Administration

- 12.1 Securing a New MySQL Installation . 610
  - 12.1.1 Establishing Passwords for the Initial MySQL Accounts . 610
  - 12.1.2 Setting Up Passwords for a Second Server. 615
- 12.2 Arranging for MySQL Server Startup and Shutdown . 616
  - 12.2.1 Running the MySQL Server On Unix . 616
  - 12.2.2 Running the MySQL Server On Windows . 621
  - 12.2.3 Specifying Server Startup Options . 624
  - 12.2.4 Stopping the Server . 626
  - 12.2.5 Regaining Control of the Server When You Cannot Connect to It . 626
- 12.3 Controlling How the Server Listens for Connections . 629
- 12.4 Managing MySQL User Accounts . 630
  - 12.4.1 High-Level MySQL Account Management . 631
  - 12.4.2 Granting Privileges . 634
  - 12.4.3 Displaying Account Privileges. 643
  - 12.4.4 Revoking Privileges and Removing Users . 643
  - 12.4.5 Changing Passwords or Resetting Lost Passwords . 644
- 12.5 Maintaining Logs . 645
  - 12.5.1 The Error Log . 648
  - 12.5.2 The General Query Log . 649
  - 12.5.3 The Slow-Query Log . 649
  - 12.5.4 The Binary Log and the Binary Log Index File . 650
  - 12.5.5 The Relay Log and the Relay Log Index File . 652
  - 12.5.6 Using Log Tables . 652
  - 12.5.7 Log Management . 653
- 12.6 Tuning the Server . 660
  - 12.6.1 Checking and Setting System Variable Values. 661
  - 12.6.2 General-Purpose System Variables. 665
  - 12.6.3 Checking Status Variable Values . 667
- 12.7 Storage Engine Configuration . 669
  - 12.7.1 Selecting Which Storage Engines a Server Supports . 669
  - 12.7.2 Configuring the MyISAM Storage Engine . 671
  - 12.7.3 Configuring the InnoDB Storage Engine . 674
  - 12.7.4 Configuring the Falcon Storage Engine . 680
- 12.8 Enabling or Disabling *LOCAL* Capability for *LOAD DATA* . 681
- 12.9 Internationalization and Localization Issues . 681
  - 12.9.1 Configuring Time Zone Support . 682
  - 12.9.2 Selecting the Language for Error Messages . 684
  - 12.9.3 Configuring Character Set Support . 684
- 12.10 Running Multiple Servers . 685
  - 12.10.1 General Multiple Server Issues . 686
  - 12.10.2 Configuring and Compiling Different Servers . 688
  - 12.10.3 Strategies for Specifying Startup Options . 690
  - 12.10.4 Using *mysqld_multi* for Server Management . 691
  - 12.10.5 Running Multiple Servers on Windows . 693
- 12.11 Updating MySQL . 695

## 13 Access Control and Security

- 13.1 Internal Security: Preventing Unauthorized Filesystem Access . 700
  - 13.1.1 How to Steal Data . 701
  - 13.1.2 Securing Your MySQL Installation . 702
- 13.2 External Security: Preventing Unauthorized Network Access . 709
  - 13.2.1 Structure and Contents of the MySQL Grant Tables . 709
  - 13.2.2 How the Server Controls Client Access . 719
  - 13.2.3 A Privilege Puzzle . 724
  - 13.2.4 Grant Table Risks to Avoid . 728
- 13.3 Setting Up Secure Connections . 731

## 14 Database Maintenance, Backups, and Replication

- 14.1 Principles of Preventive Maintenance . 737
- 14.2 Performing Database Maintenance with the Server Running . 739
  - 14.2.1 Locking Individual Tables for Read-Only or Read/Write Access . 740
  - 14.2.2 Locking All Databases for Read-Only Access . 743
- 14.3 General Preventative Maintenance . 743
  - 14.3.1 Using the Server's Auto-Recovery Capabilities . 744
  - 14.3.2 Scheduling Preventive Maintenance . 745
- 14.4 Making Database Backups . 746
  - 14.4.1 Making Text Backups with mysqldump . 748
  - 14.4.2 Making Binary Database Backups . 751
  - 14.4.3 Backing Up InnoDB or Falcon Tables . 754
- 14.5 Copying Databases to Another Server . 755
  - 14.5.1 Copying Databases Using a Backup File . 755
  - 14.5.2 Copying Databases from One Server to Another . 756
- 14.6 Checking and Repairing Database Tables . 757
  - 14.6.1 Using the Server to Check and Repair Tables . 758
  - 14.6.2 Using mysqlcheck to Check and Repair Tables . 759
  - 14.6.3 Using mysqlcheck to Check and Repair Tables . 760
- 14.7 Using Backups for Data Recovery . 763
  - 14.7.1 Recovering Entire Databases . 764
  - 14.7.2 Recovering Individual Tables . 764
  - 14.7.3 Re-Executing Statements in Binary Log Files . 765
  - 14.7.4 Coping with InnoDB Auto-Recovery Problems . 767
- 14.8 Setting Up Replication Servers . 768
  - 14.8.1 How Replication Works . 769
  - 14.8.2 Establishing a Master-Slave Replication Relationship . 770
  - 14.8.3 Binary Logging Formats . 773
  - 14.8.4 Using a Replication Slave for Making Backups . 774

## IV: Appendices

- A Obtaining and Installing Software . 777
  - A.1 Obtaining the sampDB Sample Database Distribution . 777
  - A.2 Obtaining MySQL and Related Software . 778
  - A.3 Choosing a Version of MySQL . 780
  - A.4 Installing MySQL on Unix . 780
    - A.4.1 Creating a Login Account for the MySQL User . 782
    - A.4.2 Obtaining and Installing a MySQL Distribution on Unix . 782
    - A.4.3 Post-Installation Steps . 786
    - A.4.4 Installing Perl DBI Support on Unix . 789
    - A.4.5 Installing Apache and PHP on Unix . 790
  - A.5 Installing MySQL on Windows . 792
    - A.5.1 Installing Perl DBI Support on Windows . 796
    - A.5.2 Installing Apache and PHP on Windows . 796
