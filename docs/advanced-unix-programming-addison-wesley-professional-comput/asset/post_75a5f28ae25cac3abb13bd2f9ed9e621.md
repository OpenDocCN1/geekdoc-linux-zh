
# Index

interrupted, 607–608

nanosleep, 657

pause, 624

pthread_create, 623–624

sigaction, 611–615

sigaltstack, 634

siglongjmp, 650–651

sigpending, 634

sigqueue, 643

sigsetjmp, 650–651

sigsuspend, 628–634

sigtimedwait, 643–646

sigwait, 624–628

sigwaitinfo, 643–646

sleep, 653–656

ualerp, 657

timer, 605

user/application generated, 605

sigpause, 636

sigpending, 634

sigqueue, 643

sigrelse, 636

sigset, 636

sigsetjmp, 650–651

sigsuspend, 628–634

sigtimedwait, 643–646

sigwait, 624–628

sigwaitinfo, 643–646

simple commands, shells, 376

sleep, 653–657

SMI (Simple Messaging Interface), 405

- client example, 420
- functions, 415–418
- implementation
    - FIFO and, 420–428
    - sockets and, 563–566
- introduction, 414
- POSIX shared memory implementation, 508–515
- POSIX message-queue implementation, 451–456
- server example, 419–420
- System V Message-Queue implementation, 438–442
- types, 415–418

socket, 524–525

socketpair, 595

sockets, 13, 519

- addresses, 523
    - AF_INET6, 538–539
    - AF_UNIX, 534–535
- functions, 700
- structures, 533–534
- clients, multiple, 527–530
- connected, system calls, 524–527
- connectionless, datagrams, 567–568
- FIFOs, 700
- file descriptors, 73
- functions, 699–700
- options, 544–549
- out-of-band data, 577
- overview, 520–524
- SMI implementation, 563–566

special files, 4–5

- block special files, 4–5
- character special files, 4
- disk special files, I/O on, 123–127

SSI (Simple Socket Interface)

- function calls, 550–551
- HTTP and, 551–552
- implementation, 559–563
- introduction, 549
- Web browser, 552–554
- Web server, 554–558

ssi_close, 550

ssi_close_fd, 551

ssi_get_server_fd, 551

ssi_open, 550

ssi_wait_server, 550

standard file descriptors, 73

standard interfaces, library function calls and, 22

stat, 147–154

statvfs, 131–135

STREAMS I/O, 255

strftime, 59

struct dirent, 161–162

struct iovecs, 111

struct timespec, 64

struct timeval, 58

struct tm, 58

struct tms, 64

super user, 11

supplementary group-ID, 10

symbolic links, 2–4, 3–4, 137–138

- creating, 141–144
- metadata and, 147–154
- symbols, 141–144

sync, 115–117

synchronization, threads, 333–338

synchronized I/O

- definition, 189–190
- open flags and, 117–119
- versus synchronous, 114

synchronized writes, 94

synchronous I/O

- asynchronous I/O comparison, 196–198
- defined, 189–190
- versus synchronized, 114

synthetically generated signals, 621–623

sysconf, 51–52

system calls, 19, 661. *See also* functions

- accept, 526
- access, 185–186
- bind, 525
- buffer-flushing, 115–117
- C bindings, 20–21
- C++ bindings, 20–21
- chdir, 166–168
- chmod, 182
- chown, 182–184
- chroot, 319–320
- close, 97–98
- closedir, 160–162
- confstr, 53
- connect, 526–527, 576
- connect sockets and, 524–527
- creat, 77–80
- ctty, 248
- dup, 371–375
- dup2, 371–375
- exec, 284–292
    - exec1, 285
    - exec1e, 289
    - exec1p, 288
    - execvp, 288
    - execve, 289
    - execvp, 288
- exit, 301–304
- fchdir, 166–168
- fchmod, 182
- fchown, 182–184
- fcntl, 187–189
- fdatasync, 116–117
- fork, 284, 296–300
- fpathconf, 52
- fstat, 147–154
- fstatvfs, 131–135
- ftok, 429–431
- ftruncate, 119–120
- getaddinfo, 540–543
- getcwd, 145–147, 170–174
- getgroupld, 154–155
- gethsoame, 543–544
- getlogin, 154–155
- getpeername, 594
- getpgid, 228–229
- getpwd, 154–155
- getrlimit, 323
- getrusage, 328
- gettid, 227
- getsockopt, 594
- getsockopt, 545–549
- gettimer, 658
- group IDs, 315–316
- interrupted, signals and, 607–608
- ioctl, 232–233
- isatty, 249
- lchown, 182–184
- links, 138–139
- listen, 525
- lockf, 483–485
- look, 105–108
- lstat, 147–154
- mkdir, 168–170
- mkfif0, 407
- mknod, 186–187
- mount, 135–136
- mq_close, 447
- mq_getatr, 450
- mq_notify, 450
- mq_open, 446
- mq_receive, 448
- mq_send, 448
- mq_setatr, 451
- mq_timedreceive, 449
- mq_timedsend, 449
- mq_unlink, 447
- magctl, 445
- magget, 434
- magcrv, 436
- magsend, 436
- nanoSleep, 657
- nice, 320–321
- open, 76–77
- opendir, 160–162
- pathconf, 52
- pipe, 362–363
- poll, 218–221
- POSIX message queues, 445–451
- POSIX shared memory, 505–507
- pread, 108–110
- priority setting/getting, 320–321
- process groups, 228–229
- process IDs, 319
- pthread_cancel, 344–345
- pthread_cleanup_pop, 347–348
- pthread_cleanup_push, 347–348
- pthread_cond_signal, 341–344
- pthread_cond_wait, 341–344
- pthread_create, 331
- pthread_join, 332–333
- pthread_mutex_lock, 334–338
- pthread_mutex_unlock, 334–338
- pthread_testcancel, 345–347
- pwrite, 108–110
- read, 96–97
- readdir, 161–162
- readv, 110–113
- recvfrom, 568–574
- recvmsg, 574–576
- rename, 139–141
- rewinddir, 161–162
- rmkdir, 168–170
- seekdir, 161–162
- select, 213–218, 528
- semctl, 461
- semget, 460
- semmsg, 574–576
- sendto, 568–574
- sessions, 227–228, 230–232
- setgid, 318
- setuid, 318
- setgid, 318
- setpgid, 228–229
- setrlimit, 323
- setuid, 227
- setsockopt, 544–545
- settimer, 658
- setuid, 318
- shm.at, 490
- shmctl, 489
- shmdt, 490
- shmat, 489
- shm_open, 505
- shm_unlink, 505
- shutdown, 595
- sigaction, 611–615
- sigattack, 634
- sighold, 636
- sigignore, 636
- siglongjmp, 650–651
- sig1, 635–636
- sigpause, 636
- sigpending, 634
- sigsqueue, 643
- sigrelse, 636
- sigset, 636
- sigsetjmp, 650–651
- sigsuspend, 628–634
- sigtimedwait, 643–646
- sigwait, 624–628
- sigwaitinfo, 643–646
- sleep, 653–656
- socket, 524–525
- socketpair, 395
- stat, 147–154
- statvfs, 131–135
- symlink, 141–144
- sync, 115–117
- sysconf, 51–52
- System V message queues, 434–437
- System V semaphores, 460–463
- System V shared memory, 489–492
- tdrain, 245–247
- tcflow, 246
- tcflush, 246
- togtppgrp, 229–230
- tgetsid, 229–230
- tosendbreak, 247
- tosetpgrp, 229–230
- telldir, 161–162
- terminal control, 229–230, 245–247
- terminal identification, 248–250
- truncates, 119–120
- ttyname, 248
- ttyname_r, 248
- umask, 86
- umount, 135–136
- union semvar, 461
- unlink, 86–87
- user IDs, 315–316
- ualerp, 657
- utime, 184–185
- vfork, 299
- wait, 304–313
- waitid, 304–313
- waitpid, 304–313
- write, 92–96
- writev, 110–113

system data, 5, 6

System V

- `IPC`, 428 (*See also* **IPC**
    - [*interprocess communication*]
        - identifiers, 429–431
        - objects, 428–429
        - ownerships, 431–432
        - permissions, 431–432
        - utilities, 432–433
- message queues
    - disadvantages/advantages, 442
    - limits, 437–438
    - SMI implementation, 438–442
    - system calls, 434–437
- performance comparisons, 515–517
- semaphores
    - POSIX comparison, 476
    - system calls, 460–463
- shared memory
    - advantages/disadvantages, 504
    - SMI implementation, 496–504
    - system calls, 489–492

T

tabs, terminals, 237

`tcflow`, 246

`tcflush`, 246

`tcgetattr`, 233

`tcsetattr`, 233

`tcgetpgrp`, 229–230

`tcsetpgrp`, 229–230

`tcsendbrk`, 247

`tcsetattr`, 233

`tsendbrk`, 247

`telldir`, 161–162

temporary files, creating, 88–90

terminal functions, 700

terminal I/O

- canonical, 239–242
- introduction, 203
- `poll`, 218–221
- `punctual`, 239–242
- raw terminal I/O, 242–245

reading from terminal

- `glin`, 206
- nonblocking input, 208–213
- `select`, 213–218
- testing input, 221–224

terminal (Py) functions, 700

terminals

- attributes
    - `tcgetattr`, 233
    - `tcsetattr`, 233
- breaks, 247
- character mapping, 236–237
- characters, 234–235
- control characters, 238–239
- controlling terminal, 8
- delays, 237
- echo on/off, 239
- flow control, 237
- flushing, 246
- I/O flow control, 246
- padding, 248
- pseudo terminals, 256–257
- reading from, terminal I/O and, 204–224
- speed, 235–236
- system calls, 229–230
- tabs, 237
- testing for, 249

termination

- processes, 301–304
- threads, waiting for, 332–333

terminos structure, 233–234

testing, input, terminal I/O, 221–224

text, object files, 5

text files, 5

Thompson, Ken, 16

thread functions, 701

threads, 6

- blocking and, 350–351
- canceling, 344–348
- creating, 329–331
- library functions and, 22
- processes comparison, 348–349
- synchronization, 333–338
- termination, waiting for, 332–333
- variables, condition variables, 338–344

time, See data time

`time`, 58

time functions, 701–702

timers, functions, 702
