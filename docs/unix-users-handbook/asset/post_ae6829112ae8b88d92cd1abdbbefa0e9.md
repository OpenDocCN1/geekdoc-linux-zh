
## Understanding Computer Programs
943

### Compiled vs. Interpreted Languages
944

### Programming Constructs
947

- Assignment 948
- Mathematical Operators 948
- Comparison Expressions 949
- Loops 949
- Choice 952

### Data Structures
954

### Programming Design
955

### The Next Step: Object-Oriented Method and Design
959

- Extendibility 959
- Reusability 960
- Reliability 960

### Procedural Paradigm
962

### Object-Oriented Paradigm
963

- Encapsulation 964
- Inheritance 967
- Polymorphism 970

### How to Design for Object-Oriented Languages
972

### Development Life Cycle
973

- Analysis Phase 974
- Development Phase 974
- Test Phase 975

### SCCS - Source Code Control System
976

- SCCS Revision Versioning 978
- SCCS Commands 980

## C and C++ - The History
984

## C and C++ - Compilers
985

## Compiling Programs
986
- Compiler Options 988

## C and C++ - Make Utility
990
- Makefiles 990
    - Targets and Dependencies 991

## C and C++ - Debugging
998

## C Language
999

### Format of a C Program
1002
- Good Programming Practices 1002
- Comments 1003
- Uppercase and Lowercase 1003

### C Language Nuts and Bolts
1004
- Standard Library 1004
- Constants 1005
- Symbolic Constants 1005
- Escape Sequences 1006
- Data Types 1007

## C++ Language
1067

### C++ Basics
1068
- Enhancements 1068
- New Features of C++ 1072
- More Data Types and Operators 1075

## Internet Programming Basics
1096

### Internet Basics
1096

## Java
1107
- Introduction 1107
- Architecture Independence 1108
- The Java Platform 1110
- Java vs. C and C++ 1112
- Java Environment 1113

## Manual Pages of Some Commands Used in Chapter 14
1128
- make 1129
- sccs 1142

# UNIX and Windows NT Interoperability Section

## CHAPTER 15 The X Window System
1147
- Interoperability Topics 1147
- Why the X Window System? 1150
- X Window System Background 1150
- X Server Software 1152

## CHAPTER 16 Networking
1165
- Why Cover Interoperability? 1165
- TCP/IP Networking Background 1166
- Internet Protocol (IP) Addressing 1170
- NFS Background 1173
- Using Windows and UNIX Networking 1175
- File Transfer Protocol (FTP) 1187
- Other Connection Topics 1193

## CHAPTER 17 Advanced Server for UNIX
1199
- Windows Functionality on UNIX 1199
- Installing Advanced Server/9000 on UNIX 1202
- Sharing a Printer 1209
- Sharing a File System 1212

## CHAPTER 18 Services for UNIX (SFU)
1217
- Introduction to SFU 1217
- Using the Network File System (NFS) Functionality of SFU 1217
- Telnet Client 1231
- Telnet Server 1232
- UNIX Utilities 1233
- NFS Server 1235
- Password Synchronization 1241

## CHAPTER 19 The Windows Command Line: NET Commands, POSIX Utilities, and Others
1243
- Introduction for UNIX System Administrators 1243
- The Windows Command Line 1244
- NET Commands 1244
    - NET ACCOUNTS 1248
    - NET COMPUTER 1251
    - NET CONFIG SERVER 1252
    - NET CONTINUE 1253
    - NET FILE 1256
    - NET GROUP 1257
    - NET HELP 1260
    - NET HELPMSG 1262
    - NET LOCALGROUP 1263
    - NET NAME 1265
    - NET PAUSE 1266
    - NET PRINT 1269
    - NET SEND 1270
    - NET SESSION 1272
    - NET SHARE 1273
    - NET START 1276
    - NET STATISTICS 1278
    - NET STOP 1280
    - NET TIME 1281
    - NET USE 1282
    - NET USER 1284
    - NET VIEW 1286
- POSIX Utilities 1287
    - cat 1290
    - chmod 1292
    - cp 1294
    - find 1295
    - grep 1296
    - ls 1297
    - mkdir 1301
    - mv 1302
    - rm 1303
    - touch 1304
    - wc 1305
- Additional Commands 1306
    - Networking Commands 1306
    - Permissions with cacls 1311
    - Command-Line Backup 1313
    - NTBACKUP 1314
    - AT 1316

# CHAPTER 20 SAMBA
1319
- Samba Overview 1319
    - Setup 1320
    - Using Shares 1328
    - Additional Samba Topics 1330
- Samba Web Configuration Tool (SWAT) 1330
    - Log Files 1335
    - File Name Mangling 1336
    - User Issues 1338
    - Samba Utilities and Programs 1339
    - Obtaining Samba 1340

# INDEX
1343

# FOREWORD

UNIX has evolved from its rather inconspicuous beginnings in a research and development environment to immense popularity in the Internet community. It is always amazing to step back and realize how much something has changed. Fortunately, in computing, this doesn't take long. The Unix operating system progressed from R&D through uses within select major industries to the Internet. Today's UNIX options for a computer system include a wide range of products, from utilizing a UNIX command set on non-UNIX systems, through various Linux distributions, to the different variants of UNIX, including HP-UX, Solaris, and AIX. Understanding the processes and procedures of the UNIX operating system has never been more important or necessary. Whether you are an administrator or user, beginning or experienced, the concepts and implementations of UNIX and Linux systems have become essential knowledge in today's computer-oriented world.

Many books, software, and advertisements refer to a "basic knowledge" of UNIX without defining it. Because it is always easier to relate to a known quantity (also called "the bird in the hand is worth two in the bush" theory), here is my definition of basic UNIX knowledge. A user with a fundamental understanding of UNIX should know: the structure of UNIX, how to log in and log off, the commands required to move from one directory to another (and back again), an editor, some shell commands, Internet basics, an electronic mail program, the principles of shell scripting, and a little C. However, because a little knowledge is like eating one potato chip, most readers and users find that reading and learning more about UNIX is not only an accomplishment, but also an enjoyable experience.

Coupled with the necessity for knowledge is the demand for documentation. Some documentation unfortunately resembles the User Guide to your VCR. It tells you something, but you aren't quite sure what. A good computer book can be easily identified. It not only illustrates the concepts you are trying to learn, but also furnishes the ideas and information you'll want in six months. An excellent book can also be used as a reference guide as you learn. The UNIX User's Handbook demonstrates the requisite structure of the UNIX operating system and its accompanying commands. It also details three shell environments, the vi editor, data manipulation tools, a thorough chapter on Common Desktop Environment (CDE), and an elaborate Software Development chapter. It surveys issues related to administration, development, and performance through examples employing several UNIX variants, including Linux. For easy reference, many chapters conclude with the manual pages for commands introduced within that chapter. A vi reference card is also provided as an additional quickly accessed resource. This is a book that can be an aid to both the beginning and the experienced user and administrator.

The UNIX User's Handbook provides the reader with the opportunity to learn UNIX from an experienced UNIX professional and an excellent author. I have read (and reviewed) most of Marty Pontiatowski's books. He has a flair for making complex procedures completely understandable, especially for the beginner. When I review a book, I look for logical organization, content, readability, examples, and enthusiasm. There is no substitute for enthusiasm; it is thankfully contagious. An author's enthusiasm can inspire readers to unexpected achievements. All authors try to write the book they wish had existed when they were beginning. Mr. Pontiatowski succeeds.

Elizabeth Zinkann
Contributing Editor and Review Columnist for Sys Admin Magazine

# PREFACE

Since its inception, UNIX® has been viewed as requiring a certain amount of "magic" to understand. Nothing could be further from the truth. Like all operating systems most UNIX commands are simple and easy to use. There are also powerful UNIX commands, to which every user has access, that you will find indispensable once you master them.

That proficiency is, in fact, what I wish to accomplish in this book. Cover all UNIX commands and tools that a new UNIX user needs to know in order to become quickly proficient with UNIX, going from the beginner level of UNIX proficiency to the intermediate level.

I could never tell you everything you need to know about UNIX in just one book. I do, however, cover every essential command and tool to get you started quickly with UNIX. If you take a few seconds to look at the upcoming table of contents, I think that you’ll see that I’ve included every essential UNIX topic to help you gain an understanding of UNIX.

You may very well find that you’ll need additional resources as your UNIX knowledge grows. All top UNIX suppliers offer training courses in a variety of forms. In addition, the manuals of the top UNIX suppliers are extensive and cover many topics in great depth. And, of course, there are
