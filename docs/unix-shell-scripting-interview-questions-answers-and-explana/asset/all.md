![](cover.jpg)

![cover](cover.jpg)

UNIX Shell Scripting

Interview Questions:

UNIX Shell Scripting Questions, Answers and Explanations

by Terry Sanchez-Clark

UNIX Shell Scripting Interview Questions and Answers

978-1-4657-4397-8

Smashwords Edition

by Terry Sanchez-Clark

edited by Emilee Newman Bowles

Copyright© 2007 Equity Press and itcookbook.com all rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording or otherwise) without either the prior written permission of the publisher or a license permitting restricted copying in the United States or abroad.

The scanning, uploading and distribution of this book via the internet or via any other means with the permission of the publisher is illegal and punishable by law. Please purchase only authorized electronic editions, and do not participate in or encourage piracy of copyrighted materials.

The programs in this book have been included for

instructional value only. They have been tested with

care but are not guaranteed for any particular purpose.

The publisher does not offer any warranties or

representations not does it accept any liabilities with

respect to the programs.

Trademarks: All trademarks are the property of their respective owners. Equity Press is not associated with any product or vendor mentioned in this book.

www.itcookbook.com

Table of Contents

[INTRODUCTION](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_002.html_introduction)

[BASIC QUESTIONS & ANSWERS](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_004.html_Basic)

[Question 01 Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_005.html_q1)

[Question 02 Invoking Shell Scripts](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_005.html_q2)

[Question 03 Language Constructs](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_005.html_q3)

[Question 04 Shells](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_005.html_q4)

[Question 05 Learning Shell Scripting](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_006.html_q5)

[Question 06 UNIX Filenames](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_006.html_q6)

[Question 07 Strange UNIX Command Name](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_007.html_q7)

[Question 08 Rename "*.foo" to "*.bar"](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_011.html_q8)

[Question 09 Reading Characters from the Terminal](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_011.html_q9)

[Question 10 Set an Environment Variable Inside Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_011.html_q10)

[Question 11 Ring the Terminal Bell During a Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_011.html_q11)

[Question 12 Calendar Produce the Wrong Output](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_012.html_q12)

[Question 13 Print Environment Variables](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_013.html_q13)

[Question 14 Welcome Users as They Log-in](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_014.html_q14)

[Question 15 Display Subdirectories](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_015.html_q15)

[Question 16 Difference Between Two Syntax](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_016.html_q16)

[Question 17 Extracting Usernames](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_017.html_q17)

[Question 18 Remove Blanks at the End of String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_017.html_q18)

[Question 19 Run a Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_018.html_q19)

[Question 20 Simple Explanation About xargs](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_018.html_q20)

[Question 21 Get Return Value](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_019.html_q21)

[Question 22 Assistance with Merge Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_020.html_q22)

[Question 23 Finding Substrings](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_020.html_q23)

[Question 24 Writing Scripts](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_020.html_q24)

[Question 25 Merging Columns from Different Files](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_q25)

[Question 26 Remove Duplicate Lines in File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_q26)

[Question 27 Reverse and Trim a String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_q27)

[Question 28 Transposing Data](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_q28)

[Question 29 Test for Bad Numbers](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_021.html_q29)

[Question 30 Remove Comma within Quotation Marks](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_022.html_q30)

[INTERMEDIATE QUESTIONS & ANSWERS](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_023.html_intermediate)

[Question 31 Search and Replace](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_024.html_q31)

[Question 32 “Read in a While” Loop](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_025.html_q32)

[Question 33 Shell Script Functions](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_026.html_q33)

[Question 34 Execute a Script for Each Logout](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_027.html_q34)

[Question 35 Calling Script1 from Inside of Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_q35)

[Question 36 Deleting Lines from a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_q36)

[Question 37 File Size Checking](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_028.html_q37)

[Question 38 Modify Log File Timestamp](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_029.html_q38)

[Question 39 Correct Usage of Input](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_030.html_q39)

[Question 40 First Occurrence of a Timestamp within a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_031.html_q40)

[Question 41 Backup Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_032.html_q41)

[Question 42 Find Command Exec Error](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_033.html_q42)

[Question 43 Remove the File Extension from File Name](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_034.html_q43)

[Question 44 Retain Blank Spaces](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_035.html_q44)

[Question 45 Hide Password](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_036.html_q45)

[Question 46 Stored Procedure](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_037.html_q46)

[Question 47 Checking Exit Status](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_038.html_q47)

[Question 48 Separating Filenames](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_039.html_q48)

[Question 49 Extract a String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_039.html_q49)

[Question 50 Splitting a String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_040.html_q50)

[Question 51 Searching the Line + Next 20 Lines](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_040.html_q51)

[Question 52 Number and Name of Records in a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_041.html_q52)

[Question 53 Merging Columns from Different Files](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_042.html_q53)

[Question 54 Formatting a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_042.html_q54)

[Question 55 File Comparison](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_043.html_q55)

[Question 56 Include "$" in a String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_043.html_q56)

[Question 57 Deleting the Empty File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_043.html_q57)

[Question 58 Copy Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_043.html_q58)

[Question 59 Parsing a String in a Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_043.html_q59)

[Question 60 Replace All Occurrences of a String](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_045.html_q60)

[Question 61 Replace Character Occurrences](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_045.html_q61)

[Question 62 Passing Parameters to Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_q62)

[Question 63 Schedule Script without Using cron](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_046.html_q63)

[Question 64 Get Current User](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_047.html_q64)

[Question 65 String Substitution](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_048.html_q65)

[Question 66 Read a Specific Line](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_049.html_q66)

[Question 67 Server or Environment Determination](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_q67)

[Question 68 Timer](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_q68)

[Question 69 Dynamic Variable Evaluation](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_q69)

[Question 70 Eliminate Duplicates from a Long List](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_q70)

[Question 71 Crontab Relative Path](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_050.html_q71)

[Question 72 Security Work Around](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_051.html_q72)

[Question 73 Renaming Multiple Files](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_051.html_q73)

[Question 74 Traverse and Download](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_051.html_q74)

[Question 75 Output a Specific Line in a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_q75)

[Question 76 About Kill Command](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_q76)

[Question 77 Calling Shell Script with * as a Parameter](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_052.html_q77)

[Question 78 Extract a Section of Text in File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_053.html_q78)

[Question 79 Run UNIX in a New Shell Inside a Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_054.html_q79)

[Question 80 String Replacement Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_055.html_q80)

[Question 81 UNIX Script Issues](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_055.html_q81)

[Question 82 Split a Document](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_056.html_q82)

[Question 83 Exit Shell Script from Function](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_057.html_q83)

[Question 84 Search Multiple String Occurrences](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_057.html_q84)

[Question 85 Search/Copy Records](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_058.html_q85)

[ADVANCED QUESTIONS & ANSWERS](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_059.html_advanced)

[Question 86 Menu Considerations](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_060.html_q86)

[Question 87 Finding the Last Row](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_061.html_q87)

[Question 88 Catching All Exit Codes](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_062.html_q88)

[Question 89 Converting Text File into XML](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_063.html_q89)

[Question 90 Back Up Log Files](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_063.html_q90)

[Question 91 Stop Simultaneous Execution of the Same Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_064.html_q91)

[Question 92 Displaying Script Command with Output](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_064.html_q92)

[Question 93 Build Text File with Calendar Dates](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_064.html_q93)

[Question 94 grep in a Loop](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_065.html_q94)

[Question 95 Generating a List of Choices in a Menu](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_065.html_q95)

[Question 96 Delete Empty Files in a Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_065.html_q96)

[Question 97 Replace a Line in a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_066.html_q97)

[Question 98 Shrinking a File](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_066.html_q98)

[Question 99 awk in Shell Script](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_067.html_q99)

[Question 100 while Loop](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_067.html_q100)

[Acknowledgements](#tmp_ed5c9b94b54b2e388d079425315fd245_4HOK8o.ch.fixed.fc.tidied.stylehacked.xfixed_split_068.html_acknowledgements)

Introduction

UNIX shell, also called "the command line," provides the traditional user interface for the UNIX operating system. Users direct the operation of the computer by entering command input as text for a shell to execute. Within the Microsoft Windows suite of operating systems the analogous program is command.com or cmd.exe for Windows NT-based operating systems.

In the most generic sense of the term, shell means any program that users use to type commands. Since in the UNIX operating system users can select which shell they want to use (which program should execute when they login), many different shells have been developed. It is called a "shell" because it hides the details of the underlying operating system behind the shell's interface (contrast "kernel" which refers to the lowest-level or “inner-most” component of an operating system). Similarly, graphical user interfaces for UNIX, such as GNOME and KDE, are sometimes called visual shells or graphical shells. By itself, the term shell is usually associated with the command line. In UNIX, any program can be the user's shell. Users who want to use a different syntax for typing commands can specify a different program as their shell.

The term shell also refers to a particular program, namely the Bourne shell, sh. The Bourne shell was the shell used in early versions of UNIX and became a de facto standard; every Unix-like system has the equivalent of the Bourne shell. The Bourne shell program is located in the UNIX file hierarchy at /bin/sh. On some systems, such as BSD, /bin/sh is a Bourne shell or equivalent, but on other systems such as Linux, /bin/sh is likely to be a link to a compatible, but more feature-rich shell, such as Bash. POSIX specifies the standard shell as a strict subset of the Korn shell.

The UNIX shell was unusual when first created, since it is both an interactive command language and the language used to script the system; it is a scripting programming language. Many shells created for other operating systems since offer rough equivalents to UNIX shell functionality.

On systems using a windowing system, some users may never use the shell directly, though on UNIX systems, the shell is still the implementation language of system startup scripts, including the program that starts the windowing system, the program that dials into the Internet, and many other essential functions.

On MS-DOS, OS/2, and Windows, equivalents to UNIX system scripts are called batch files, and have either a ".bat" or ".cmd" extension. A newer CLI, code named Monad and to be released as the Windows PowerShell, will replace the existing NT command line, cmd.exe; it has many features derived from UNIX shells, though it uses a somewhat different syntax.

Many regular users of a UNIX system still find a modern command line shell much more convenient for many tasks than any GUI application.

Due to the recent movement in favor of open source, most UNIX shells have at least one version that is open source.

BASIC QUESTIONS AND ANSWERS:

Questions most likely to be asked by beginners

Question 01: Shell Script

What is shell script anyway?

A: A shell script, in its most basic form, is simply a collection of operating system commands put into a text file in the order they are needed for execution. Using any of the shells mentioned so far, a text file containing the commands listed in example basic shell script would work every time the script was executed.

Example basic shell script:

#!/bin/sh

rm -f /tmp/listing.tmp> /dev/null 2>&1

touch /tmp/listing.tmp

ls -l [a-z]*.doc | sort> /tmp/listing.tmp

lpr -Ppostscript_1 /tmp/listing.tmp

rm -f /tmp/listing.tmp

Of course, not all scripts are this simple but it does show that ordinary UNIX commands can be used without any extra, fancy scripting constructs. If this script was executed any number of times the result would be the same, a long listing of all the files starting with lower case letters and ending with a doc extension from the current directory printed out on your local PostScript printer. Let’s start to look at this in detail starting at the beginning.

In the Beginning:

The first line of any script should always look a bit like the top line in the example basic shell script; the only difference would be the path leading to the shell executable file, in this case the /bin/sh part. By default, the UNIX system will attempt to execute an ASCII text file

if the files name is supplied as the first argument on the command line. UNIX will attempt to execute the file in the current shell and try to process the included command strings within the file using the syntax rules of the current shell. So, if you are using the Bourne Shell as your default environment and the ASCII file contains a list of UNIX command structures formatted how the Bourne Shell likes them to be formatted, all will work fine. However, if you try and execute a C Shell file with a different syntax structure, the Operating System will complain about unrecognized commands and syntax errors. The reason is no one told the Operating System that it was a C Shell file, so it processed it as a Bourne Shell. The correct way to indicate this to the Operating System is to pass the script name to the shell executable as an argument thus:

user@system$ /bin/csh my_script arg_1 arg_2

However, it didn't take long for someone to notice that this was extra typing that could well be done away with and hence the short hand first line comment was born.

Basically, all comments in shell scripts start with a hash sign (#). However, for the first line only, UNIX reads past the hash to see what's next. If it finds an exclamation point (!), or Bang! as it's known, then what follows is taken as the path to the shell executable binary program. Not only can that, but all the command line arguments that the shell executable allows also be stacked up on this line. With this feature it doesn't matter what flavor of shell your environment is, you can execute a script in any other flavor of shell, as if it was a real UNIX command. Let’s look at the Bourne Shell syntax rules more closely. It would be helpful at this point to print out the sh man pages from your system so that you can compare them with what I have here.

Question 02: Invoking Shell Scripts

How do you invoke shell scripts?

A: There are two ways to invoke a shell script file.

1\. Direct Interpretation:

In direct interpretation, the command csh filename [arg ...] invokes the program csh to interpret the script contained in the file “filename.”

2\. Indirect Interpretation:

In indirect interpretation, we must insert as the first line of the file:

#! /bin/csh

or

#! /bin/csh -f

There are situations in which this is not necessary, but it won't hurt to have it and the file must be made executable using chmod. Then it can be invoked in the same way as any other command, i.e., by typing the script file name on the command line.

The -f option says that we want fast startup, which it will achieve by not reading or executing the commands in .cshrc. Thus for example, we won't have the “set” values for shell variables or the aliases from that file, but if we don't need them, this will be much faster (if we need a few of them, we can simply add them to the script file itself).

Question 03: Language Constructs

How do you implement a shell script?

A: The shell script language, like other programming languages, has constructs for conditional execution (if-then-else; while), iterative execution (for loop), a switch statement, and a go to statement:

1\. if-then-else:

The syntax of the if-then-else construct is “if” (expr) simple-command

or

if ( expr ) then commandlist-1 [else commandlist-2]

endif

The expression expr will be evaluated and according to its value, the commandlist-1 or the commandlist-2 will be executed. The portion of the construct enclosed in “[” and “]” is optional. This is standard notation in the software world, so remember it.

As an example, suppose we write a shell script which is supposed to have two parameters and that the code will set up two variables, “name1” and “name2” from those two parameters:

set name1 = $argv[1]

set name2 = $argv[2]

(Which presumably it would make use of later on). But suppose we also wish to do error-checking, emitting an error message if the user gives fewer than two, or more than two, parameters. We could use the following code:

if ($#argv <> 2) then

echo "you must give exactly two parameters"

else

set name1 = $argv[1]

set name2 = $argv[2]

endif

2. while:

The syntax of while loop construct is

while ( expr )

commandlist

end

The command list will be executed until the expr evaluates to false.

3\. foreach:

The syntax of foreach loop construct is

foreach var ( worddlist )

commandlist

end

The command list is executed once for each word in the wordlist, and each time the variable var will contain the value of that word. For example, the following script can search all immediate subdirectories of the current directory for a given file (and then quit if it finds one):

#! /bin/csh -f

set f = $1

foreach d (*)

if (-e $d/$f) then

echo FOUND: $d/$f

exit(0)

endif

end

echo $f not found in subdirectories

For example, say I call this script FindImm, and my current directory consists of files s, t and u, with s and t being subdirectories, and with t having a file x.

Typing:

FindImm x

would yield the message

FOUND: t/x

Here is how it works: In the line

foreach d (*)

The “*” is a wild card, so it would expand to a list of all files in my current directory, i.e., the list (s t u). So, the for-loop will first set d = s, then d = t, and finally d = u.

In the line if (-e $d/$f) then the -e means existence; in other words, we are asking if the file $d/$f exists. If we type “FindImm x” as in the example above, $f would be x, and $d would start out as s, so we would be asking if the file s/x exists (the answer would be no).

4\. switch:

The switch command provides a multiple branch similar to the switch statement in C. The general form of switch is:

switch ( str )

case string1:

commandlist1

breaksw

case string2:

commandlist2

breaksw

default

commandlist

endsw

The given string str is successively matched against the case patterns. Control flow is switched to where the first match occurs. As in file name expansion, a case label may be a literal string, or contain variable substitution, or contain wild-card character such as *,?, etc.

5\. Goto:

The goto command provides a way to branch unconditionally to a line identified by a label.

goto lab

where lab is a label on a line (by itself) somewhere in the script in the form lab.

6.  A Shell Script for Deleting Files:

This code, which we will call Del, will delete files like rm does, prompting for your confirmation for each file to be deleted, including directory files (which the -i option of rm won't do).

#! /bin/csh -f

foreach name ($argv)

if ( -f $name ) then

echo -n "delete the file '${name}' (y/n/q)?"

else

echo -n "delete the entire directory '${name}' (y/n/q)? "

endif

set ans = $<

switch ($ans)

case n:

continue

case q:

exit

case y:

rm -r $name

continue

endsw

end

Before reading further, try this program yourself. Set up a test directory, with several files in it, at least one of which is a subdirectory, with at least one file there. Afterwards, you can then type “Del *”

The line:

if ( -f $name ) then

tests to see if the file whose name is in $name is an ordinary file, as opposed to a directory file.

The -n option of echo tells the shell not to print the newline character, so that our answer, y/n/q, will be on the same line.

In the line:

set ans = $<

the symbol $ < means the input from the keyboard.

The keyword “continue” means to go to the top of the enclosing loop.

The -r option of the rm command means that if an argument is a directory, then remove that directory, and all the files and subdirectories within it.

Question 04: Shells

Why should I use Shells?

A: Well, most likely because it’s a simple way to string together a bunch of UNIX commands for execution at any time without the need for prior compilation. Also because it’s generally fast to get a script going. Not forgetting the ease with which other scripters can read the code and understand what is happening. Lastly, they are generally completely portable across the whole UNIX world, as long as they have been written to a common standard.

Question 05: Learning Shell Scripting

Is there a link where I can start learning UNIX scripting and can go online and download the content? I can start with basic Bourne scripting.

A: Try this:

[ ] abs-guide.html.tar.gz 21-Oct-2005 09:28 479k GZIP compressed docume>

[ ] abs-guide.pdb21-Oct-2005 09:28 507k

[ ] abs-guide.pdf21-Oct-2005 09:28 1.8M

[ ] abs-guide.ps.gz 21-Oct-2005 09:28 1.1M GZIP compressed docume>

[ ] abs-guide.txt.gz 21-Oct-2005 09:28 457k GZIP compressed docume>

[DIR] html/ 21-Oct-2005 09:27-

[DIR] images/18-Jul-2000 11:24-

Question 06: UNIX Filenames

Where can I get an explanation of the UNIX filenames and their functions, e.g. /usr, /etc, /var?

A: /: The Root Directory. Under UNIX-like system there is just one unified directory. Everything begins with the root directory. The root directory is symbolized by just a forward slash ("/"), with nothing following it. There are many directories hanging off of the root directory. The contents of the root file system should be adequate to boot, restore, recover, and/or repair the system.

/bin: This contains commands that may be used by both the system administrator and by users, but which are required in single user mode. It may also contain commands which are used indirectly by scripts.

/sbin: Utilities used for system administration and maintenance. (and other root-only commands) are stored in /sbin.

/boot: This is for anything which is used before the kernel execs /sbin/init. This includes saved master boot sectors, sector map files, and anything else that is not directly edited by hand.

/dev: This is where special files are kept. Special files represent input/output (i/o) devices, like a tty (terminal), a disk drive, or a printer. Unix treats such devices as files. /dev also contains a script named MAKEDEV which can create devices as needed. It may also contain a MAKEDEV.local for any local-only devices.

/etc: This is for the system configuration files and directories. Examples are startup scripts configuration files for networking, etc.

/usr: /usr is shareable, read-only data. It maybe shared with other machines with the same architecture and operating system version and most of the root directory structure is mirrored here.

--- /usr/bin: most user commands

--- /usr/local: local software

--- /usr/dict: Word lists

--- /usr/etc: Site-wide system configuration

--- /usr/includes: Directory for standard includes files.

--- /usr/lib: Libraries for programming and packages

--- /usr/man: Manual pages

--- /usr/sbin: Non-essential standard system binaries

--- /usr/share: Architecture-independent data

--- /usr/src: Source code

etc.

/lib: These are used for essential shared libraries and kernel modules.

/proc: This provides information about processes, storage and retrieval of process information as well as other kernel and memory information.

/var: This is used for material which is necessarily per-machine. It contains variable data files. This includes spool directories and files, administrative and logging data.

--- /var/adm: This is used for administrative materials like the system logging and accounting files.

--- /var/log: This contains miscellaneous log files. Most logs should be written to this directory or an appropriate subdirectory.

--- /var/spool: This is traditionally used for machine-local data being spooled to or from UNIX subsystems. Print jobs are spooled here for delivery to the line printer daemon, mail is spooled for delivery to remote systems and UUCP files are spooled for transmission. In-bound mail and news are spooled here for delivery to users and at and cron jobs are spooled for delayed execution by the cron daemon.

/root: This is the home directory for the superuser root. It usually contains things that concern system administration that don't belong in public view, and has read privileges only for the root user and other administration accounts.

/home: This is used for home directories for users. Each user has a username and a directory in /home with that username to use as their home directory. They can place any kind of files there and set up permissions to allow exactly whom they wish to see their data.

/tmp: This is sued for temporary files. The system scratches files that all users write here.

/lost+found: This is used for any pieces of files system can't identify when it cleans up the filesystem(fsck). If you lose some data mysteriously, check here.

/mnt: This is just such a temporary mount point. Sometimes it has subdirectories for the different types of file systems which can be mounted there.

Question 07: Strange UNIX Command Name

What does some strange UNIX command name stand for?

A: awk = "Aho Weinberger and Kernighan"

This language was named by its authors, Al Aho, Peter Weinberger and Brian Kernighan.

grep = "Global Regular Expression Print"

Grep comes from the ed command to print all lines matching a certain pattern; g/re/p where "re" is a "regular expression."

fgrep = "Fixed GREP"

fgrep searches for fixed strings only. The "f" does not stand for "fast." In fact, "fgrep foobar *.c" is usually slower than "egrep foobar *.c" (Yes, this is kind of surprising. Try it.)

Fgrep still has its uses though, and may be useful when searching a file for a larger number of strings than egrep can handle.

egrep = "Extended GREP"

egrep uses fancier regular expressions than grep. Many people use egrep all the time, since it has some more sophisticated internal algorithms than grep or fgrep, and is usually the fastest of the three programs.

cat = "CATenate"

Catenate is an obscure word meaning "to connect in a series." This is what the "cat" command does to one or more files. Not to be confused with C/A/T, the Computer Aided Typesetter.

gecos = "General Electric Comprehensive Operating Supervisor"

When GE's large systems division was sold to Honeywell, Honeywell dropped the "E" from "GECOS."

Unix's password file has a "pw_gecos" field. The name is a real holdover from the early days. Dennis Ritchie has reported:

"Sometimes we sent printer output or batch jobs to the GCOS machine. The gcos field in the password file was a place to stash the information for the $IDENT card. Not elegant."

nroff = "New ROFF"

troff = "Typesetter new ROFF"

These are descendants of "roff," which was a re-implementation of the Multics "runoff" program (a program that you'd use to "run off" a good copy of a document).

tee = T

This was taken from a plumbing terminology for a T-shaped pipe splitter.

bss = "Block Started by Symbol"

Dennis Ritchie says:

Actually the acronym (in the sense we took it up; it may have other credible etymologies) is "Block Started by Symbol." It was a pseudo-op in FAP (Fortran Assembly [-er?] Program), an assembler for the IBM 704-709-7090-7094 machines. It defined its label and set aside space for a given number of words.

There was another pseudo-op, BES, "Block Ended by Symbol" that did the same except that the label was defined by the last assigned word + 1\. (On these machines Fortran arrays were stored backwards in storage and were 1-origin.)

The usage is reasonably appropriate, because just as with standard Unix loaders, the space assigned didn't have to be punched literally into the object deck but was represented by a count somewhere.

biff = "BIFF"

This command, which turns on asynchronous mail notification, was actually named after a dog at Berkeley.

I can confirm the origin of biff, if you're interested.

Biff was Heidi Stettner's dog, back when Heidi (and I, and Bill Joy) were all grad students at U.C. Berkeley and the early versions of BSD were being developed. Biff was popular among the residents of Evans Hall, and was known for barking at the mailman, hence the name of the command.

This was confirmed, courtesy of Eric Cooper of Carnegie Mellon University.

rc (as in ".cshrc" or "/etc/rc") = "RunCom"

"rc" derives from "runcom," from the MIT CTSS system, ca. 1965.

“There was a facility that would execute a bunch of

commands stored in a file; it was called ‘runcom’ for ‘run commands’ and the file began to be called ‘a runcom.’ ‘rc’ in Unix is a fossil from that usage.”

(Source: Brian Kernighan & Dennis Ritchie, as told to Vicki Brown)

"rc" is also the name of the shell from the new Plan 9 Operating system.

Perl = "Practical Extraction and Report Language"

Perl = "Pathologically Eclectic Rubbish Lister"

The Perl language is Larry Wall's highly popular freely-available completely portable text, process, and file manipulation tool that bridges the gap between shell and C programming (or between doing it on the command line and pulling your hair out).

For further information, see the Usenet newsgroup comp.lang.perl.misc.

Don Libes' book Life with Unix contains lots more of these tidbits.

Question 08: Rename "*.foo" to "*.bar"

How do I rename "*.foo" to "*.bar" or change file names to lowercase?

A: Why doesn't "mv *.foo *.bar" work? Think about how the shell expands wildcards. "*.foo" and "*.bar" are expanded before the mv command ever sees the arguments. Depending on your shell, this can fail in a couple of ways. CSH prints "No match." because it can't match "*.bar". SH executes "mv a.foo b.foo, c.foo *.bar", which will only succeed if you happen to have a single directory named "*.bar" which is very unlikely and almost certainly not what you had in mind.

Depending on your shell, you can do it with a loop to "mv" each file individually. If your system has "basename" you can use:

C Shell:

foreach f ( *.foo )

set base=`basename $f .foo`

mv $f $base.bar

end

Bourne Shell:

for f in *.foo; do

base=`basename $f .foo`

mv $f $base.bar

done

Some shells have their own variable substitution features, so instead of using "basename" you can use simpler loops like:

C Shell:

foreach f ( *.foo )

mv $f $f:r.bar

end

Korn Shell:

for f in *.foo; do

mv $f ${f%foo}bar

done

If you don't have a "basename" or want to do something like renaming foo.* to bar.*, you can use something like "sed" to strip apart the original file name in other ways, but the general looping idea is the same. You can also convert file names into "mv" commands with “sed” and hand the commands off to "sh" for execution. Try:

ls -d *.foo | sed -e 's/.*/mv & &/' -e 's/foo$/bar/' | sh

A program by Vladimir Lanin called "mmv" that does this job nicely was posted to comp.sources.unix (Volume 21, issues 87 and 88) in April 1990\. It lets you use:

mmv '*.foo' '=1.bar'

Shell loops like the above can also be used to translate file names from upper to lower case or vice versa. You could use something like this to rename uppercase files to lowercase:

C Shell:

foreach f ( * )

mv $f `echo $f | tr '[A-Z]' '[a-z]'`

end

Bourne Shell:

for f in *; do

mv $f `echo $f | tr '[A-Z]' '[a-z]'`

done

Korn Shell:

typeset -l l

for f in *; do

l="$f"

mv $f $l

done

If you wanted to be really thorough and handle files with “funny” names (embedded blanks or whatever) you'd need to use:

Bourne Shell:

for f in *; do

g=`expr "xxx$f" : 'xxx\(.*\)' | tr '[A-Z]' '[a-z]'`

mv "$f" "$g"

done

The “expr” command will always print the filename, even if it equals “-n” or if it contains a System V escape sequence like “\c.”

Some versions of "tr" require the [ and ], some don't. It happens to be harmless to include them in this particular example; versions of tr that don't want the [] will conveniently think they are supposed to translate '[' to '[' and ']' to ']'.

If you have the Perl language installed, you may find this rename script by Larry Wall very useful. It can be used to accomplish a wide variety of filename changes.

#!/usr/bin/perl

#

# rename script examples from lwall:

# rename 's/\.orig$//' *.orig

# rename 'y/A-Z/a-z/ unless /^Make/' *

# rename '$_ .= ".bad"' *.f

# rename 'print "$_: "; s/foo/bar/ if <stdin> =~ /^y/i' *

$op = shift;

for (@ARGV) {

$was = $_;

eval $op;

die $@ if $@;

rename($was,$_) unless $was eq $_;

}

Question 09: Reading Characters from the Terminal

How do I read characters from the terminal in a shell script?

A: In sh, use read. It is most common to use a loop like:

while read line

do

done

In csh, use $< like this:

while ( 1 )

set line = "$<"

if ( "$line" == "" ) break

end

Unfortunately, csh has no way of distinguishing between a blank line and an end-of-file.

If you're using sh and want to read a *single* character from the terminal, you can try something like:

echo -n "Enter a character: "

stty cbreak # or stty raw

readchar=`dd if=/dev/tty bs=1 count=1 2>/dev/null`

stty -cbreak

echo "Thank you for typing a $readchar ."

Question 10: Set an Environment Variable Inside Script

How do I set an environment variable, change directory inside a program or shell script and have that change affect my current shell?

A: In general, you can't, at least not without making special arrangements. When a child process is created, it inherits a copy of its parent's variables (and current directory). The child can change these values all it wants but the changes won't affect the parent shell, since the child is changing a copy of the original data.

Some special arrangements are possible. Your child process could write out the changed variables, if the parent was prepared to read the output and interpret it as commands to set its own variables.

Also, shells can arrange to run other shell scripts in the context of the current shell, rather than in a child process, so that changes will affect the original shell.

For instance, if you have a C shell script named "myscript":

cd /very/long/path

setenv PATH /something:/something-else

or the equivalent Bourne or Korn shell script:

cd /very/long/path

PATH=/something:/something-else export PATH

and try to run "myscript" from your shell, your shell will fork and run the shell script in a sub process. The sub process is also running the shell; when it sees the "cd" command it changes *its* current directory, and when it sees the "setenv" command it changes *its* environment, but neither has any effect on the current directory of the shell at which you're typing (your login shell, let's say).

In order to get your login shell to execute the script (without forking) you have to use the "." command (for the Bourne or Korn shells) or the "source" command (for the C shell). For example, you type:

.myscript to the Bourne or Korn shells, or source myscript to the C shell.

If all you are trying to do is change directory or set an environment variable, it will probably be simpler to use a C shell alias or Bourne/Korn shell function.

Question 11: Ring the Terminal Bell During a Shell Script

How do I ring the terminal bell during a shell script?

A: The answer depends on your UNIX version (or rather on the kind of "echo" program that is available on your machine).

A BSD-like "echo" uses the "-n" option for suppressing the final newline and does not understand the octal \nnn notation. Thus the command is:

echo -n '^G'

where ^G means a _literal_ BEL-character (you can produce this in emacs using "Ctrl-Q Ctrl-G" and in vi using "Ctrl-V Ctrl-G").

A SysV-like "echo" understands the \nnn notation and uses \c to suppress the final newline, so the answer is:

echo '\007\c'

Question 12: Calendar Produce the Wrong Output

Why does calendar produce the wrong output?

A: Frequently, people find that the output for the UNIX calendar program, “cal” produces output that they do not expect.

The calendar for September 1752 is very odd:

September 1752

S M Tu W Th F S

01 02 14 15 16

17 18 19 20 21 22 23

24 25 26 27 28 29 30

This is the month in which the US (the entire British Empire actually) switched from the Julian to the Gregorian calendar.

The other common problem people have with the calendar program is that they pass it arguments like “cal 9 94.” This gives the calendar for September of AD 94, NOT 1994.

Question 13: Print Environment Variables

How do I print environment in an easy to read format?

A: Replace a normal environment variable output as in $PATH:

/usr/bin:/usr/ccs/bin:/usr/local/bin:

with:

/usr/bin

/usr/ccs/bin

/usr/local/bin

Use this SIMPLE script:

#! /usr/bin/ksh

IFS=':'

for ii in $PATH

do

echo $ii

done

# end of file

Question 14: Welcome Users as They Log-in

How do I “welcome” users as they log-in to the system?

A: Try the following:

tt=`date +"%T" | cut -c1-2`

NAME=`grep "^$LOGNAME" /etc/passwd | awk -F: ' {print $5}'`

echo "\n\n\n"

tput smso

if [ $tt -gt 0 -a $tt -lt 12 ]

then

echo " $NAME !!!!!! GOOD MORNING !!!!!!"

elif [ $tt -gt 12 -a $tt -le 16 ]

then

echo " $NAME !!!!!!GOOD AFTERNOON !!!!!!"

else

echo " $NAME !!!!!! GOOD EVENING !!!!!!"

fi

tput rmso

Question 15: Display Subdirectories

How can I find subdirectories from the current directory?

A: There are times you can’t remember the name of the subdirectory you want to go to. In the jungle of files and directories it is easier if you could see only the directories.

Put the following function in your environment file:

dir()

{

ls -l |awk '{ if ( substr($1,1,1)== "d") {print}}'

}

Here is an easier command to list sub-directories alone in directories:

ls -l | grep ^d

or

ls -d */

Question 16: Difference Between Two Syntax

What is the difference between these two syntax?:

if (( $lines = 0 ));

and

if [ $lines -eq 0 ];

When do we use the square brackets and when to use the paranthesis?

A: “if [ $lines -eq 0 ]”

This came first. With the old Bourne shell it is all you have. So it works everywhere. But it is not what it seems to be. The if statement runs a command and tests to see if it worked. So you can do stuff like:

if mkdir tmp; then echo mkdir worked; fi

mkdir is just a command and tmp is parameter to mkdir. There is a command called [ and like many commands it takes parameters. It checks its last parameter and gets mad unless it is ]. If the last parameter is a ], it looks at everything else and tries to determine what you are trying to test. If you do:

lines=""

if [ $lines -eq 0 ]

you will have a problem. All that the [ command will see is the -eq and the 0 so it will complain. Because of these concerns, Dave Korn invented syntax. Now you can do:

if [[ $lines = 0 ]]

And it won't get mixed up as easily. Bash has picked this up from ksh and it is a better choice than the single [ most of the time. The idea is that [ might disappear eventually, but I tend to doubt that it will. Still, the official word is that [ is present in ksh to support older scripts and you should switch to [[.

But you asked about "if (($lines = 0 ))." That precise syntax is a terrible mistake and you should probably never use it. First, ksh has built-in arithmetic and you can do stuff like:

((k=7+1)) ; echo $k

and get 8\. The ((expression)) syntax is just a command to do arithmetic. This command has an exit code. If the expression is non-zero, the command succeeds. But if the expression is zero, the command fails. So you can test the result of an expression. I often do stuff like:

if ((lines == 0 ))

which tests if lines are equal to 0\. With (($lines = 0)), assuming that lines contained the name of another variable, it might almost work:

lines=xyz

if (($lines = 0))

$lines would be replaced by xyz, so the shell would see ((xyz = 0)). xyz would set to 0\. ((xyz = 0)) would always fail so the if statement would never be true. You never need to use a $ sign inside ((expression)). This is ok:

((lines=lines+1))

The arithmetic statement will know that line is a variable and will look up the value. Bash has also picked up arithmetic from ksh.

Question 17: Extracting Usernames

How do I use grep to extract users with at least 4 characters in their username? I have tried who | grep \{4,\} but it’s not working.

A: Just continue with your original line of thought. Take note of the spaces.

who | grep "^[^ ]\{4,\} "

Question 18: Remove Blanks at the End of String

I have several fields, some of them are numbers and others are strings. Some of the string fields have several blank spaces at the end, for example:

"string ",123,"one string here ",98777,"hello ","etc "

I need to eliminate the white spaces so I would be able to compare this file with another one generated somewhere else.

So the result should be something like this:

"string",123,"one string here",98777,"hello","etc"

I tried with sed doing this:

sed 's/[ ]*//g' filename > output.txt;

That removes all of the blanks which is not what I need.

How do I remove blanks only at the end of the string?

A: You can do this easily by:

Code:

sed 's/[ ]*"/"/g'

You can drop the square brackets as well. But retain the space.

Code:

sed 's/ *"/"/g'

Question 19: Run a Script

Is there a way to run a script without changing file access permissions?

A: Usually a user has to change the file permissions for a shell script to make it executable, for example:

chmod +x script

Sometimes it's more convenient to just invoke the shell with the script as an argument:

sh script

Question 20: Simple Explanation About xargs

Could you give me a basic understanding or sample use of “xargs”?

A: Quite simply, xargs is used to read strings on standard input, passing as many arguments as possible to a given command. It's normally used to get around the ARG_MAX limitations. 24,576 IBM & 1,048,320 Solaris.

Using the xargs Command

by Ed Schaefer

[http://www.unixreview.com/documents/s=8274/sam0306g/](http://www.unixreview.com/documents/s=8274/sam0306g/)

Many UNIX professionals think the xargs command, construct and execute argument lists, are only useful for processing long lists of files generated by the find command. While xargs dutifully serves this purpose, xargs has other uses. In this article, I describe xargs and the historical "Too many arguments" problem, and present eight xargs "one-liners":

* Find the unique owners of all the files in a directory.

* Echo each file to standard output as it deletes.

* Duplicate the current directory structure to another directory.

* Group the output of multiple UNIX commands on one line.

* Display to standard output the contents of a file one word per line.

* Prompt the user whether to remove each file individually.

* Concatenate the contents of the files whose names are contained in file into another file.

* Move all files from one directory to another directory, echoing each move to standard output as it happens.

Examining the "Too Many Arguments" Problem.

In the early days of UNIX/xenix, it was easy to overflow the command-line buffer, causing a "Too many arguments" failure. Finding a large number of files and piping them to another command was enough to cause the failure. Executing the following command, from Unix Power Tools, first edition (O'Reilly & Associates):

pr -n 'find . -type f -mtime -1 -print'|lpr

This will potentially overflow the command line given enough files. This command provides a list of all the files edited today to pr, and pipes pr's output to the printer. We can solve this problem with xargs:

find . -type f -mtime -1 -print|xargs pr -n |lp

With no options, xargs reads standard input, but only writes enough arguments to standard output as to not overflow the command-line buffer. Thus, if needed, xargs forces multiple executions of pr -n|lp.

While xargs controls overflowing the command-line buffer, the command xargs services may overflow. I've witnessed the following mv command fail—not the command-line buffer—with an argument list too long error:

find ./ -type f -print | xargs -i mv -f {} ./newdir

Limit the number of files sent to mv at a time by using the xargs -l option. (The xargs -i () syntax is explained later in the article). The following command sets a limit of 56 files at time, which mv receives:

find ./ -type f -print | xargs -l56 -i mv -f {} ./newdir

The modern UNIX OS seems to have solved the problem of the find command overflowing the command-line buffer. However, using the find -exec command is still troublesome. It's better to do this:

# remove all files with a txt extension

find . -type f -name "*.txt" -print|xargs rm

than this:

find . -type f -name "*.txt" -exec rm {} \; -print

Controlling the call to rm with xargs is more efficient than having the find command execute rm for each object found.

xargs One-Liners

The find-xargs command combination is a powerful tool. The following example finds the unique owners of all the files in the /bin directory:

# all on one line

find /bin -type f -follow | xargs ls -al | awk ' NF==9 { print $3 }

'|sort -u

If /bin is a soft link, as it is with Solaris, the -follow option forces find to follow the link. The xargs command feeds the ls -al command, which pipes to awk. If the output of the ls -al command is 9 fields, print field 3—the file owner. Sorting the awk output and piping to the unique command ensures unique owners.

You can use xargs options to build extremely powerful commands. Expanding the xargs/rm example, let's assume the requirement exists to echo each file to standard output as it deletes:

find . -type f -name "*.txt" | xargs -i ksh -c "echo deleting {}; rm {}"

The xargs -i option replaces instances of {} in a command (i.e., echo and rm are commands).

Conversely, instead of using the -i option with {}, the xargs -I option replaces instances of a string. The above command can be written as:

find . -type f -name "*.txt" | xargs -I {} ksh -c "echo deleting {}; rm {}"

The new, third edition of Unix Power Tools by Powers et al. provides an xargs "one-liner" that duplicates a directory tree. The following command creates in the usr/project directory, a copy of the current working directory structure:

find . -type d -print|sed 's@^@/usr/project/@'|xargs mkdir

The /usr/project directory must exist. When executing, note the error:

mkdir: Failed to make directory "/usr/project/"; File exists

This doesn't prevent the directory structure creation. Ignore it. To learn how the above command works, you can read more in Unix Power Tools, third edition, Chapter 9.17 (O'Reilly & Associates).

In addition to serving the find command, xargs can be a slave to other commands. Suppose the requirement is to group the output of UNIX commands on one line. Executing:

logname; date

displays the logname and date on two separate lines. Placing commands in parentheses and piping to xargs places the output of both commands on one line:

(logname; date)|xargs

Executing the following command places all the file names in the current directory on one line, and redirects to file "file.ls":

ls |xargs echo > file.ls

Use the xargs number of arguments option, -n, to display the contents of "file.ls" to standard output, one name per line:

cat file.ls|xargs -n1 # from Unix in a Nutshell

In the current directory, use the xargs -p option to prompt the user to remove each file individually:

ls|xargs -p -n1 rm

Without the -n option, the user is prompted to delete all the files in the current directory.

Concatenate the contents of all the files whose names are contained in file:

xargs cat < file > file.contents

into file.contents.

Move all files from directory $1 to directory $2, and use the xargs -t option to echo each move as it happens:

ls $1 | xargs -I {} -t mv $1/{} $2/{}

The xargs -I argument replaces each {} in the string with each object piped to xargs.

Conclusion:

When should you use xargs? When the output of a command is the command-line options of another command, use xargs in conjunction with pipes. When the output of a command is the input of another command, use pipes.

Question 21: Get Return Value

In a Bourne shell script I want to ping a hostname to see if it is there. I know I can do it this way:

CODE

STATUS=`ping $HOSTNAME`

echo $STATUS

and then grep for "alive," etc.

I cannot remember how to get the return value. I want to use it like this:

CODE

ping $HOSTNAME

if [ <what goes here> -ne 0 ];

echo "Host not available." fi

What is the character that I need that will have the return value of ping?

A: To get the return value, use this simple code:

if [ $? -ne 0 ];

Question 22: Assistance with Merge Script

I have about 70 files to merge into one. Each file has about 7 lines or so of data. The final format has to be:

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE1 DATA FROM FILE2 DATA FROM FILE3

DATA FROM FILE4 DATA FROM FILE5 DATA FROM FILE6

DATA FROM FILE4 DATA FROM FILE5 DATA FROM FILE6

DATA FROM FILE4 DATA FROM FILE5 DATA FROM FILE6

DATA FROM FILE4 DATA FROM FILE5 DATA FROM FILE6

And so on and so forth until all 70 plus files have been processed. I am able to merge three files together on the command line using the pr command (and various flags).

How do I get all the files together in the format mentioned above?

A: Assuming all the files are in one directory and nothing else is in that dir, use something like this:

Code:

cd /path/to/dir

set -- $(ls)

while [ $# -gt 0 ]

do

# now use $1 $2 and $3

paste...

# skip to next 3 files and subtract 3 from $#

shift 3

# empty line

echo

done >/path/to/outfile

Question 23: Finding Substrings

I have a ksh script and within this I have two variables that contain directory paths SB_HOME and CD. I want to test if that CD is under SB_HOME and then fill a third variable BASE with the value of the directory under SB_HOME that contains CD.

For example, if SB_HOME is:

"/home/mthales/workspace" and CD is "/home/mthales/workspace/Testing/src/level1/sub" then I want BASE to become "/home/mthales/workspace/Testing"

I've got the line if [ -n "$(echo "${CD}" | grep "${SB_HOME}")" ]; then to be able to test if that CD is under SB_HOME but I can't get the extraction of the sub string from CD to work.

How do I go about this?

A: Use ksh and this should solve your problem:

Code:

#!/bin/ksh

SB_HOME="/home/mthales/workspace"

CD="/home/mthales/workspace/Testing/src/level1/sub"

if [[ "${CD}" == "${SB_HOME}"* ]]

then

# Get the subdirectory only

SUBDIR=${CD#${SB_HOME}/}

print "SUBDIR is $SUBDIR"

# Append the first level of the subdirectory to SB_HOME

BASE=${SB_HOME}/${SUBDIR%%/*}

print "BASE is ${BASE}"

else

print "Error: ${CD} is not in ${SB_HOME}"

exit 1

fi

Question 24: Writing Scripts

What is the danger associated with not adding " ./ " before a > >script name when you run it?"

I know what it means but I don't know what would happen if I don't add it to a command.

A: You have the risk of running some other script of the same name.

Say for example the script name is run.ksh, you have it in your current directory as /users/some/data/run.ksh and in another directory with the same name as /users/some/run.ksh and the directory /users/some is in your $PATH variable.

If you intend to run the actual run.ksh in /users/some/data/run.ksh from /users/some/data/ run it as ./run.ksh. Else running as run.ksh would execute run.ksh available in /users/some/ directory and not the desired one.

Question 25: Merging Columns from Different Files

I have three files that contain numbers as the first column. I want to add these files together so the numbers from the first file is in the first column; the numbers from the second file in the second column and the numbers from the third file in the third column. How can I do this?

As an example:

file1 file2 file3

12 23 236

13 234 234

134 233 234

14 237 233

14 2367 232

14 2399 232

file 4

12 23 236

13 234 234

134 233 234

14 237 233

14 2367 332

14 2399 232

A: Let us say, your data is in file1 file2 file3 and file4.

#!/bin/ksh

rm a1 b1 c1 d1

cat file1 | while read record

do

echo $record | cut -d" " -f1 >> a1

done

cat file2 | while read record

do

echo $record | cut -d" " -f1 >> b1

done

cat file3 | while read record

do

echo $record | cut -d" " -f1 >> c1

done

cat file4 | while read record

do

echo $record | cut -d" " -f1 >> d1

done

paste a1 b1 c1 d1

Question 26: Remove Duplicate Lines in File

I am doing KSH script to remove duplicate lines in a file. Let say the file has the format below.

FileA:

1253-6856

3101-4011

1827-1356

1822-1157

1822-1157

1000-1410

1000-1410

1822-1231

1822-1231

3101-4011

1822-1157

1822-1231

I want to simply do it with no duplicate line as file below.

FileA:

1253-6856

3101-4011

1827-1356

1822-1157

1000-1410

1822-1231

How can I do that in KSH?

A: Try the following command:

Code:

awk '!x[$0]++' file > file.new

Question 27: Reverse and Trim a String

I am using Bourne shells.

How can I reverse and trim a string using UNIX shell scripts?

A: To reverse a string, follow this method:

Code:

str="program"

echo $str | awk '{

for(i=length($0);i>=1;i--)

printf("%s",substr($0,i,1));

}'

Another method:

Code:

str="program"

i=${#str}

final=""

while [ $i -gt 0 ]

do

rev=`echo $str | awk '{printf substr($0, '$i', 1)}'`

final=$final$rev

i=$(($i - 1))

done

echo "Reversed String: $final"

To reverse a line:

Code:

str="this script is to reverse"

i=${#str}

word=""

fin=""

final=""

while [ $i -ge 0 ]

do

temp=`echo $str | awk '{printf substr($0, '$i', 1)}'`

if [ \( "$temp" = " " \) -o $i -eq 0 ]

then

wordlen=${#word}

while [ $wordlen -gt 0 ]

do

revtemp=`echo $word | awk '{printf substr($0, '$wordlen', 1)}'`

fin=$fin$revtemp

wordlen=$(($wordlen -1))

done

final=$final$fin" "

fin=""

word=""

temp=""

else

word=$word$temp

fi

i=$(($i - 1))

done

echo "Reversed line: $final"

Question 28: Transposing Data

I have a report that I would like to import into excel for each record that looks like this:

Record1

Name: Bob

Date: 1/1/2004

Amount:3456

Time: 12:00pm

Record 2

Name: Mary

Date: 2/1/1974

Amount:3000

Time: 5:00pm

Record n

Name: x

Date: y

Amount: z

Time: p

How do I write a shell script (sh) that will give me a single comma delimited line for each record?

A: A starting point:

Code:

awk -F: '

BEGIN{printf "Name,Date,Amount,Time\n"}

NF>1 && $1!="Time"{printf "%s,",$2}

$1=="Time"{printf "%s:%s\n",$2,$3}

' /path/to/report > output.csv

Question 29: Test for Bad Numbers

How can I test for bad numbers?

For example in ksh:

I want the user to input an integer but they input characters.

read number

while (number = letter)

read number //until valid number is inputted

A: You can use egrep to test:

Code:

read foo echo "${foo}" | egrep "^[0-9]+$" >/dev/null 2>&1 if [ "$?" -eq "0" ]; then echo "Yay" else echo "Nay" fi

Question 30: Remove Comma within Quotation Marks

I have a csv file where some strings are enclosed by quotation marks. We found that the following sed operations:

/\(".*\)[,]\(.*"\)/\1\2/g'

will remove the commas within the quotation marks. If any exists, this is what we want but only if one set of quotation marks exist within each line. When more than one set of quotation marks exists then the sed operation does not work on that particular line.

sed 's/\(".*\)[,]\(.*"\)/\1\2/g'

xxxxxxx,xxxxxxxx,"Russellville,",AR,xxxxxx,xxxxxxx ,xxxxxxxx,",ARLINGTON HEIGHTS,IL,60005,US,5.96,0.98,,,,,,,,,,,,,,,,,,,,, ,,,,

Is there a way to pass a second, third or multiple arguments within the sed operations so when it does pass through a line with multiple quotes it understands it and executes the operation of removing the commas?

A: You can do something like this:

sed -e 's/\("[^,]*\)[,]\([^"]*"\)/\1\2/g' file

sed's regex-s are "greedy" - specifying ".*" was eating up too much and you had to limit it to a ','.

How would you do that? If we have "something followed by a comma" it means "anything but a comma followed by a comma":

[^,]*

anything BUT a comma is repeated 0 or more times

[,]

followed by a comma.

INTERMEDIATE QUESTIONS & ANSWERS

Question 31: Search and Replace

How do I perform search and replace operations with extended regular expressions?

A: To perform search-and-replace operations with extended regular expressions, copy and paste the following script to /usr/local/bin/extreg or $HOME/bin/extreg:

Code:

#!/bin/sh

if [ $# -gt 1 ]; then

perl -we '$/="'"$2"'";while(<>){'"$1"';print $_}'

else

perl -we 'undef $/;$_=<>;'"$1"';print $_;'

fi

Syntax: extreg regexp [separator]

"regexp" is one or more extended regular expression, separated by a semicolon.

A "separator" is an optional separator, see perlvar(1), section $INPUT_RECORD_SEPARATOR. The data which has to be processed is divided into (with the separator ending) blocks, on which the regular expressions are applied.

If you want to be portable you should invoke Perl directly. "extreg" is primarily meant to be used in your private scripts or in interactive shell mode.

Question 32: “Read in a While” Loop

I have a script which tries to read input from a user for every value read from a file. The input file is:

Code:

#> more testfile

TEST1 | D200 | 12345601 | | ABC company | m

TEST2 | D201 | 12345602 | | ABC company | m

The script test.sh is as follows:

Code:

while read line

do

read test?"Enter a Value:"

done < testfile

However when executed, the shell never responds to the read command.

Code:

#>test.sh

#>

Is there a special read option that I have to use when using read within a while loop?

A: Look at this code:

while read line

do

read test?"Enter a Value:"

done < testfile

In the first line of the above code, it says “read line.” This reads the first line from the test file and puts it into the variable called line. Again, when you say read test, it actually reads the second line from test file and puts it into the variable test. It won't take the input from the keyboard because you have given the input as test file by specifying the "<".

Use this code:

#!/usr/bin/ksh

IFS="

"

for line in $(< testfile)

do

echo $line

echo "Enter value :"

read a

done

Or do this:

Code:

while read line

do read test?"Enter a Value:" < /dev/tty

done < testfile

Question 33: Shell Script Functions

A simple shell script:

date

test_fn()

{

echo "function within test shell script "

}

On the shell prompt I run:

> . test

Then I invoke the function on the command line as below:

test_fn()

It echoes the line function within the test shell script and works as expected.

How do I find out what are the shell functions known to the current shell?

A: In ksh, use "typeset +f" and "unset –f."

Question 34: Execute a Script for Each Logout

How do I execute a script for each logout?

A: Sometimes it's useful to execute a command after each logout. For example: cleaning up temporary directories or to log working hours.

This is the way to make the shell execute the script $HOME/.atexit after each logout:

1\. Insert this line at the beginning of the file

$HOME/.profile:

trap ". $HOME/.atexit" 0

2\. Create a file named "$HOME/.atexit", that may contain arbitrary shell commands, for example:

$ cat > $HOME/.atexit

echo "Good bye $LOGNAME, the time is `date`"

^D

That's it! After the next login, the shell will execute the contents of the file "$HOME/.atexit."

NOTE: This will not work for C-Shell dialects, i.e., TCSH.

Question 35: Calling Script1 from Inside of Script2

We have a load monitor script that runs every two minutes that search for files in a directory called got it and load them into our Oracle Financials Application. The problem is that this load monitor checks every two minutes using the sleep command and causes the error to be sent via mailx at that same time. As you may know this can load numerous email with the same error into our mailbox.

Is there any way we could call the error checking script2 from inside script1 which will check for errors every four hours using this same sleep command?

A: If I understand you correctly, you want to do something like this:

Code:

#!/bin/sh

# script1.sh

# Do the actual checking

cd /gotit/

while :

do

if [ -f "foo*" ]; then

# ... do whatever needs doing

# Now remove the /tmp/errorfound file, as all is good.

rm -f /tmp/errorfound

else

# Don't send an email on error...

date >> /tmp/errorfound

fi

sleep 120

done

This will do stuff if necessary, or exit with a code of "1" if there are no files. The second script can then call this one in this manner:

Code:

#!/bin/sh

# script2.sh

# Overall monitor

# Call script1.sh in the background

script1.sh &

while :

do

sleep 14400

if [ -f /tmp/errorfound ]; then

mailx -s "There has been an error(s) in the past 4 hours" me@example.com < /tmp/errorfound

fi

done

Question 36: Deleting Lines from a File

I want to delete lines from a file. I have a sample script as below which deletes lines 1 to 3 from the file txt4process. But I need to supply the variable 3 (lines to delete) as an argument.

sed -e '1,3d' txt4process

I tried:

lineNum=someNum

sed -e '1,$lineNum d' txt4process > tppp

sed -e '1,${lineNum}d' txt4process > tppp

However, it is not working.

How do I pass the line number as a variable to the script and delete the same?

A: You're nearly there, just use the double quote: "instead of the single quote:'

The reason is, that the shell treats these two differently; with 'single quotes' the exact text is passed to sed (which doesn't know the shell variable); with "double quotes" the value of the variable is passed to sed, so that will work.

Question 37: File Size Checking

I have a script to send a file but I want to run a check on the size of the file first and if it’s over a certain limit then not to send.

How can I do this?

A: Try something like this: (Take note: do not use the "h" option for ls!).

Code:

filesize=`ls -l $myfile| awk '{ print $5 }'`

if [ "$filesize" -gt "1024" ]; then

echo "File too large for email"

else

# send the email

fi

On the other hand, if you have a file of the exact size you want to compare against, then "test" can do it like this:

Code:

if [ $myfile -gt SAMPLE_FILE ]; then

echo "File too large for email"

else

# Send the email

fi

If you don’t want directories but regular files then do this:

filesize=`ls -l $myfile| grep -v "^d" | awk '{ print $5 }'`

if [ "$filesize" -gt "1024" ]; then

echo "File too large for email"

else

# send the email

fi

Do not forget to use "ls –ld."

Question 38: Modify Log File Timestamp

My shell script (bash) does some queries every hour and appends result of query to a log file. If there is no result, the query would return something like "Query has no entries." If the previous hour's query result is also "Query has no entries," then instead of appending the result, the script only modifies the timestamp for the "Query has no entries" section in the log file.

The log file looks like this:

############

Query time - Mon May 8 09:59:14 PDT 2006

Query has no entries

In this case, how can I find out the last entry in the log "Query has no entries"?

How can I modify only the timestamp in this "Query has no entries" section?

A: Appending the text should be in a function to save repeating the same code three times over. Something like this should do it:

Code:

#!/bin/sh

# Usage: $0 message text

now=`date`

last=`tail -2 q.txt`

result=$@ # message text

if [ "$result" == "Query has no entries" ]; then

# Special case - no entries...

tail -1 q.txt | grep "^Query has no entries$" > /dev/null

if [ "$?" -eq "0" ]; then

# A repeated non-entry

# Get the rest of the file

filelen=`wc -l q.txt | awk '{ print $1 }'`

shorter=`expr $filelen - 2`

head -${shorter} q.txt > qq.txt

# qq.txt now contains the full logfile minus the final two lines

echo "Query time - $now" >> qq.txt

echo "$@" >> qq.txt

mv qq.txt q.txt

else

# First non-entry... log it as usual

echo "Query time - $now" >> q.txt

echo "$@" >> q.txt

fi

else

# A "real" entry... log it

echo "Query time - $now" >> q.txt

echo "$@" >> q.txt

fi

With this script, let's say it's called "q.sh":

Code:

$ ./q.sh Query has no entries

$ ./q.sh Hello

$ ./q.sh Query has no entries

$ ./q.sh Query has no entries

$

And check q.txt each time.

Question 39: Correct Usage of Input

I'm trying to write a UNIX shell to streamline some work I have for a research project. To start, there are three files.

Program: This is a program, that in the course of running, prompts the users once for input file, and then for the output file. Treat it as a black box. It does exactly what it's supposed to if fed the right information.

Data file: It contains a list of the various inputs and output files and there are 50 of each. Let's just say that it looks something like this:

in01.txt

out01.txt

in02.txt

out02.txt

in50.txt

out50.txt

Then the final part, which I'm having most trouble with. This is the actual shell that I was hoping would make this all work. The code within the shell looks like this:

#!/bin/sh

program < Data-file < Date-file

program < Data-file < Data-file

program > Data-file < Data-file (up through 50 times)

I want to go sequentially through the data-file and run it on each pair of input/output. I think it is simply running the program from in01.txt and out01.txt 50 times, leaving the other inputs and outputs untouched.

What is the best thing to do to fix this?

A: You'll have to iterate through the file, like this:

Code:

#!/bin/sh

infile=unknown

while read f

do

echo "$f" | grep "^in" > /dev/null

if [ "$?" -eq "0" ]; then

infile=$f

else

outfile=$f

# Okay, we should have $infile and $outfile now ...

if [ "$infile" != "unknown" ]; then

echo "Calling program from $infile to $outfile

program < $infile > $outfile

fi

fi

done < Datafile

If you want to make life a bit easier, there is some logical link between "in01.txt" and "out01.txt." You could just list one kind (in or out) and work out the name of $outfile from it. That way, you call "program" on every read:

Code:

#!/bin/sh

while read f

do

infile=$f

outfile=`echo $f | sed s/"in"/"out"/1`

program < $infile > $outfile

done < Datafile

That's much shorter and simpler!

Question 40: First Occurrence of a Timestamp within a File

I have bash shell programming question. I want to find the first occurrence of a timestamp, such as "03/09/2006 | 10:30:20" in a file. I tried to use awk or sed. However, what I got is all the timestamp within the file.

How I can do this?

A: The "head" utility will give you the first "x" results, so pipe your sed/awk through "head -1," like this:

Code:

foo=`grep "3/09/2006 | 10:30:20" myfile | head -1`

Similarly, you can use "tail" to get the last entry matching the expression.

Question 41: Backup Script

I want to create a script to backup some files to rewritable cds. The way I see it there are four main tasks to be done:

1\. Erase the CDRW.

2\. Create the ISO to be burnt.

3\. Burn data.

4\. Delete ISO.

How can I bundle these things into one script?

A: Run the four tasks in order. You can do something like this:

Code:

#!/bin/sh

cdrecord -dev=0,0,0 -blank

mkisofs <options> backup.iso $@ (or a list of files)

cdrecord -dev=0,0,0 backup.iso

if [ "$?" -eq "0" ]; then

rm backup.iso

else

echo "An error occured during the CD burn"

exit 1

fi

Better still, do the "$?" error checks after each command

Question 42: Find Command Exec Error

I am writing a shell script in korn shell which deletes all the files in a directory once in every 10 days. The directory has different format files.

The script has something like this:

cd /home/data/pavi

echo "Please Enter the Number of Days to search for"

read DAYS

echo "The entered number of days is $DAYS"

DOACTION="rm -rf"

find DD.* -maxdepth 1 -mtime +$DAYS -exec $DOACTION {} \;

find AA.* -maxdepth 1 -mtime +$DAYS -exec $DOACTION {} \;

The script is working fine DD.* extension.

But for those files with AA.* extension, I am getting the following error message:

pav.ksh[33]: find: Argument list too long.

there are total 22,309 files with AA.* extension.

What is the best approach here?

A: You can try this method:

Code:

find . -name 'DD.*' -maxdepth 1 -mtime +$DAYS -exec $DOACTION {} \; find . -name 'AA.*' -maxdepth 1 -mtime +$DAYS -exec $DOACTION {} \;

Question 43: Remove the File Extension from File Name

I am getting the file name in a variable and need to remove the extension and append a string to it.

file= file1.xml

I need to trim and append "_output.txt" to it without changing the file file1\. Output should be file1_output.xml.

How can I modify the file name string?

A: The following code will help you:

#!/bin/ksh

newExt='_output.txt'

file=file1.xml

echo "before->[$file]"

file=${file%%.*}${newExt}

echo "after->[$file]"

Question 44: Retain Blank Spaces

How do I retain all the blank spaces when I am reading from a file using while...do...done?

A: Just use quotes around the variable.

Example without quotes:

Code:

# ps -f | while read line > do > echo $line > done UID PID PPID C STIME TTY TIME CMD root 15172 15171 0 08:30 pts/4 00:00:00 -bash root 15210 15172 0 08:33 pts/4 00:00:00 ps -f root 15211 15172 0 08:33 pts/4 00:00:00 -bash

And with quotes:

Code:

# ps -f | while read line > do > echo "$line" > done UID PID PPID C STIME TTY TIME CMD root 15172 15171 0 08:30 pts/4 00:00:00 -bash root 15212 15172 0 08:33 pts/4 00:00:00 ps -f root 15213 15172 0 08:33 pts/4 00:00:00 –bash

Question 45: Hide Password

I am trying to write a shell script to call ftp program to send files to windows shared drive. I don't want my user to directly deal with ftp program, so I use shell as an interface to allow them to give userID and password.

Is there any way I can hide the password when the user inputs within the shell program just like when we log into UNIX?

A: This code can work for what you need:

#! /usr/bin/ksh

print -n "Enter password - "

stty -echo

read PASSWORD

stty echo

print

Then just use $PASSWORD where you need it.

Question 46: Stored Procedure

I am working in korn shell and need to execute a shell script that in turn executes a stored procedure (e.g. select * from temp). Now I want to get the result of the stored procedure or the select statement output and store that result in a file.

How do I do this?

A: Use these statements in your script:

isql -Uuser_name -Ppassword<<!RUN>>outputfile_name

select * from temp

go

!RUN

After this execute the script:

as

sh filename

Question 47: Checking Exit Status

In a script, I am doing a cmp on two files. I am trying to check the exit status with an “if statement” but can't seem to figure out the syntax. If the exit status is 1, I want to do something else. I am using Solaris 8 and my shell is ksh.

Here is what I have in the script followed by the error message:

#!/usr/bin/ksh

cmp file1 file2

rtrncd=$?

if [$rtrncd -ne 0 ] then

cat error-message-file | mailx -s "Error `date`" email address

exit $rtrncd

fi

The error I get is:

check_rep2.sh[7]: syntax error at line 11 : 'fi' unexpected

How can I rectify this error?

A: You need spaces around [and]. Also "then" is a separate command. You must put it on a new line or use a semicolon. if [ $rtrncd -ne 0 ] ; then

Question 48: Separating Filenames

I am trying to write a script that will take a list of filenames, operate on them individually and output a changed file name—mainly for renaming a large number of files.

So far I have the following:

TARGET="$(ls -1 |)"

for FILE in "$TARGET"; do

NEW=$(echo "$FILE" | 'do some stuff to file')

mv $FILE $NEW

done

All the filenames are kept as one long string in $FILE, and $NEW, so I can't do anything with them once I have changed them.

How can I get the script to see each filename separately?

A: Remove the double quotes in:

Code:

for FILE in $TARGET; do

The double quotes will make it one parameter:

#!/usr/bin/ksh

echo $1

echo $2

echo $3

# s1 "a b c" d e

a b c

d

e

# s1 a b c d e

a

b

c

Question 49: Extract a String

How can I extract a string from a given string?

Example:

1\. /detl01/SHL/TARG/SHL

I need to start reading the directory path from the first '/' :

/detl01/SHL/TARG/SHL

For example, what do I need to do to eliminate all the previous characters?

A: You can try this line:

Code:

name="1\. /detl01/SHL/TARG/SHL" path=`echo $name|cut -d' ' -f 2` echo $path

Here's another approach:

name="1\. /detl01/SHL/TARG/SHL"

name1=${name#*}

echo $name1

Question 50: Splitting a String

I have a number of filenames made up of letters and numbers like the following:

01-000.134off.log

01-000.14off.log

01-000.4off.log

I would like to strip away everything leaving just the non-zero numbers. For example:

134

14

4

I have managed to get this using grep and sed with no problem. What I really want to do next is split the string of numbers into single digits so that I am left being able to use the digits to place of another part of the program.

Is this possible?

A: If you want the digits separated on a single line add:

Code:

-e 's/\(.\)/\1 /g'

to your sed statement

If you want each digit on a separate line use:

Code:

-e 's/\(.\)/\1^M/g'

where you create ^M by pressing Ctrl-V, Enter.

Question 51: Searching the Line + Next 20 Lines

I want to search a pattern in a simple file in UNIX. I can use the grep command for this but I want to get the search pattern line and the next 20 lines redirected into some other file.

Is there any option in grep or some other way through which I can get the output?

A: Place the following code into a file called script.awk:

Code:

BEGIN { count = 21 } /pattern/ { count = 0; } count <= 20 { print; count++; }

From the command line run:

awk -f script.awk file-you-want-to-search

Question 52: Number and Name of Records in a File

I’m trying to get the count of number of records of a file named as:

wc -l file1.txt

I am getting the correct count and the file name too. The output I get is:

7 file1.txt

How can I avoid the filename in the output?

A: You can "cut" out the number of records or you can use “awk” to count records:

Code:

awk '{n++} END {print n}' file1.txt

Or, depending on your shell, you can strip off the filename:

Code:

#! /usr/bin/ksh x="7 file1.txt" # your command would be x=$(wc -l file1.txt) print ${x% *}

Question 53: Merging Columns from Different Files

I have three files that contain numbers as the first column. I want to add these files together so the numbers from the first file is in the first column, the numbers from the second file in the second column, and the numbers from the third file in the third column.

As an example:

file1 file2 file3

12 23 236

13 234 234

134 233 234

14 237 233

14 2367 232

14 2399 232

file 4

12 23 236

13 234 234

134 233 234

14 237 233

14 2367 332

14 2399 232

What is the best method for doing this?

A: Let us assume your data is in file1 file2 file3 and file4:

Code:

#!/bin/ksh

rm a1 b1 c1 d1

cat file1 | while read record

do

echo $record | cut -d" " -f1 >> a1

done

cat file2 | while read record

do

echo $record | cut -d" " -f1 >> b1

done

cat file3 | while read record

do

echo $record | cut -d" " -f1 >> c1

done

cat file4 | while read record

do

echo $record | cut -d" " -f1 >> d1

done

paste a1 b1 c1 d1

Question 54: Formatting a File

I have been trying to format a file using sed. I want to append the next line delimited by a comma or a comma and double quotes. Here is an example of the file I'm trying to format:

Before formatting:

00324

03A0312

BRI-u24

0000324

01

H-12

KKG

00325

03A0312

BRI-u25

0000325

02

H-13

KKG

00326

03A0313

BRI-u26

0000326

03

H-14

KKG

After formatting:

00324, 03A0312, BRI-u24, 0000324, 01, H-12, KKG

00325, 03A0312, BRI-u25, 0000325, 02, H-13, KKG

00326, 03A0313, BRI-u26, 0000326, 03, H-14, KKG

Or

"00324" , "03A0312" , "BRI-u24" , "0000324" , "01" , "H-12" , "KKG"

"00325" , "03A0312" , "BRI-u25" , "0000325" , "02" , "H-13" , "KKG"

"00326" , "03A0313" , "BRI-u26" , "0000326" , "03" , "H-14" , "KKG"

A: Try this Code:

nawk -v OFS=, -v RS='' '$1=$1' myFile.txt OR nawk -v OFS=, -v RS='' '{for(i=1;i<=NF;i++) gsub(/.*/,"\"&\"", $i); print}' myFile.txt

Question 55: File Comparison

Is it possible to compare two files bit by bit and output the following?:

1\. Bit position of mismatch in each line.

2\. Missing records in either of the two files.

Take note that the third column in both the files is unique.

File 1

ABC 1212 san

ASB 2121 van

AWS 2122 man

AKS 1112 dan

AQZ 1123 ran

SQA 3232 jam

BQA 3121 pan

GAT 3452 wat

File 2

ABC 1212 san

ASB 2222 van

AWS 2122 man

AQZ 1123 ran

AQZ 1123 wat

DAT 3223 sat

SQA 3232 jam

BQA 3121 pan

GAT 3452 wat

Output File

Records missing in file 1 are: DAT 3223 sat, AQZ 1123 wat

Records missing in file 2 are: AKS 1112 dan

Mismatch in bit position: 6 & 8 for string van

Is there any way to locate the exact bit position of mismatch within a line?

A: Try this Code:

awk '{print $1,$2}' file1 | sort > tmp1

awk '{print $1,$2}' file2 | sort > tmp2

# records unique to file1 comm -1 tmp1 tmp2

#records unique to file2 comm -2 tmp1 tmp2

Question 56: Include "$" in a String

I have the following code:

SqlString="CREATE USER $1 IDENTIFIED BY $3

DEFAULT TABLESPACE TEMPTABS

TEMPORARY TABLESPACE TEMPSEGS

QUOTA UNLIMITED ON TEMPTABS

PROFILE DEFAULT

ACCOUNT UNLOCK;

GRANT xxxxxx_ROLE TO $1;

ALTER USER $1 DEFAULT ROLE xxxxxx_ROLE;

CREATE USER $2 IDENTIFIED EXTERNALLY

DEFAULT TABLESPACE TEMPTABS

TEMPORARY TABLESPACE TEMPSEGS

QUOTA UNLIMITED ON TEMPTABS

PROFILE DEFAULT ACCOUNT UNLOCK;

GRANT xxxxxx_ROLE TO $2;

GRANT yyyyyy_ROLE TO $2;

ALTER USER $2 DEFAULT ROLE xxxxxx_ROLE,yyyyyy_ROLE;

exit;"

echo "$sqlString" > $APP_HOME/test/EMPMC.$$

sqlplus system/xxxxx @$APP_HOME/test/EMPMC.$$

rm $APP_HOME/test/EMPMC.$$

When I invoke the script test.sh APPLE OPS$APPLE PEAR, I get an error message that the APPLE variable is not defined.

How do I pass the argument without UNIX interpreting the "$APPLE" as a variable?

A: This should fix your problem:

OPS\$APPLE.

Question 57: Deleting the Empty File

I have a TEST.dat file. As a clean up process, I have to delete the TEST.dat file if it is empty. Basically, I don't want to delete TEST.dat if it contains anything in it but want to delete TEST.dat if it contains any spaces or nothing in it.

Is there a command to check if the file is empty then delete it?

A: Follow these steps:

1\. Check for spaces using sed to remove all the spaces.

2\. Use an if condition to check the size of the file like:

if [[ ! -s txt ]] then

echo " empty "

else

echo "non empty"

fi

3\. Now delete in if statement:

rm -f txt.

Question 58: Copy Script

How do I copy a file that changes daily to a new directory with a different name each day?

Example:

Webfile created today: copy webfile to /hold/webfile.1

Tomorrow: copy webfile /hold/webfile.2

A: It is always advisable to append the timestamp to the file. It’s easier unless you have specific requirements. However, if you really want a numeric increment, you can try following:

Code:

#!/bin/ksh

#=================== extn=`ls -l webfile* | sed -e 's/.*[.]//g' | sort -nr | head -1` let extn=$extn+1 cp webfile webfile.$extn #===================

This assumes that you a webfile.file to start with. You just have to make the first copy with a .1 at the end or you’ll get a bad number message.

Question 59: Parsing a String in a Shell Script

I need to parse a string in a shell script. Is there some built-in function to do this? Can you explain how to do the syntax?

For example:

#!/bin/ksh

read input

# input is entered as 'welcome'

#Now I want to extract say only first 4 characters or last four #characters.

A: You can use awk for both.

For example:

First four characters:

Code:

$ echo "welcome" | awk '{ print substr( $0, 0, 4 ) }' welc

Last four characters:

Code:

$ echo "welcome" | awk '{ print substr( $0, length($0) - 3, length($0) ) }' come

IN substr( s, i, n )

Where s is the string you want to perform the substr operation on, i is the first character that you want to extract, and n is the last character you want to match.

So if you said substr( "hello," 2, 4 ) it would match the second, third and fourth character and return "ell."

Let me explain the code I gave:

Code:

$ echo "welcome" | awk '{ print substr( $0, 0, 4 ) }'

In the above example, the first argument to substr is $0 (which in this case is the text piped to it; "$0" is the entire record). The second argument is 0 (I could also have used 1) because I want to match it from the start of the string. I want to grab the first four characters, so the third argument is 4.

Code:

$ echo "welcome" | awk '{ print substr( $0, length($0) - 3, length($0) ) }'

The above code also makes use length (string) command to return the number of characters in the string.

So here, I'm saying "return the substring from the first character (which is the length of the string minus 3), up until the very end of the string."

To clarify this:

Code:

$ echo "welcome" | awk '{ print (length($0) - 3), length($0) }' 4 7

So in our substr, we grab from character 4 to character 7 inclusive, which are chars 4, 5, 6, 7 - the last 4 chars.

Another solution is:

typeset -L4 first4

typeset -R4 last4

x="welcome"

first4=$x

last4=$x

echo $first4 $last4

Also you can discard the first 4 or the last 4.

last_part=${x#????}

first_part=${x%????}

echo $first_part $last_part

Question 60: Replace All Occurrences of a String

I need a script that will replace all occurrences of a string in all filenames and folder names, recursively.

Right now I have this script:

Code:

for f in `find -name *eye*`; do echo processing $f g=`expr "xxx$f" : 'xxx\(.*\)' | tr 'eye' 'm'` mv "$f" "$g" done

The problem is that tr replaces the characters e and y with m instead of the string "eye."

I adapted this from: [http://webxadmin.free.fr/article/sh...to-lowe-135.php](http://webxadmin.free.fr/article/sh...to-lowe-135.php) so I don't really know what the regular expressions in expr are doing.

How can I make this work?

A: Here is a code that can work for you:

Code:

for f in `find . -name \*eye\* -print`; do echo processing $f g=`print "$f" | nawk 'gsub(/eye/,"m")'` mv "$f" "$g" done

"tr" in the script that your link reference is simply changing upper case names to lower case.

Question 61: Replace Character Occurrences

In a Bourne shell script, I have a list of items delimited by a comma and I would like to change this, setting it to a variable, to be delimited by spaces.

Code:

TABLES1="a,b,c,d"

TABLES2="<same list a TABLES1 but delimited by spaces>"

How do I convert all the commas to spaces in the list and set this to a variable?

A: Try this code:

# bash & ksh, not sure about sh

TABLES2="${TABLES1//,/ }"

# any shell

TABLES2=`echo "$TABLES1" | tr ',' ' '`

Question 62: Passing Parameters to Script

In a Bourne shell script I am calling an include file where I am trying to add the ability of the called script to act upon parameters being passed.

The included script runs okay by itself being called from the command line but not when being called from within my parent script. It does not seem to be getting the parameters or setting\exporting the variable.

Parent Script:

#!/bin/sh

. /mypath/initVars.sh DB1

# The value of this is set in initVars.sh

# but is empty when running from this script.

echo $MYDB

initVars.sh (this works fine being executed by itself)

Code:

#!/bin/sh

# Usage: initVars.sh <db_name>

# Example: initVars.sh DB1

MYDB="$1"

export MYDB

echo $MYDB

What can you suggest?

A: You could try a shell function:

------/mypath/sh_fun_lib.sh-----

#!/bin/sh

F_Init_Vars ()

{

MYDB=$1

export MYDB

}

--------------------------------

------/your/script.sh-----------

#!/bin/sh

###

#install shell functions

. /mypath/sh_fun_lib.sh

###

# set vars

echo before MYDB=$MYDB

F_Init_Vars DB1

echo after MYDB=$MYDB

Question 63: Schedule Script without Using cron

How can I run my script every day at 8:00 a.m. and 10:30 a.m. except Saturday and Sunday? I don't have cron installed in my account.

A: Try this code:

#!/bin/ksh

TIMES="0800 1030"

DAYS="1 2 3 4 5"

JOB="uptime"

while true

do

sleep 50 # check at least once a minute

for DAY in $DAYS

do

if [[ "$(date +%w)" -eq "$DAY" ]]

then

for TIME in $TIMES

do

if [[ "$(date +%H%M)" -eq "$TIME" ]]

then

$JOB &

# make sure we do

# not run twice

sleep 20

fi

done

fi

done

done

Replace uptime with your job of course and run this script in the background, probably best with nohup.

If you check every 60 seconds, there is a very small chance on a busy system that it will check once at 07:59:59, and the next time at 08:01:00, so your job would not run.

$JOB & runs the job in the background, so that the annicron keeps running, in case the jobs overlap or take a long time, etc. You can take out the & of course if you want, and that would make sure they would never overlap.

“sleep 20” is to make sure it doesn't run a job twice in one minute, e.g., at 08:05 and 08:55.

Question 64: Get Current User

On a Solaris 8 and 10 systems in a Bourne shell script, I need to set the current user to a variable. My problem is I cannot use an environment variable like LOGNAME or USER.

Could I use id command if I can just extract the username and set it to a variable? What is the correct code for this?

A: Try any of the following codes:

Code:

USERID=`id|sed 's/).*$//g;s/^.*(//g'`

Code:

USERID=`/usr/ucb/whoami`

This is a little easier to understand and does the same thing:

Code:

user=$(id | cut -d\( -f2 | cut -d\) -f1)

Question 65: String Substitution

I have two shell variables(v1, v3) and I want to substitute a part of one variable (v1) with the other(v3).

let v1=NPDL0000000

let v2=12

let des=

v3=`expr $v2 + 1`

I would like des=NPDL0000013, which comes from

NPDL0000000 (v1)

13 (v3)

---------------------------

NPDL0000013 (des)

Is there a way to do this in shell script?

A: The following approach can help you:

Code:

master # v1=NPDL0000000

master # v2=12

master # v3=${v1%??}$v2

master # echo $v3

NPDL0000012

Question 66: Read a Specific Line

I have a huge file (about 25 millions lines).

Is there a way to read Line n directly without looping through each line of the file?

A: There are several ways to do this. Try one of the following codes:

sed -n '250p;251q' bigfile

sed '250q;d' bigfile

sed -n '250{;p;q;}'

A similar optimization for awk:

awk 'NR==250{print;exit}' bigfile

Question 67: Server or Environment Determination

I want to use the server name as a switch to populate various environment variables for development, QA/test, or production as applicable.

Is there an internal shell command or environment variable that can tell me which server I am on?

A: Create your own environment variable (like a HOST maybe) and set it in the /etc/profile script.

Or, write a simple file in /etc/me.txt and write down the server name into it and make a simple script called servername.sh with cat /etc/me.txt.

Question 68: Timer

For a Bourne shell script, what is the code snippets required to display how long a script took to run?

I am thinking there needs to be at minimum two variables: TIMER_START and TIMER_END, but I am not sure how to best set the values and calculate the elapse time.

A: A starting point:

Code:

s=`eval 'date "+expr \( 3600 \* %H \) + \( 60 \* %M \) + %S"'`

start=`eval $s`

# your script here

s=`eval 'date "+expr \( 3600 \* %H \) + \( 60 \* %M \) + %S"'`

end=`eval $s`

echo "Elapsed time = `expr $end - $start` seconds"

Question 69: Dynamic Variable Evaluation

On a Sun Solaris 8 system in a Bourne script, I am dynamically creating and testing some variables. I am having a problem detecting when/if a dynamic variable value does not have a value.

The assumption is that there will always be a DEST1 but the goal is to test if there are more. It is also assumed that they will be created in sequential order (DEST1, DEST2 etc.).

Code:

#User Defined Variables

DEST1="/dir_x"

DEST2="/dir_y"

# Build Destination String

for i in 1 2 3 4

do

echo "$DEST$i" # <=== This displays correctly

if [ -n $DEST$i ] then

# Stuff I need to do if above true

fi

done

How can I test if the user created a DESTn variable?

A: Try something like this:

Code:

#!/bin/sh

#User Defined Variables

DEST1="/dir_x"

DEST2="/dir_y"

# Build Destination String

for i in 1 2

do

eval DIR=\$DEST$i

echo "$DIR"

if [ -n $DIR ] ; then

# Stuff I need to do if above true

echo "Dir = ${DIR}"

fi

done

Question 70: Eliminate Duplicates from a Long List

I am trying to eliminate duplicates from a comma-separated list of email addresses that looks something like this:

myemail@address.com,bossemail@address.com,

computerstaffemail@address.com,myemail@address.com

I have tried:

sort -u -t , emailfile.txt

But it doesn't seem to work. What am I doing wrong?

A: Try to use this code:

awk 'BEGIN{ORS=RS=","}!a[$1]++' emailfile.txt

BEGIN{ORS=RS=","}

This is executed before the file is read. Since the RecordSeparator is set to ",", Awk will read a field at a time instead of a line of a time.

!a[$1]++

"!a[$1]" means if the array "a" has no value or a zero value for $1, then print the item just read. After this, the "++" causes the value of "a[$1]" to be incremented by 1\. The effect of all this is to print the item only the first time it is encountered.

Question 71: Crontab Relative Path

Say we have a shell script that refers to relative paths for files/directories:

For example:

Code:

#!/bin/sh

cp thisfile ../thatfile

cd mydir

This type of file works fine when we issue it from the command line, but when we register it as a crontab, it seems that the files/directories have to be referred to as absolute path.

It is easy to change this script since it is small, but what if we have a really large shell script and all of it is implemented with relative references.

Is there another option than to check every line and make it absolute?

A: In the crontab:

cd /path/to/dir && yourscript

Question 72: Security Work Around

I have a JSP page running on Redhat that will execute a shell script. The shell script contains the following code:

#!/bin/sh

scp schedule.sh user1@differenthost:~/schedule.sh

ssh user1@differenthost <<END_SCRIPT

./schedule.sh $1 $2

exit

END_SCRIPT

exit 0

Basically, the code uploads a shell script to a different box and then ssh to that box to execute that shell script with some arguments. This code is currently owned by “user1” on my Redhat and is working just fine when evoked from the command line. I have setup private/public ssh keys between user1 and a different host with no password required, so that I don’t have to hardcode the pw.

My problem is, when this code is invoked from JSP, I get a permission denied error. I finally found out the reason for this and it was because JSP is running as the “Apache” user and it has no right to ssh to differenthost. A direct workaround will be to have this shell owned by the “Apache” user and setup a public/private key for “Apache” but this will create a big security risk.

How I should go about setting the permission for my scenario?

A: I'm a big fan of Sudo as a solution to security problems. If the sudoers file is set up correctly then Apache' can run the transfer script as user1 and nothing else. The sudoers entry will look something like this:

Code:

apache thisserver = /usr/bin/su - user1 -c /home/user1/tx.sh

Question 73: Renaming Multiple Files

I want to create a shell script that will automatically rename a bunch of graphics files cutting off the last part of the filename as there is no pattern to match on without a bunch of if statements.

For example, the filenames are:

5568012_101_12.jpg

5652901_101_12.jpg

5890390_101_13.jpg

5992313_101_71.jpg

I simply want the files to be renamed as:

5568012.jpg

5652901.jpg

5890390.jpg

5992313.jpg

Is there a way to do this?

A: Yes there is. Here’s one possible way:

ls *_*.jpg | awk '{split($0,a,"_");print "mv "$0" "a[1]".jpg"}' | sh -v

Question 74: Traverse and Download

Is it possible to give a URL to a script and pick out the link for a ".doc" or ".xls" then download it?

For example:

% find_file ".doc .xls" http://local_site/foo_docs_1.htm

It will go to foo_docs_1.htm and look for .doc and .xls files and download it for me.

A: You can try this procedure:

wget with the -A or --accept option:

Code:

wget -r -p -A.doc,.xls http://local_site/foo_docs_1.htm

Or:

lynx with the -dump option, then wget :

Code:

lynx -dump http://local_site/foo_docs_1.htm | \

sed '1,/References/d; s/.* //' | \

grep -E "\.(doc|xls)$" | \

wget -i -

Question 75: Output a Specific Line in a File

In UNIX, the head command can be used to show the first few lines of a file. However, what if we want to show only a specific line?

What if we wanted to show line 5 of a file named test.txt, is there any command that would accomplish this?

A: One way to do that is:

sed -n '5p' test.txt

Here’s another way:

awk 'NR==5{print;exit}' test.txt

Question 76: About Kill Command

How does the kill command work?

How does it communicate to a process that it should die?

A: By a call to the system function signal.

A signal is a kind of software interrupt that's sent to the process. It’s kind of a tap-on-the-shoulder from the OS. The process can either handle the signal by jumping to some code that deals with it, or not. If a process is not programmed to handle a signal, the signal will usually cause the process to terminate. The programmer of the process can write handler routines to deal with or ignore every signal except for 9, SIGKILL. This is the only signal that can't be caught and will kill all processes (unless something's really messed up).

The function sigaction (man sigaction) lets you define functions that your code will jump to handle whatever signals your code receives. This lets you "trap" those signals and allows you to do something smart and controlled, instead of just dying. This is useful to have a program shut down cleanly and properly close files instead of just aborting and leaving a mess.

See the main pages for signal and sigaction. There are a lot of good links with info on signals. Here's one:

[http://www.cis.temple.edu/~ingargio/cis307/readings/signals.html](http://www.cis.temple.edu/~ingargio/cis307/readings/signals.html)

Question 77: Calling Shell Script with * as a Parameter

When running a shell script, I want to call another shell script and pass in a parameter representing a filename.

The structure of the filename is: ProgramName.DatabaseName.Date.log

The ProgramName and DatabaseName are known but the date is unknown.

If:

ProgramName=export

DatabaseName=test

Date=any value in the format of <MonYY>

The filename parameter passed in is: export.test.*.log

When I pass in this parameter, the shell script being called substitutes the * with all sorts of strange values, whereas I want the shell to receive export.test.*.log and treat the asterisk as an asterisk.

How can I do this?

A: In the Korn Shell, a "set -f" will turn off globbing so you can pass the asterisk as is. That is, it won't translate the asterisk. It should appear like this:

Code:

set -f

shell.ksh ${FILE}.*.${FILE_EXT}

Question 78: Extract a Section of Text in File

Using a Bourne shell script, I need to extract some lines from a text file.

My file looks like this:

Code:

SQL> SELECT bla bla bla

/export/oracle/myfile1.dbf

/export/oracle/myfile2.dbf

/export/oracle/myfile3.dbf

SQL> spool off

In a file, I need to extract just the lines that start with "/export..." to another file (files.lst). The tricky part is that the header’s two lines and bottom single line will remain the same but the total other lines (with /export) are variable.

Is there some syntax to grab just the /export lines?

A: One way of doing that is through this is:

grep '^/export' /path/to/input > files.lst

Question 79: Run UNIX in a New Shell Inside a Shell Script

I am having one situation in which I need to run some simple UNIX commands after doing "chroot" command in a shell script. This in turn creates a new shell.

So the scenario is that:

1\. I need to have one shell script which is run as a part of crontab.

2\. In this shell script, I need to do a "chroot" to some particular directory.

3\. After chroot, I need to run some UNIX command.

Here is the script:

#!/usr/bin/ksh

cd /safedir/rdns/opt/MKDownload

#java MKProcessor

Val=`diff /safedir/rdns/opt/MKDownload/sun.csv

/safedir/rdns/opt/RDNS1.1/WEB-INF/lib/sun.csv |wc

-l`

if [ $Val -gt 0 ];

then

(

# `mv /safedir/rdns/opt/RDNS1.1/WEB-INF/lib/sun.csv

/safedir/rdns/opt/RDNS1.1/WEB-INF/lib/sun.csv.bak`

# `cp /safedir/rdns/opt/MKDownload/sun.csv

/safedir/rdns/opt/RDNS1.1/WEB-INF/lib`

/usr/sbin/chroot /safedir/rdns /bin/sh ------------------1

echo `pwd` -------------------------------------- 2

cd /opt/iws61/https-rdns/

./stop

./start

)

fi

So as apparent from the script, after chrooting in line 1, it creates a new shell and the execution of this script suspends there. As soon as I exit the shell, the remaining commands from line 2 onwards execute in current shell and I get an error. But as per my requirement, the remaining commands need to run from chrooted directory only.

Is there a way to solve this?

A: If I were you, I would do this:

/usr/sbin/chroot /safedir/rdns /bin/sh -c "cd /opt/iws61/https-rdns ; ./stop ; ./start"

Question 80: String Replacement Script

I have a script right now that is made to search through a file and replace certain strings with a new one. The format to execute is "/subst <replacethis> <withthis> <filename>" and it only updates the file if changes are made in order to preserve the time it was made/last modified. I have this working 100% right now, but the next step is to edit the script so that it is possible for users to do "/subst <replacethis> <withthis> <filename> <filename2> <filename3> <filenamex>" as high as they want.

Can this be done?

Here is my current script:

#!/bin/bash

replacethis=$1

withthis=$2

file=$3

sed -e "s+$replacethis+$withthis+g" $file >

$file.bak cmp $file $file.bak > /dev/null if [ $? -eq 0 ]

then

echo "Files are the same, nothing was replaced."

rm $file.bak

else mv $file.bak $file

fi

A: Of course you can! This code should work perfectly:

#!/bin/bash

replace this=$1

with this=$2

shift 2

for file in $@

do

sed -e "s+$replacethis+$withthis+g" $file > $file.bak

cmp $file $file.bak > /dev/null

if [ $? -eq 0 ]

then

echo "Files are the same, nothing was replaced."

rm $file.bak

else mv $file.bak $file

fi

done

Question 81: UNIX Script Issues

I have written the following UNIX for HP-UX 11i. The script basically checks for files older than 45 minutes in 2 respective directories and then sends an email to the administrator about them.

The problem with the script is that I can run it from the command line and crontab tab but 80% of the time it errors out with the following message "date: bad conversion."

I'm puzzled as to why it works brilliantly sometimes but the why majority of the times it errors out with the above error message.

Here is my script:

#!/usr/bin/ksh

mailgroup='testuser@xxx.com'

LOGFILEIN=/tmp/sipstimein.log

LOGFILEPROC='/tmp/sipstimeproc.log'

#GET AND PARSE THE CURRENT DATE

date "+%m %d %H %M" | while read MONTH DAY HOURS MINS

do

#SUBTRACT 45 MIN

MINS=$(($MINS-45))

if [ $MINS -lt 0 ]

then

HOURS=$(($HOURS-1))

MINS=$(($MINS+60))

fi

#TOUCH A FILE SO THAT IT IS 45 MINUTES OLD

touch -t ${MONTH}${DAY}${HOURS}${MINS} /tmp/oldtime

done

#Find files older then 45mins condition

find /interface/data8/sips/proc ! -newer /tmp/oldtime | while read FILENAME

do

#CHECK THAT IT IS A REGULAR FILE, AND NOT A DIR OR

# CHARACTER FILE, BEFORE RUNNING THE COMMAND AGAINST IT

if [ -f $FILENAME ]

then

echo "$FILENAME" >$LOGFILEIN

sleep 4

mailx -s "Files have been detected older then 45mins in PROD system for SIPS in the PROC directory" <$LOGFILEIN $mailgroup

2>&1

fi

done

find /interface/data8/sips/in ! -newer /tmp/oldtime | while read FILENAME

do

#CHECK THAT IT IS A REGULAR FILE, AND NOT A DIR OR

# CHARACTER FILE, BEFORE RUNNING THE COMMAND AGAINST IT

if [ -f $FILENAME ]

then

echo "$FILENAME" >$LOGFILEPROC

sleep 4

mailx -s "Files have been detected older then 45mins in PROD system for SIPS in the IN directory" <$LOGFILEPROC $mailgroup

2>&1

fi

done

#rm /tmp/oldtime

What am I doing wrong?

A: I think your problem is with your $HOURS and MINS calculations. If you subtract 45 from 50, for example, you get "5" not "05." So your touch command gets confused because the timestamp is not formatted "MMDDhhmm."

Since you are using ksh, you could fix using this code:

typeset -Z2 HOURS MINS

However, if you have Perl, perhaps you should try this:

#GET AND PARSE THE CURRENT DATE

SUBTRACT 45 MIN (2700 SECONDS)

STAMP=$(perl -e '($ss, $mm, $hh, $DD, $MM, $YY) = localtime(time() - 2700);

printf "%04d%02d%02d%02d%02d", $YY + 1900, $MM + 1, $DD, $hh, $mm') #TOUCH A FILE SO THAT IT IS 45 MINUTES OLD touch -t $STAMP /tmp/oldtime :

Question 82: Split a Document

I have a document of more than 80,000 lines. It is generated in a dynamic way, sometimes it has 80,000 others 30,000, or 1000,000\. I’m trying to break this file in only 1 line of commands but I want to break it in N different files of nearly the same lines equally. So I need to check the number of lines of this file and after that split it in N different files with the same number of lines. This is because I need to have parallel process working each one of these files.

I know about the wc -l command return the number of lines, and the split command split -l XXXXX the file.

How can I pipe these commands in order to have N files of the same time in a dynamic way?

A: You can try this command:

split -l `wc -l yourfile | awk '{print $1/N'` yourfile

You can replace N by any number.

Question 83: Exit Shell Script from Function

I have tried to put an exit 0 statement within a function I have created in the shell script, but it doesn't seem to exit out of the script.

Is there another way to exit the script from within a function?

A: This one works:

Code:

$ cat funtest

#! /usr/bin/ksh

one()

{

echo in one

exit 0

}

function two

{

echo in two

exit 0

}

echo at start

if [[ $1 = one ]] ; then

one

echo back from one

else

two

echo back from two

fi

exit 0

$ ./funtest one

at start

in one

$ ./funtest two

at start

in two

$

Question 84: Search Multiple String Occurrences

I need to search the strings in the text file that has the following information:

INSERT INTO TEST123

values (1,2,3);

INSERT INTO ABCD

values (1,2,3);

UPDATE TEST123

SET

ABC='123'

WHERE ABC='124';

UPDATE ABCD

SET

ABC='123'

WHERE ABC='124';

DELETE FROM TEST123

WHERE ABC = '111'

AND DEF= '222'

AND GHI='333';

DELETE FROM ABCD

WHERE ABC = '111'

AND DEF= '222'

AND GHI='333';

I need to search for the string "TEST123" and then search for the following character: ;

Once these two strings are found, I want to copy the data from line1(FIRST STRING FOUND) and lineN(SECOND STRING FOUND) to another file.

NEW FILE OUTPUT:

INSERT INTO TEST123

values (1,2,3);

UPDATE TEST123

SET

ABC='123'

WHERE ABC='124';

DELETE FROM TEST123

WHERE ABC = '111'

AND DEF= '222'

AND GHI='333';

How can I achieve this?

A: Try using this code:

awk '{printf $0}' old.file.name|awk 'BEGIN{RS=";"}{print $0 ";"}'|grep -i "test123" > new.file.name

Question 85: Search/Copy Records

I am trying to search a text file with hundreds of lines (records).

So I need to search until the end of the file per each line. Within each line, I need to search for a particular string. If the string matches, I want to copy the whole line (record) into a new file like building a new file with the list of matching records.

Also, when I copy the record, I would like to place an “insert into table” statement at the beginning and then put a semicolon at the end so that I can execute the file as sql.

Is there a way to do this?

A: You can try this code:

sed -ne '/MFP/s#.*#&#p' file1 > file2

ADVANCED QUESTIONS & ANSWERS:

Queries likely to be asked by experts in Programming

Question 86: Menu Considerations

I am trying to enhance a menu using a Bourne shell script on Solaris 8\. In the past, I have used the read OPTION to grab user input but this requires a user to press Enter.

Is there a way to grab a single key input and execute it immediately without requiring an Enter key being pressed?

A: Try this part of code:

Code:

#----------------------------------

# subroutine to read one char

#----------------------------------

function getchar {

typeset OLDSTTY=$(stty -g 2>/dev/null)

stty -icanon -echo min 1 time 0 2>/dev/null

typeset CAR=$(dd bs=1 count=1 <&0 2>/dev/null)

stty $OLDSTTY 2>/dev/null

print $CAR

}

print "Answer Y N or Q to quit : \c"

C1=$(getchar)

print "You typed : $C1"

# treat the answer given

Question 87: Finding the Last Row

Using Linux and Bash, I have a script that outputs filenames with complete path, like this:

/foo/bar/filename.pdf

/foo/bar/filename with space.pdf

/foo/filename.txt

I would like the following output:

filename.pdf

filename with space.pdf

filename.txt

I would like to get the filenames only. The tricky part is that I cannot predict how many levels deep the filename is located, so I cannot use standard Bash to solve this.

What is the best method to do this?

A: Add this line to the script:

Code:

FILENAME=${file##*/}

Where file would hold contain the values.

Code:

/foo/bar/filename.pdf /foo/bar/filename with space.pdf /foo/filename.txt -- - one at a time.

And FILENAME would hold filename.pdf filename with space… et al.

Quote:

${parameter##word}

The word is expanded to produce a pattern just as in pathname expansion. If the pattern matches the beginning of the value of parameter, then the result of the expansion is the expanded value of parameter with the shortest matching pattern (the ``#'' case) or the longest matching pattern (the ``##'' case) deleted. If parameter is @ or *, the pattern removal operation is applied to each positional parameter

in turn, and the expansion is the resulting list. If the parameter is an array variable subscripted with @ or *, the pattern removal operation is applied to each member of the array in turn, and the expansion is the resulting list.

So the ##-case expands to the longest matching pattern deletion. Since the parameter is *, it removes all matching patterns in the array, until it has no matches left. You read in the entire pathname as an array which has a delimiter "/" and the final result is the filename only.

This would mean that /foo/bar/filename.pdf would result in filename.pdf, but if the input would have a trailing slash like so: /foo/bar/files/ it would return nothing.

At times {file##*/} can be used as a shell-built-in alternative for the command basename. But as you see, this scenario shows the difference between basename and {file##*/}.

Question 88: Catching All Exit Codes

I have a Unix Script that has several exits in the middle, each returning separate exit codes. I have to catch the entire exit's and perform an operation say "Mail the status code" before the actual code completes.

How can I do this in KSH ?

A: Introduce a function to catch all the exit codes.

Something like:

Code:

EXIT_CODE="" function assembleExitCode { EXIT_CODE="${EXIT_CODE} $@" }

At every place where you are looking for an exit code, invoke the function as:

assembleExitCode $?

At the end of the code:

if [[ x"$EXIT_CODE" != x ]] ; then echo "Mail status" fi ;

Question 89: Converting Text File into XML

The file has fields with each field having a certain number of bytes, but the fields are not delimited by anything (e.g., whitespace). I need to get those fields into some sort of data structure so that I can use them to generate the XML using a simple for loop. The following is an example of what I am looking at:

Jack Johnson 90980288Harv 9090998

Joe Joie 8989 Sed 99488

I can't use whitespace as a delimiter. How can I convert a file into xml format using Unix shell scripts?

A: Try something like this:

Code:

#!/bin/ksh

cat - <<! >data.txt

Jack Johnson 2005-02-11Harv9090998

Joe Joie2005-01-23Sed 0099488

!

awk ' BEGIN {[print](http://www.dbforums.com/showthread.php?t=1117910) "<?xmlversion=""1.0""?>";print "<ROWSET>"}

{print "<ROW>"

print "<NAME>" substr($0,1,20) "</NAME>"

print "<TRN_DATE>" substr($0,21,10) "</TRN_DATE>"

print "<TEXT>" substr($0,31,10) "</TEXT>"

print "<ID>" substr($0,41,7) "</ID>"

print "</ROW>";}

END { print "</ROWSET>";}' data.txt >data.xml

To strip out the leading and trailing whitespace from the each string before having it print out, do this:

Code:

function trim(str)

{

sub("^[ ]*", "", str);

sub("[ ]*$", "", str);

return str;

}

Question 90: Back Up Log Files

My log files have become too large and need to be backed up and compressed. Renaming the file with mv will mess up any links to the file and could disrupt servers using the logs. If servers are expected to be running 24/7, renaming is not an option.

How can I do this?

A: Here is a possible solution:

suffix=`date +%Y%m%d%H%M%S`.bak

newFileName=${YourLogName.log}.${suffix}

cp -p YourLogName.log $newFileName

cp /dev/null YourLogName.log

compress $newFileName

A copy of your log is made and compressed and the log file is initialized (emptied) and ready for more messages. Processing can continue without interruption. I suppose there is a possibility of a few messages being dropped, so do this during times of slow usage with a crontab entry.

Question 91: Stop Simultaneous Execution of the Same Script

How can I simultaneously stop execution of the same script?

A: Try this procedure:

My_pid=$$

print $My_pid >> temp.file

read input_pid < temp.file

if [[ "$input_pid" == "$My_pid" ]] then

(allow the script to continue)

else

(exit the script, My_pid was not 1st)

fi

This guarantees that the first instance of the script submitted will run and any other occurrences of the same script will exit. Remove temp.file before the script ends and I suggest using a Trap. It’s better than trying to deal with ps/grep and it makes a nice little function.

If only one instance of a script should run at a given time, a lock directory could be used to ensure mutual exclusion:

lockname=/tmp/myscript.lock

if mkdir "$lockname"

then

echo >&2 "aquired lock; continuing"

# Remove lock directory when script terminates

trap 'rmdir "$lockname"' 0

trap "exit 2" 1 2 3 15

else

echo >&2 "lock already held"

echo >&" "another script instance running?"

exit 1

fi

This can be extended to write the current process id to a file in the lock directory. This way, another instance can check if the process that acquired the lock is still running.

Question 92: Displaying Script Command with Output

We have hundreds of lines in the script which we would like to see along with the output, and don't want to have to put displays in every line manually.

How do you display the script command for a particular output result? Is there an editor that will allow for an echo or sysout of the script that causes an output result?

A: You could try set -x.

man set

SYNOPSIS

sh

set [ --aefhkntuvx [ argument ] ] ...

unset [ name ... ]

export [ name ... ]

csh

set [ var [ = value ] ]

set var [ n ] = word

unset pattern

setenv [ VAR [ word ] ]

unsetenv variable

ksh

set [ +aefhkmnopstuvx ] [ +o option ] ... [ +A name ] [

arg ... ]

unset [ -f ] name ...

**export [ name [ =value ] ] ...

Question 93: Build Text File with Calendar Dates

Is there a way to build a text file which will contain the dates of 2 years in the format YYYYMMDD using korn shell?

For example, to generate a file with the contents:

20010101

20010102

20010131

20010201

20010228

20010301

and so on.

A: Use the following code:

#! /usr/bin/ksh

# ja fe ma ap ma ju ju ag se oc no de

set -A lasts 0 31 28 31 30 31 30 31 31 30 31 30 31

typeset -Z2 dmonth dday

# # loop on years

year=2001

while ((year<2003)) ; do

# # is this a leap year?

leap=0

if ((!(year%100))); then

((!(year%400))) && leap=1

else

((!(year%4))) && leap=1

fi

#

# set number of days in February

lasts[2]=28

((leap)) && lasts[2]=29

#

# loop on month month=1

while ((month<13));

do # # loop on day day=1

while((day<(lasts[month])+1)) ;

do dday=$day dmonth=$month

echo ${year}${dmonth}${dday} ((day=day+1))

done ((month=month+1))

done

((year=year+1))

done

exit 0

Question 94: grep in a Loop

I am trying a script which takes user input userid. I am stuck on how to check whether that is a valid user id or not in the audit log files.

Here is my code:

cd $CCP_AUDIT

cat * > /export/home/$USR/l***/files

echo "UserId:\c"

read UserId

#Date Function

echo "DATE [YYYY-MM-DD] : \c"

read xxx

I need help in putting this in a loop:

grep $xxx /export/home/$USR/lalitha/files |grep -v Created |grep -v Rejecte

d | grep -i $UserId | Mail -s "Transactions for $UserId" ***@***.com

~

How do I break out of the loop if there is no log entry for a given user?

A: I'm taking this to mean there are zero lines in the resulting output.

This is where a temporary file makes sense. You need the same intermediate data for 2 different purposes:

Code:

grep ... > tempfile

if [ -s tempfile ]; then

Mail ... < tempfile

else

echo No such userid $UserId >&2

break

fi

rm tempfile

Question 95: Generating a List of Choices in a Menu

I'm creating a text file (systems.txt) with a list of servers in it by hostname. Then I would like to echo a menu with each hostname and a number to use to pick it from the list. It's somehow associating the number with the hostname that is confusing me.

Here is my code:

#!/bin/bash

clear

COUNT=0

SYSTEMS=`cat systems.txt`

while [ "$CHOICE" != "q" ]

do

for SYSTEM in $SYSTEMS

do

COUNT=`expr $COUNT + 1`

echo "$COUNT. $SYSTEM"

done

echo ""

echo "Please choose."

echo ""

read CHOICE

COUNT=0

clear

done

What I have so far is:

1\. host1

2\. host2

3\. host3

Please choose.

3

What I'd like is:

1\. host1

2\. host2

3\. host3

Please choose.

3

You picked host3!

The hostnames are not always host* of course, so I can't use that as a convention for the script to know which server I mean.

How should I continue?

A: Assuming your '/tmp/hosts.txt' contains:

Code:

host1

host2

host3

host4

Here’s one way of creating a menu:

Code:

#!/bin/ksh

hosts='/tmp/hosts.txt'

PS3="Pick one of the above: "

select i in $(< ${hosts})

do

[ $i ] && print "you picked->[${i}]" || print -u2 'invalid selection'

clear

ssh -X ${i}

nl -s') ' "${hosts}"

done

Question 96: Delete Empty Files in a Shell Script

I'm trying to figure out a way to delete empty files in a directory. I have a cron that runs and creates a flat file every 15 minutes. However, most times at night the flat file will be empty.

How can I run a script to delete empty files that end with *.dat?

A: Try doing this:

Code:

find ./ -name "*.dat" -size 0 -exec rm {} \;

Read your man page before invoking this so you understand the implications. Find goes through sub-directories by default and if you don't put the {} \; correctly, it will cause problems. For example, it could start deleting things you did not want to delete.

Question 97: Replace a Line in a File

I have a property file in which the DB name is specified and when I run my servers they will point to the DB specified in that property file. Now I’m going to write a script which will start all the services. But before that I just want to dynamically change the DB name in that property files by getting as command line argument of my script.

Say this is the line in that property files as:

Application.Database = snowdropDB

This line should be modified with the command line argument of my script. If I call the script like this:

startup tulipDB

First, the script should modify that line of the property file as:

Application.Database = tulipDB - and should start the services.

How do I modify a line of a file thru script?

A: Let prop_file is name of your property file.

File prop_file contains the following line with other contents.

Application.Database=snowdropDB

Make shell sript file startup.sh

Shell script startup.sh contains

sed "s/Application.Database=.*/Application.Database=$1/g" prop_file > tmp

mv tmp prop_file

Execute

sh startup.sh tulipDB

All occurrences of snowdropDB will get replaced by tulipDB.

Question 98: Shrinking a File

I have a file containing about 1 million records. The records in the file are of fixed length. Every record begins with 03, 04, 05, or 06.

03 record is the parent record. 04, 05 and 06 are child records. Every 03 record can have zero, one or more than 1 child record.

The position 12:16 of 03 record indicates the TYPE. Every record has a TYPE. There are about 10 unique file TYPEs in the whole file.

Now my requirement is that:

IF number of 03 records for a particular TYPE is less than 100, then ALL the 03 records for that TYPE along with their CHILD records should be written to a new file.

IF number of 03 records for a particular TYPE is more than 100, then ONLY 2% of the 03 records(selected randomly) for that TYPE along with their corresponding CHILD records should be written to a new file.

Please note that all the records need to go to a single file.

Is this possible to achieve using shell scripts?

A: This can be done in most languages. I would go with C mostly based on file size. If not c, then I would use ksh. The choice of language really is just a personal choice.

This task is tough enough that it will require a real programmer. You say that you have worked on a few simple shell scripts. Unless you have several years of programming experience in some procedural language it's unlikely that you will succeed.

To answer your question, you need to make a pass though the file creating lists of each of the types of 03 records. Then you need to examine the lists. If a list has less then 100 items, all items on the list will be marked ok. If the list has over 100 items, only some will be marked ok.

Since you counted the elements, you can compute 2% of that number. Now you know how many to mark ok.

To mark one ok, generate a random integer between 1 and n where n in the number of non-ok elements in the list. Now scan the list from element 1 to the end and find the selected element. Mark it ok. Subtract one from your number of non-ok elements on the list. Generate a new random integer between 1 and current number of non-ok elements. Find that one. And so on until you have marked the required number ok.

After you have done this with each list, go back to main file. For each 03 record, see if it's marked ok on the lists. If so, write it and the child records to the final output file.

Question 99: awk in Shell Script

I have an awk script contained within a ksh script that I want to read the contents of a file with, say 3 records. Fields are a, b, and c, delimiter '|'.

I want to read the file and then I want to set different variables for $1, $2, $3 to be used as parameters to run a series of reports outside the scope of the awk script but within the same ksh script.

Here's part of what I have:

# Run each of the reports in series (3 total) for each record:

awk '

BEGIN{FS="|";FILENAME="$loc/myfile"}

split(FILENAME,results,FS)

a=results[1]

b=results[2]

c=results[3]

etc…

How do I execute the rest of a command within/outside of?

A: I cannot understand your code, but I gather that you have a file with three data fields per line and the fields are delimited by | like this:

1|2|3

4|5|6

I think that you want to loop and set a=1, b=2, and c=3 on the first loop and a=4, b=5, and c=6 on the second loop. That is easy.

Code:

/usr/bin/ksh

exec < inputfile

IFS='|'

while read a b c ; do

echo a = $a

echo b = $b

echo c = $c

done

exit 0

I don't see an easy way to inject awk into something like this.

Question 100: while Loop

In a text file (PL_SENDEVENT), I have the following line:

CHANGE_STATUS INACTIVE

And another file (PL_JOBS) with the following lines:

TEST

TEST1

What I'm trying to do is change the STATUS of TEST and TEST1 to the status that I specify in the file which is INACTIVE (or IN) in this case. I do not want the script to exit until both jobs have been verified that they are in an INACTIVE (IN) status. It is not going well so far. As it stands, it exits successfully once it sets TEST to INACTIVE and doesn't even check TEST1\. If the jobs are not in an INACTIVE status, I want it to check again until they both are.

Here’s what I have now:

Code:

cat $PL_DIR/PL_SENDEVENT | while read event status

do

case $event in

CHANGE_STATUS)

cat $PL_DIR/PL_JOBNAME | while read job

do

sendevent -E CHANGE_STATUS -s ${status} -J ${job}

done

case $status in

INACTIVE) export ST=IN ;;

ON_HOLD) export ST=OH ;;

ON_ICE) export ST=OI ;;

TERMINATED) export ST=TE ;;

*) echo "Invalid Status!"; exit 1 ;;

esac

rc3=1

while (($rc3 > 0))

do

sleep 5

cat $PL_DIR/PL_JOBNAME | while read job

do

$AUTOSYS/bin/autorep -J ${job} -l0 | sed '1,4d' |

if [ `awk '{print $6}'` == ${ST} ]; then

echo "Status is set for ${job}!"

rc3=0

fi

done

done ;;

What am I doing wrong?

A: Try replacing the last part with this:

Code:

rc3=1

while (($rc3 > 0))

do

sleep 5

rc7=0

cat $PL_DIR/PL_JOBNAME | while read job

do

$AUTOSYS/bin/autorep -J ${job} -l0 | sed '1,4d' | \

if [ `awk '{[print](http://www.dbforums.com/showthread.php?t=1074468) $6}'` == ${ST} ]; then

echo "Status is set for ${job}!"

(( rc7 += 1 ))

fi

done

[ $rc7 == `wc -l $PL_DIR/PL_JOBNAME` ] && rc3=0

done

Acknowledgements

All the foregoing was culled from the following websites:

[http://en.wikipedia.org/wiki/Unix_shell](http://en.wikipedia.org/wiki/Unix_shell)

[http://heather.cs.ucdavis.edu/~matloff/UnixAndC/Unix/CShellII.html](http://heather.cs.ucdavis.edu/~matloff/UnixAndC/Unix/CShellII.html)

[http://steve-parker.org/forum/viewforum.php?f=2](http://steve-parker.org/forum/viewforum.php?f=2)

[http://www.injunea.demon.co.uk/pages/page203.htm](http://www.injunea.demon.co.uk/pages/page203.htm)

[http://www.dbforums.com/forumdisplay.php?f=13](http://www.dbforums.com/forumdisplay.php?f=13)

[http://www.unix.com/index.php](http://www.unix.com/index.php)

[http://www.tek-tips.com/threadminder.cfm?pid=822](http://www.tek-tips.com/threadminder.cfm?pid=822)

[http://www.shelldorado.com/](http://www.shelldorado.com/)