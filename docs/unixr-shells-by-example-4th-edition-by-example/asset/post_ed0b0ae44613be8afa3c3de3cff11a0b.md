
14.6.4 The until Command 910
14.6.5 The select Command and Menus 912
14.6.6 Looping Control Commands 917
The shift Command 917
The break Command 919
The continue Command 920
Nested Loops and Loop Control 921
14.6.7 I/O Redirection and Subshells 923
Redirecting the Output of a Loop to a File 923
Piping the Output of a Loop to a UNIX/Linux Command 925
14.6.8 Running Loops in the Background 925
14.6.9 The IFS and Loops 926
14.7 Functions 927
14.7.1 Unsetting Functions 928
14.7.2 Exporting Functions 928
14.7.3 Function Arguments and the Return Value 929
Arguments 929
The Built-In local Function 929
The Built-In return Function 929
14.7.4 Functions and the source (or dot) Command 932
Storing Functions 932
14.8 Trapping Signals 935
14.8.1 Resetting Signals 937
14.8.2 Ignoring Signals 938
14.8.3 Listing Traps 938
14.8.4 Traps and Functions 940
14.9 Debugging 941
14.10 The Command Line 943
14.10.1 Processing Command-Line Options with getopts 943
Sample getopts Scripts 944
Special getopts Variables 947
14.10.2 The eval Command and Parsing the Command Line 949
14.11 bash Options 951
14.11.1 Shell Invocation Options 951
14.11.2 The set Command and Options 953
14.11.3 The shopt Command and Options 955
14.12 Shell Built-In Commands 957
Lab 54: bash Shell—First Script 959
Lab 55: Command-Line Arguments 960
Lab 56: Getting User Input 960
Lab 57: Conditional Statements 961
Lab 58: Conditionals and File Testing 962
Lab 59: The case Statement 962
Lab 60: Loops 964
Lab 61: Functions 965

## 15 Debugging Shell Scripts 967

- 15.1 Introduction 967
- 15.2 Style Issues 967
- 15.3 Types of Errors 968
- 15.3.1 Runtime Errors 969
- 15.3.2 Naming Conventions 969
- 15.3.3 Insufficient Permissions 970
- 15.3.4 Path Problems 970
- 15.3.5 The Shbang Line 972
- 15.3.6 Sneaky Aliases 973
- 15.4 Probable Causes for Syntax Errors 975
- 15.4.1 Undefined and Misspelled Variables 975
- 15.4.2 Incomplete Programming Statements 976
- Missing Keywords 976
- Indentation 976
- if/endif Errors 977
- case and switch Errors 978
- Looping Errors 979
- Operator Errors 981
- Misusing an Operator 982
- Quoting Errors 983
- Quoting Metacharacters 983
- What You Should Know About Quotes 985
- Problems with the here document 989
- File-Testing Errors 990
- 15.4.3 Common Error Messages from the Big 5 Shells 991
- Common C/TC Shell Error Messages 992
- Common Bourne Shell Error Messages 994
- Common Korn Shell Error Messages 996
- Common Bash Error Messages 999
- 15.4.4 Logic Errors and Robustness 1001
- Logical Operator Errors 1001
- Relational Operator Errors 1002
- Branching Errors 1003
- Exit Status with an if Conditional 1004
- Lacking Robustness 1005
- 15.5 Tracing with Shell Options and the set Command 1009
- 15.5.1 Debugging Bourne Shell Scripts 1009
- Bourne Shell Debugging Options 1009
- 15.5.2 Debugging C/TC Shell Scripts 1011
- 15.5.3 Debugging Korn Shell Scripts 1014

### 15.5.4 Debugging Bash Scripts 1016

Bash Invocation Options 1017

The set Command and Options 1018

The shopt Command and Options 1020

15.6 Summary 1021

## 16 The System Administrator and the Shell 1023

16.1 Introduction 1023

16.2 The Superuser 1023

16.3 Becoming a Superuser with the su Command 1024

16.3.1 Running Scripts As Root 1027

Running a Script in the Current Directory 1027

16.3.2 Scripts That Run As Root (setuid Programs) 1029

16.4 Boot Scripts 1030

16.4.1 A Little Terminology 1031

The Kernel and init 1031

What Is a Run Level? 1031

Single-User Mode 1033

Boot Scripts 1034

What Is a Daemon? 1035

16.4.2 An Example Boot Script—The cron Utility 1035

Creating a cron Instruction File (crontab File) 1035

The cron Boot Script 1037

16.4.3 Writing a Portable Script 1041

16.4.4 User-Specific Initialization Files 1044

Possible Files for /etc/skel 1045

16.4.5 System-Wide Initialization Files 1046

/etc/profile 1047

/etc/bashrc 1049

/etc/csh.login 1050

/etc/csh.cshrc 1051

16.5 Summary 1053

## A Useful UNIX/Linux Utilities for Shell Programmers 1055

## B Comparison of the Shells 1103

B.1 The Shells Compared 1103

B.2 tcsh versus csh 1104

B.3 bash versus sh 1104

Index 1113
