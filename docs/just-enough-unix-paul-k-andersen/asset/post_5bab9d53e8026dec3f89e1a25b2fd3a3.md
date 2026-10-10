
### G.2 Running make

The first thing to do with make is to remove the executable and object files that were produced when you compiled the Trip program the first time. Try the `ls` command to see the files in Trip:

```
$ ls (Return)
```

You should see something like this:

```
a.out    indiana.c    indy.o     main.o
chicago.c  indiana.o    main.c    makefile
chicago.o  indy.c
```

Now get rid of the old object files:

```
$ make clean (Return)
```

The "clean" dependency line in makefile causes the following command line to run:

```
rm *.o
```

Use the `ls` command now to list the files remaining in Trip:

```
$ ls (Return)
```

You should see:

```
a.out    indiana.c    main.c
chicago.c  indy.c     makefile
```

Note that make did nothing to the old executable file a.out, because it was not instructed to do so.

Next, use make to compile the program. Simply type `make` and press (Return):

```
$ make (Return)
```

make then follows the instructions in makefile to compile the program:

```
cc -c main.c
cc -c chicago.c
cc -c indiana.c
cc -c indy.c
cc -o trip main.o chicago.o indiana.o indy.o
```

Note that the files are not necessarily compiled in exactly the same order as they appear in makefile; instead, make figures out which files should be compiled first. Try the `ls` command to see the files in Trip:

```
$ ls (Return)
```

You should see something like this:

```
a.out    indiana.c    indy.o     makefile
chicago.c  indiana.o    main.c    trip
chicago.o  indy.c       main.o
```

`trip` contains the new executable code, which you can run simply by typing `trip`, followed by **Return**:

```
$ trip (Return)
```

The advantage of using `make` to compile the files becomes apparent when you begin making alterations in any of the source files. When you are finished, all you have to do is type `make`, and `make` will automatically recompile only those files that need it. And if you have not made any changes in the program, `make` will take no action. To see how this works, try running `make` again:

```
$ make (Return)
```

Assuming you have not made any changes in the files, you should see a message such as:

'trip' is up to date. (Return)

## INDEX

### Symbols

- " (double quotes) 100
- # (alternative shell prompt) 30, 46
- # (in comments) 230, 233, 253
- #!/bin/sh 254
- $ (Bourne or Korn Shell prompt) 30, 46
- $ (variable value) 100, 224, 232, 242
- $# (number of arguments) 256
- $* (command-line arguments) 256, 262
- % (C Shell prompt) 30
- & (background processing) 47, 100
- & (mail prompt) 33, 51, 165
- @ (alternative shell prompt) 30, 46
- * (Fortran comment) 299
- * (wildcard) 98
- . (current directory) 61, 62, 63
- . ("dot" command) 234, 270
- .. (parent directory) 61, 62, 63
- / (in pathnames) 61, 62
- ; (alternative shell prompt) 30, 46
- ‖ (pg prompt) 71
- < (input redirection) 253
- > (alternative shell prompt) 30, 46
- > (output redirection) 66, 70
- >> (append output) 73
- ? (mail help) 169
- ? (mail prompt) 165
- ? (telnet help) 177
- ? (wildcard) 98
- @ (alternative shell prompt) 30, 46
- [] (wildcard) 98
- \ (backslash) 100
- ^\ (telnet escape sequence) 177
- ^D (Logging out) 34
- ^Q key combination 34, 35
- ^S key combination 53
- ` (backquotes) 100, 257
- | (OR operator) 262
- | (pipe) 95, 326
- || (OR operator) 261
- ~ (mail escape) 163, 173
- ~ (in pathnames) 61

### A

- a.out 280, 285, 300
- A/UX 19
- Absolute or full pathnames 59
- Account
  - login name 16
  - name 16
  - password 16
- Active window 46
- Advanced Research Projects Agency (ARPA) 152
- AIX 19
- alias command 239
- Aliases 229, 237, 239
- America Online 152
- American Standard Code for Information Interchange (ASCII) 158
- Ampersand (&) 100
- Anonymous ftp 186
- Append (>>) 73
- Apple Computer 19
- Apple Macintosh 8, 10
- archie 190
- Archive files 188
- Argument 93
- ARPA (Advanced Research Projects Agency) 152
- ARPANET 152
- ASCII (American Standard Code for Information Interchange) 158
- ASCII files 184, 185
- Assembly language 9, 277
- Asterisk wildcard (*) 98
- AT&T 186
- AT&T Bell Laboratories 9, 20
- AT&T System V 19, 20
- Automatic variables 255

### B

- Backbone 149, 152
- Background processing 8, 100
  - running a window 47
- Backquotes (`) 99, 257
- Backspace key 21, 30
- Berkeley Mail 155
- Berkeley Software Distribution (BSD) UNIX 19
- bifit utility 174
- Binary digits 5
- Binary files 184, 185, 189
- Binary numbers 277
- Bit 5
- BITNET 153
- Bookmark 207
- Bourne Shell (sh) 91
  - $ prompt 30, 46
  - .profile 222, 231, 233
  - comment 230, 233
  - exit command 34
  - export command 224
  - logging out 34, 35, 52
  - prompt 30
  - PS1 variable 231, 234, 239
  - PS2 variable 231, 232
  - shell prompt 30, 46
- (Break) key 21
- Browsers 156, 157
- Buffers 141, 142
- Bugs 280
- Byte 5

### C

- C programming 9, 277-298
  - a.out 285
  - arithmetic exceptions 288
  - cb ("C beautifier") 297
  - cc ("C compiler") command 285
  - cc -g 289
  - cc -Im 291
  - cc -O 286, 288
  - compiler 285
  - core 288
  - ctrace utility 297
  - executable code 285
  - hello.c 283
  - indiana.c 293
  - indy.c 293
  - library function 284, 287, 290
  - linker 285
  - lint 297
  - main() function 284
  - main.c 292
  - make 296, 343
  - object code 285
  - preprocessor 284, 285
  - recip.c 286
  - sqroot.c 289
  - stdio.h 284
  - system() function 296
  - time utility 298
  - Trip 291
- C Shell (csh) 91, 242
  - % prompt 30, 46
  - .cshrc 222, 223, 241, 243
  - .login 222, 223, 241, 243
  - .logout 222
  - /bin/csh 221, 242
  - alias 229
  - environment variable 241
  - history 227, 242
  - job number 112
  - logging out 34, 35
  - noclobber 250
  - prompt 30
  - setenv ("set environment") command 224
  - shell prompt 30, 46
  - startup files 241-250
  - variables 242
- Cache 213
- cal ("calendar") command 34, 51, 69, 70, 76
- calendar utility 227, 236
- Campus Area Network (CAN) 149
- Case sensitivity 36, 54
- cat ("catenate") command 70, 86, 85
- cb ("C beautifier") utility 297
- cc ("C compiler") command 285
- cd ("Change directory") command 85, 183, 184
- Central processing unit (CPU) 3, 5, 8
  - clock speed 5
  - flops 5
  - MIPS 5
  - word size 5
- Cert, Viton 152
- Changing directories 85
- Changing passwords 31, 35, 53
- Child 58
- chmod ("change mode") command 254, 329
- Classifying files 77
- Click-to-Focus 46
- Client 11
- Client-server model 11, 156
- Clock speed 5
- Collating sequence 109
- Command argument 93
- Commands 10
- Comments 230, 233, 253, 283, 299, 311
- Compilers and compiling 279
- Control files 222
  - .cshrc 222, 223, 241, 243
  - .exrc 222
  - .forward 222
  - .kshrc 222, 231, 233, 236
  - .login 222, 223, 241, 243
  - .logout 222
  - .mailrc 222
  - .newsrc 195, 222
  - .plan 222
  - .profile 222, 231, 233
  - .xinitrc 222
- **Control** key 21, 23
- Copying files 65, 76
- core 280
- cp (“copy”) command 65, 73, 76
  - cp -i (“copy interactively”) 240, 250
- CPU—see Central processing unit
- Cray 19
- Creating a file 64
- csh—see C Shell
- ctrace utility 297
- Current directory 57, 61
- Cursor 27
- cwd (“change working directory”) command 242

### D

- date command 32, 35, 49, 53, 99, 240, 257, 270
- dbx 281, 335
  - breakpoints 337
  - compiling with the -g option 335
  - cont (“continue”) command 337
  - core file 340, 341
  - edit command 336
  - help command 335
  - list command 337
  - print command 338
  - quit command 339
  - run command 336-337
  - sh command 340
  - step command 337
  - stop command 337
  - trace command 339
  - where command 341
- Debugger 280
- Default printer 74, 75
- Default terminal type 30
- **Delete** 21
- Dialog box 212
- Digital Equipment Corporation 19, 21
- Directories 10, 57
  - /bin 58
  - /dev 58
  - /etc 58
  - /home 58
  - /tmp 58
  - /usr 58
  - /var 58
  - absolute pathname 59
  - changing 85
  - child 58
  - creating 80, 82, 86
    - creating subdirectories 80
  - current 57, 61
  - dot (.) 61
  - dotdot (..) 61
  - file tree 57
  - full pathname 59
  - hidden 62
  - home 18, 57
  - invisible 62
  - making 80, 86
  - mode 331
  - moving files 81, 86
  - names 59
  - parent 58
  - pathname 59
  - removing 86
  - root 57, 58
  - subdirectory 58
  - working 57, 61, 86, 191
- Display manager 37
- Dollar sign ($) 224, 232, 242
- Domain names 154
- dot (.) 61, 62, 63
  - dot (.) command 234, 270
- dotdot (..) 61, 62, 63
- Double quotes (“...”) 100
- Dynix 19

### E

- echo command 99, 232, 239, 241, 242
- ed (text editor) 120
- Electronic mail 155
  - & prompt 33, 165
  - .forward 222
  - .mailrc 222
