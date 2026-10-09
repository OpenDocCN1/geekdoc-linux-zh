
**ec_eof** macro, 35

**EC_FAIL** macro, 36

**ec_false** macro, 35

**ec_flush** macro, 36

echo on/off, 239

**ec_negl** macro, 35

**ec_null** macro, 35

**ec_print** macro, 36

**ec_push** macro, 36

**ec_reinit** macro, 36

**ec_rv** macro, 35

**ec_warn** macro, 36

effective group-ID, 10

effective user-ID, 9

*endhostent*, 578

*endnetent*, 586

*endprotoent*, 588

*endservent*, 590

environment, 277–283

*errno*, 24–29

error checking, 24–29
C. macros, 29–36
error handling, error checking, 24–29
event flags, poll and, 219
events. pyxa, 268
example code, 67–68
exceptions, C++, 36–38
exec system calls, 284–292
**execl**, 285
**execle**, 289
**execlp**, 288
**execv**, 288
**execve**, 289
**execvp**, 288
signals and, 623–624
execute permissions, 10
*symls*, 75–76
execution time, 63
**clock**, 64
**struct timespec**, 64
**struct time**, 64
*times*, 64
exit system calls, 301–304

## F

*fcfdil*, 166–168
*fchmod*, i-nodes and, 182
*fchown*, 182–184
*fcntl*, 187–189
file locking and, 485–486
*fdatasync*, 116–117

*FIFOs*, 15. See also named pipes
- advantages/disadvantages, 414
- creating, 407–408
- examples, 408–413
- introduction, 406–407
- performance comparison, 515–517
- pipes and, 363–371
- SMI implementation, 420–428
- *sockets*, 520

file attribute functions, 693–694
*fd* descriptors, 12
- duplicates, 371–375
- *metadata* and, *fstat*, 147–154
- numbering, 72
- opening, 74–75
- sharing, 74–75
- *standard*, 73
- uses, 73–74

file I/O functions, 694
file I/O functions (asynchronous), 694
file locks, 13, 15, 477–481
- databases, 488
- *fcntl*, 485–486
- semaphores as, 481–483

file management functions, 695
file objects
- locks, 13, 15
- messages, 13, 15
- semaphores, 13
- shared memory, 13, 15–16
- *sockets*, 13

file offset, 2, 90–92
file permission bits, *symls*, 75–76
file size limit, 13
file system functions, 695
file systems, 124
- access, low-level, 127–131
- mounting, 135–137
- unmounting, 135–137

file tree
- walking down (*ftw*), 174–180
- walking up (*getcwd*), 170–174

file-descriptor set functions, 695
files
- as locks, 80–85
- access times, 184–185
- buffers, 4
- bytes, inserting in middle, 2
- creating, 77–80, 186–187
- directories, 2–4
- header files, common header file, 55–56

# Index

# 707

files (*cont.*)
- i-numbers, 2
- metadata
    - accessing, 147–158
    - displaying, 147–158
- mknod facility, 186–187
- opening, 76–77
- owners, changing, 182–184
- regular, 1–2
- renaming, 139–141
- semaphores, 2, 458
- shared file offsets, 13
- special, 4–5
    - block, 4
    - character, 4
    - symbolic links, 2–4
- temporary, creating, 88–90
- text files, 5

flags, open flags, 85
- synchronized I/O and, 117–119

fork, 284, 296–300
- signals and, 623–624

fpathconf, 52
fstat, 147–154
fstatvfs, 131–135
ftok, 429–431
ftruncate, 119–120
ftw, implementation, 174–180
full-screen applications, 250–255
function calls, 881, 550–551
functions, 23
- aio_cancel, 194
- aio_error, 193
- aio_fsync, 194–195
- aio_read, 192
- aio_return, 193
- aio_suspend, 195–196
- aio_write, 192
- alphabetic listing, 685–693
- async-signal-safe, 616
- calendar time
    - asctime, 59
    - ctime, 59
    - difftime, 60
    - get_date, 60
    - gmtimeofday, 58
    - gmtime, 58
    - localtime, 58
    - mstime, 59
    - strftime, 59
    - struct timeval, 58
    - struct tm, 58
    - time, 58
    - wait4time, 59
- categorical listing, 693–702
- clock_getres, 661
- clock_gettime, 661
- clock_settime, 661
- configuration functions, 693
- Curses functions, 254–255
- directory I/O function, 693
- directory management, 693
- endhostent, 578
- endnetent, 586
- endprotoent, 587
- endservent, 590
- execution time
    - clock, 64
    - struct timespec, 64
    - struct tm, 64
    - times, 64
- file attributes, 693–694
- file I/O, 694
- file I/O (asynchronous), 694
- file management, 695
- file system, 695
- file-descriptor set, 695
- gai_strerror, 541
- getenv, 279
- gethostbyaddr, 581–582
- gethostbyname, 580–581
- gethostent, 578
- gethostid, 583–584
- getnameinfo, 582–583
- getnetent, 586
- getprotoent, 589
- getprotobynumber, 589
- getprotoname, 587
- getservbyname, 590
- getservbyport, 590
- getservent, 590
- if_freenameindex, 591
- if_indextoname, 593
- if_nameindex, 591
- if_nametoindex, 592–593
- inet_addr, 536–537
- inet_ntoa, 536–537
- inet_ntop, 596–597
- inet_pton, 596–597
- IPC-POSIX message queue, 695
- IPC-POSIX shared memory, 695
- IPC-System V message queue, 696
- IPC-System V semaphore, 696
- IPC-System V shared memory, 696
- library functions, calling, 22–23
- llio_listio, 199–200
- lock, 81
- lockpath, 82
- longjmp, 648–651
- mkstemp, 88–90
- network databases, 696–697
    - host functions, 578–585
    - network functions, 585–587
- process attributes, 697
- process control flow, 697
- process environment, 697
- process limit, 697
- process management, 698
- process permission, 698
- process resources, 698
- putenv, 280
- recv, 593–594
- send, 593–594
- setenv, 280–281
- sethostent, 578
- setjump, 648–651
- setnetent, 586
- setprotoent, 586
- setservernt, 589
- sigaddset, 608
- sigdelset, 608
- sigemptyset, 608
- sigfillset, 608
- sigismember/set, 609
- signal masks, 698–699
- signals, 698–699
- sockets, 699, 700
- tcgetattr, 233
- tcsetattr, 233
- terminal, 700
- terminal (Py), 700
- thread, 701
- time, 701–702
- timers, 702
- tmpnam, 88–90
- uname, 584
- unloc_k, 81
- unsetenv, 280–281
- user buffering and, 100–105
- user info, 702

## G

- gai_strerror, 541
- gathe rwrite, 110
- generating signals, synthetically, 621–623
- get date, 60
- getaddrinfo, 540–543
- getcwd, 145–147
    - implementation, 170–174
- getegid, 315–316
- getenv, 279
- geteid, 315–316
- getgid, 315–316
- getgrgid, 154–155
- getgrbyaddr, 581–582
- gethostbyname, 580–581
- gethostent, 578
- gethostid, 583–584
- gethostname, 543–544
- getlogin, 154–155
- getnameinfo, 582–583
- getnetent, 586
- getpeername, 594
- getpgrd, 228–229
- getpid, 319
- getppid, 319
- getprotobynumber, 589
- getprotobyname, 589
- getprotent, 587
- getpvo id, 154–155
- getrlimit, 323
- getruusage, 328
- getservbyname, 590
- getservbyport, 590
- getservent, 590
- getxid, 227
- getxokname, 594
- gettimeofday, 58
- gettimer, 658
- getuid, 315–316
- global jumps, 648–651
- gmt ime, 58
- group files, 10
- group IDs
    - setting, 317–318
    - system calls, 315–316

group-1D, 9

groups, users, 9

GUIs (Graphical User Interfaces), 250

## H

hard links
- creating, 138–139
- introduction, 137–138
- renaming and, 139–141

header files
- common header file, 55–56
- system calls, 20

host functions, network databases, 578–585

HTTP (HyperText Transfer Protocol), SSI and, 551–552

## I

identifiers, System V IPC, 429–431

IEEE (Institute of Electrical and Electronics Engineers), 17

if_freenameindex, 591

if_indextoname, 593

if_nameindex, 591

if_nametoindex, 592–593

implementation
- shells
    - exec, 292–296
    - fork, 300–301
    - waitpid, 314–315
- SML, sockets and, 563–566
- SSI, 559–563

inet_ntoa, 536–537

inet_addr, 536–537

inet_ntop, 596–597

inet_pton, 596–597

i-nodes
- changing, 181
- chmod and, 182
- chown and, 182–184
- device number, 4
- fchmod and, 182
- fchown and, 182–184
- lchown, 182–184
- System V IPC, 429

instructions, 5

interfaces, semaphores, 463–469

interprocess communication, introduction, 361–362

interrupted system calls, signals and, 607–608

i-numbers, files, 2

links, 3

I/O (input/output)
- asynchronous, 189–200
- buffered versus unbuffered, 104
- disk special files, 123–127
- overview, 71–72
- pipes and, 363–371
- STREAMS I/O, 255
- synchronized, versus synchronous, 114
- terminal I/O (See terminal I/O)
- user buffering
    - functions, 100–105
    - kernel buffering and, 98–100

ioctl, 1, 232–233

IPC (interprocess communication), 405.
*See also System V IPC*

IPC-POSIX
- message queue functions, 695
- semaphore functions, 695
- shared memory functions, 696

IPC-System V
- message queue functions, 696
- semaphore functions, 696
- shared memory functions, 696

ia tty, 249

## J

Java, 21

job control, 8, 225

jobs, 8

jumps, global, 648–651

## K

kernel buffered I/O, user buffering and, 98–100

keys, System V IPC, 429–431

## L

lchown, 182–184

lexical analyzer, shells, 377–381

library functions, calling, 22–23

limiting processes, 322–329

links
- directories
    - multiple, 3–4
    - removing, 86–87
- hard links, 137–138
    - creating, 138–139
    - renaming and, 139–141
- i-numbers and, 3
- symbolic links, 2–4, 3–4, 137–138
    - creating, 141–144
