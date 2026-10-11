
## Contents

### 15.4 What Is the Perl DBI? 356

- Adding Another Table with a Primary Key 543
- Inserting Data into Tables 544
- Selecting Data from Tables—The SELECT Command 546
  - Selecting by Columns 546
  - Selecting All Columns 547
- The WHERE Clause 548
- Sorting Tables 550
- Joining Tables 551
- Deleting Rows 552
- Updating Data in a Table 553
- Altering a Table 554
- Dropping a Table 555
- Dropping a Database 555

- 15.4.1 Installing the DBD Driver 556
  - Without the DBD-MySQL with PPM 556
  - Using PPM with Linux 558
  - Installing the DBD::mysql Driver from CPAN 558
- 15.4.2 The DBI Class Methods 558
- 15.4.3 How to Use DBI 560
- 15.4.4 Connecting to and Disconnecting from the Database 561
  - The connect() Method 561
  - The disconnect() Method 563
- 15.4.5 Preparing a Statement Handle and Fetching Results 563
  - Select, Execute, and Dump the Results 563
  - Select, Execute, and Fetch a Row as an Array 564
  - Select, Execute, and Fetch a Row As a Hash 566
- 15.4.6 Getting Error Messages 567
  - Automatic Error Handling 567
  - Manual Error Handling 567
  - Binding Columns and Fetching Values 569
- 15.4.7 The ? Placeholder and Parameter Binding 571
  - Binding Parameters in the execute Statement 571
  - Binding Parameters and the bind_param() Method 574
- 15.4.8 Handling Quotes 576
- 15.4.9 Cached Queries 577

### 15.5 Statements That Don't Return Anything 579

- 15.5.1 The do() Method 579
  - Adding Entries 579
  - Deleting Entries 580
  - Updating Entries 581

### 15.6 Transactions 583

- 15.6.1 Commit and Rollback 583
- 15.6.2 Perl DBI, the Web, and the Dancer Framework 585
- 15.7 What’s Left? 590
- 15.8 What You Should Know 591
- 15.9 What’s Next? 591
- EXERCISE 15 Practicing Queries and Using DBI 592

## 16 Interfacing with the System 595

- 16.1 System Calls 595
  - 16.1.1 Directories and Files 597
    - Backslash Issues 597
    - The File::Spec Module 598
  - 16.1.2 Directory and File Attributes 599
    - UNIX 599
    - Windows 600
  - 16.1.3 Finding Directories and Files 603
  - 16.1.4 Creating a Directory—The mkdir Function 605
    - UNIX 605
    - Windows 605
  - 16.1.5 Removing a Directory—The rmdir Function 607
  - 16.1.6 Changing Directories—The chdir Function 607
  - 16.1.7 Accessing a Directory via the Directory Filehandle 608
    - The opendir Function 609
    - The readdir Function 609
    - The closedir Function 610
    - The telldir Function 611
    - The rewinddir Function 611
    - The seekdir Function 611
  - 16.1.8 Permissions and Ownership 612
    - UNIX 612
    - Windows 612
    - The chmod Function (UNIX) 614
    - The chmod Function (Windows) 614
    - The chown Function (UNIX) 615
    - The umask Function (UNIX) 616
  - 16.1.9 Hard and Soft Links 616
    - UNIX 616
    - Windows 617
    - The link and unlink Functions (UNIX) 618
    - The symlink and readlink Functions (UNIX) 619
  - 16.1.10 Renaming Files 620
    - The rename Function (UNIX and Windows) 620
  - 16.1.11 Changing Access and Modification Times 620
    - The utime Function 620
  - 16.1.12 File Statistics 621
    - The stat and lstat Functions 621
  - 16.1.13 Packing and Unpacking Data 624

- 16.2 **Processes** 629
  - 16.2.1 UNIX Processes 629
  - 16.2.2 Win32 Processes 631
  - 16.2.3 The Environment (UNIX and Windows) 632
  - 16.2.4 Processes and Filehandles 634
    - Login Information—The getlogin Function 635
    - Special Process Variables (pid, uid, euid, gid, egid) 635
    - The Parent Process ID—The getppid Function and the $$ Variable 635
    - The Process Group ID—The getpgrp Function 636
  - 16.2.5 Process Priorities and Niceness 637
    - The getpriority Function 637
    - The setpriority Function (nice) 637
  - 16.2.6 Password Information 638
    - UNIX 638
    - Windows 639
    - Getting a Password Entry (UNIX)—The getpwent Function 641
    - Getting a Password Entry by Username—The getpwnam Function 642
    - Getting a Password Entry by uid—The getpwuid Function 643
  - 16.2.7 Time and Processes 643
    - The Time::Piece Module 644
    - The times Function 645
    - The time Function (UNIX and Windows) 646
    - The gmtime Function 646
    - The localtime Function 648
  - 16.2.8 Process Creation UNIX 649
    - The fork Function 649
    - The exec Function 652
    - The wait and waitpid Functions 653
    - The exit Function 654
  - 16.2.9 Process Creation Win32 654
    - The start Command 654
    - The Win32::Spawn Function 655
    - The Win32::Process Module 656

- 16.3 **Other Ways to Interface with the Operating System** 658
  - 16.3.1 The *syscall* Function and the *h2ph* Script 658
  - 16.3.2 Command Substitution—The *Backquotes* 659
  - 16.3.3 The *Shell.pm* Module 660
  - 16.3.4 The *system* Function 661
  - 16.3.5 Globbing (Filename Expansion and Wildcards) 663

- 16.4  Error Handling 664
  - 16.4.1  The Carp Module 665
    - The die Function 665
    - The warn Function 666
  - 16.4.2  The eval Function 666

- 16.5  Signals and the %SIG Hash 669
  - 16.5.1  Catching Signals 669
  - 16.5.2  Sending Signals to Processes 670
    - The kill Function 670
    - The alarm Function 671
    - The sleep Function 672
  - 16.5.3  Attention, Windows Users! 672

- 16.6  What You Should Know 673

- EXERCISE 16  Interfacing with the System 674

## A Perl Built-ins, Pragma, Modules, and the Debugger 675

- A.1  Perl Functions 675
- A.2  Special Variables 705
- A.3  Perl Pragma 708
- A.4  Perl Modules 710
- A.5  Command-Line Switches 716
- A.6  Debugger 718
  - A.6.1  Getting Information About the Debugger 718
  - A.6.2  The Perl Debugger 718
  - A.6.3  Entering and Exiting the Debugger 719
  - A.6.4  Debugger Commands 720

## B SQL Language Tutorial 723

- B.1  What Is SQL? 723
  - B.1.1  Standardizing SQL 724
    - Executing SQL Statements 724
    - The MySQL Query Browser 725
  - B.1.3  About SQL Commands/Queries 725
    - English-Like Grammar 725
    - Semicolons Terminate SQL Statements 726
    - Naming Conventions 727
    - Reserved Words 727
    - Case Sensitivity 727
    - The Result Set 728
  - B.1.4  SQL and the Database 728
    - The show databases Command 728
    - The USE Command 729
  - B.1.5  SQL Database Tables 729
    - The SHOW and DESCRIBE Commands 730

- B.2  SQL Data Manipulation Language (DML) 731
  - B.2.1  The SELECT Command 731
    - Select Specified Columns 732
    - Select All Columns 732
    - The SELECT DISTINCT Statement 733
    - Limiting the Number of Lines in the Result Set with LIMIT 734
    - The WHERE Clause 736
    - Using Quotes 737
    - Using the = and <> Operators 737
    - What Is NULL? 737
    - The > and < Operators 739
    - The AND and OR Operators 740
    - The LIKE and NOT LIKE Conditions 741
    - Pattern Matching and the % Wildcard 741
    - The _ Wildcard 743
    - The BETWEEN Statement 743
    - Sorting Results with ORDER BY 744
  - B.2.2  The INSERT Command 745
  - B.2.3  The UPDATE Command 746
  - B.2.4  The DELETE Statement 747

- B.3  SQL Data Definition Language 748
  - B.3.1  Creating the Database 748
  - B.3.2  SQL Data Types 749
  - B.3.3  Creating a Table 751
  - B.3.4  Creating a Key 753
    - Primary Keys 753
    - Foreign Keys 755
  - B.3.5  Relations 756
    - Two Tables with a Common Key 756
    - Using a Fully Qualified Name and a Dot to Join the Tables 757
    - Aliases 758
  - B.3.6  Altering a Table 759
  - B.3.7  Dropping a Table 761
  - B.3.8  Dropping a Database 761

- B.4  SQL Functions 761
  - B.4.1  Numeric Functions 762
    - Using GROUP BY 763
  - B.4.2  String Functions 765
  - B.4.3  Date and Time Functions 766
    - Formatting the Date and Time 767
    - The MySQL EXTRACT Command 769

- B.5 Appendix Summary 770
- B.6 What You Should Know 770
- EXERCISE B Do You Speak My Language? 771

## C Introduction to Moose (A Postmodern Object System for Perl 5) 775

- C.1 Getting Started 775
- C.2 The Constructor 776
- C.3 The Attributes 776
  - C.3.1 The has Function 777
  - C.3.2 Before and After Moose Examples 778
  - C.3.3 Moose Types 781
  - C.3.4 Example Using Moose and Extensions 785
  - C.3.5 Example Using Inheritance with Moose 791
- C.4 What About Moo? 795
- C.5 Appendix Summary 796
- C.6 References 796

## D Perlbrew, CPAN, and cpanm 797

- D.1 CPAN and @INC 797
  - D.1.1 Finding Modules 798
  - D.1.2 Using Modules 798
    - I Already Have It! 799
  - D.1.3 Package Manager 800
  - D.1.4 Manually: CPAN 801
    - local::lib 801
- D.2 cpanm 802
- D.3 Perlbrew 803
- D.4 Caveats: C Dependencies 805
- D.5 Windows 806

## E Dancing with Perl 807

- E.1 A New Dancer App 808
  - E.1.1 Verbs 811
  - E.1.2 Templating 814
  - E.1.3 Parameters 818
  - E.1.4 POST 826
- EXERCISE E May I Have This Dance? 829

## Index 831
