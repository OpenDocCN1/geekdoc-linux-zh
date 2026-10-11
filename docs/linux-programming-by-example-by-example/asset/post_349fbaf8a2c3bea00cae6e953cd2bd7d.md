
# Linux Programming by Example
Kurt Wall

201 West 103rd Street
Indianapolis, Indiana 46290

![](img/be588b36b489136ce784030a08a1d3d4_0_0.png)

![](img/be588b36b489136ce784030a08a1d3d4_1_0.png)

# Copyright © 2000 by Que® Corporation

All rights reserved. No part of this book shall be reproduced, stored in a retrieval system, or transmitted by any means, electronic, mechanical, photocopying, recording, or otherwise, without written permission from the publisher. No patent liability is assumed with respect to the use of the information contained herein. Although much precaution has been taken in the preparation of this book, the publisher and author assume no responsibility for errors or omissions. Neither is any liability assumed for damages resulting from the use of the information contained herein.

International Standard Book Number: 0-7897-2215-1

Library of Congress Catalog Card Number: 99-64403

Printed in the United States of America

First Printing: December, 1999

01 00 99 4 3 2 1

# Trademarks

All terms mentioned in this book that are known to be trademarks or service marks have been appropriately capitalized. Que Corporation cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

# Warning and Disclaimer

Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied. The information provided is on an "as is" basis. The authors and the publisher shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book.

# Associate Publisher

Dean Miller

# Executive Editor

Jeff Koch

# Acquisitions Editor

Gretchen Ganser

# Development Editor

Sean Dixon

# Managing Editor

Lisa Wilson

# Project Editor

Tonya Simpson

# Copy Editor

Kezia Endesley

# Indexer

Cheryl Landes

**Proofreader**
Benjamin Berg

**Technical Editor**
Cameron Laird

**Team Coordinator**
Cindy Teeters

**Interior Design**
Karen Ruggles

**Cover Design**
Duane Rader

**Copy Writer**
Eric Borgert

**Production**
Dan Harris
Heather Moselman

# CONTENTS AT A GLANCE

**Introduction 1**

**Part I**  
**The Linux Programming Environment 5**

1. Compiling Programs 7

2. Controlling the Build Process—GNU make 33

3. About the Project 55

**Part II**  
**System Programming 59**

4. Processes 61

5. Signals 93

6. System Calls 119

7. Basic Linux File Handling 131

8. Advanced Linux File Handling 157

9. Daemons 191

**Part III**  
**Linux APIs (Application Programming Interface) 201**

10. The Database API 203

11. Screen Manipulation with ncurses 219

12. Advanced ncurses Programming 249

13. The Sound API: OSS/Free 277

14. Creating and Using Programming Libraries 297

**Part IV**  
Interprocess Communication 317

15. Pipes and FIFOs 319

16. Shared Memory 339

17. Semaphores and Message Queues 353

18. TCP/IP and Socket Programming 375

**Part V**  
Linux Programming Utilities 405

19. Tracking Source Code Changes: The Revision Control System 407

20. A Debugging Toolkit 423

21. Software Distribution 443

22. Programming Project: A Music CD Database 461

**Part VI**  
Appendices 495

A. Additional Resources 497

B. Additional Programming Tools 507

Index 513

# TABLE OF CONTENTS

Linux Programming by Example 1

About This Book 1

Who Should Read This Book... 2

Linux Programming by Example, Chapter by Chapter 2

# Part I

## The Linux Programming Environment

1. Compiling Programs 7
    - Using GNU cc (gcc) 8
    - Invoking gcc 8
    - Example 8
    - Invoking gcc Step by Step 10
    - Example 11
    - Using Multiple Source Code Files 12
    - Example 12
    - Options and Arguments 14
    - Examples 16
    - GNU C Extensions 22
    - Examples 24
    - Using egcs 28
    - Enhancements to gcc 29

2. Controlling the Build Process—GNU make 33
    - Why make? 34
    - Using make 34
    - Creating Makefiles 35
    - Example 36
    - Invoking make 37
    - Examples 38
    - Creating Rules 40
    - Phony Targets 40
    - Examples 41
    - Variables 41
    - Example 42
    - Examples 44
    - Example 45
    - Example 46
    - Example 47
    - Implicit Rules 48
    - Example 48
    - Pattern Rules 49
    - Example 49
    - Comments 50
    - Useful Makefile Targets 50
    - Example 51
    - Handling Errors 52

3. About the Project 55
    - The Music CD Database Program 56
    - Components and Subsystems 56

# Part II

## System Programming 59

4. Processes 61
    - What Is a Process? 62
    - Process Attributes 62
    - Process Identifiers 62
    - Example 63
    - Real and Effective IDs 64
    - Examples 65
    - `setuid` and `setgid` Programs 66
    - User Information 67
    - Example 67
    - Additional Process Information 69
    - Sessions and Process Groups 76
    - Manipulating Processes 77
        - Creating Processes 77
        - Example 83
        - Waiting on Processes 84
        - Example 85
        - Killing Processes 86
        - When to Manipulate Processes 89

5. Signals 93
    - Signal Concepts 94
    - What Is a Signal? 94
    - Signal Terminology 94
    - Signal History 95
    - Available Signals 95
    - Sending Signals 99
        - Using the `kill` Command 99
        - Example 99
        - Using the `kill` Function 100
        - Example 101
    - Catching Signals 102
        - Setting an Alarm 102
        - Examples 103
        - Using the `pause` Function 105
        - Example 105
        - Defining a Signal Handler 106
        - Examples 107
        - Examples 111
        - Detecting Pending Signals 114
        - Example 114

6. System Calls 119
    - Understanding System Calls 120
    - What Is a System Call 120
    - System Call Limitations 121
    - Why Use System Calls 121
    - Using System Calls 122
    - Common System Calls 122
    - System Call Return Codes 124
    - Examples 124
    - Table of System Call Error Codes 124
    - Handling Errors 126
    - Examples 127

7. Basic Linux File Handling 131
    - Characteristics and Concepts 132
    - The File Mode 134
    - Example 137
    - The File-Handling Interface 138
    - Opening and Closing Files 139
    - Example 140
    - Reading and Writing Files 141
    - Example 141
    - Positioning the File Pointer 143
    - Example 143
    - Truncating Files 145
    - Example 146
    - Getting File Information 147
    - Example 149
    - Changing File Characteristics 151
    - Examples 152

8. Advanced Linux File Handling 157
    - Changing File Timestamps 158
    - Example 159
    - Features of the ext2 Filesystem 160
    - Example 161
    - Working with Directories 163
    - Changing Directories 163
    - Examples 163
    - Creating and Removing Directories 165
    - Examples 166
    - Listing a Directory 167
    - Example 168
    - I/O Multiplexing 169
    - Example 171
    - Memory Mapping Files 174
    - Creating a Memory Map 175
    - Example 177
    - Using a Mapped File 179
    - Example 180
    - File Locking 182
    - Lock Files 183
    - Example 184
    - Record Locking 185
    - Example 187

9. Daemons 191
    - Understanding Daemons 192
    - Creating a Daemon 192
    - Function Calls 193
    - Example 194
    - Handling Errors 196
    - Example 198

# Part III

## Linux APIs (*Application Programming Interface*)

10. The Database API 203
    - The Berkeley Database
    - Creating, Opening, and Closing a Database
        - Creating and Opening a Database
        - Closing a Database
        - Example
    - Storing Items in a Database
    - Example
    - Deleting Items in a Database
    - Example
    - Retrieving Items from a Database
    - Example
    - Navigating a Database
    - Syncing a Database
    - Example

11. Screen Manipulation with ncurses 219
    - ncurses' Features
        - Terminal Independence
        - Capabilities
    - Compiling with ncurses
