
## 目录（续）

Message Composition ... 360
Viewing Files and Directories with Gnus ... 362
- Directories and Document Groups ... 362
- Gnus and the World Wide Web ... 363

Gnus as an E-Mail Client ... 365
- Selecting a Mail Back End ... 366
- Mail Sources ... 368
- Splitting Mail ... 368
- Expiring Mail ... 369
- Attachments and MIME ... 370
- Mail without News ... 371

Offline News Reading with the Gnus Agent ... 371
- Setting It Up ... 372
- The Agent and Mail ... 374
- Posting Follow-Ups ... 374
- Further Exploration ... 374

Miscellaneous Gnus Settings ... 375
- Highlighting ... 375
- Asynchronous Fetching ... 375
- Skill Level ... 377

Gnus, XEmacs, and GNU Emacs 21 ... 377
- Conclusion ... 378

Chapter 19: Editing Files on a Remote Machine ... 379
- ftp ... 380
- Requesting a Remote File ... 381
- netrc and Passwords ... 382
- Binary and ASCII Transfers ... 383
- Host Types ... 385
- Hash in the Modeline ... 386
- Sources of Further Information ... 386
- Conclusion ... 387

Chapter 20: Web-Browsing with W3 ... 389
- Installing and Setting up W3 ... 390
- Images, XEmacs, and GNU Emacs ... 391
- Turning off Image Display ... 392
- MIME Support ... 392
- Basic Commands ... 393
- Bookmarks ... 394
- Using Netscape's Bookmark File ... 395
- Stylesheets ... 395
- Security ... 398
    - Using SSL ... 398
    - SSL Variables ... 399
    - Cookies ... 400
- Masquerading ... 402
- Downloading Files ... 402
- Asynchronous Operation ... 403
- Caching Web Sites ... 403
    - Cleaning out the Cache ... 404
    - Caching Only ... 405
- Conclusion ... 405

Chapter 21: Emacs Games ... 407
- Text-Based Games and Hacks ... 408
    - Zippy ... 408
    - Doctor ... 410
    - Dissociated Press ... 411
    - Conw ... 412
    - Blackbox ... 414
    - Towers of Hanoi ... 415
    - Gomoku ... 417
    - Zoning Out ... 418
    - Conway's Game of Life ... 419
    - Xmine ... 420
    - The Gamegrid Games ... 422
        - Tetris ... 422
        - Snake ... 423
        - Sokoban ... 424
        - Pong ... 425
- Conclusion ... 426

Part IV: Dealing with Problems ... 427

Chapter 22: Coping with Emacs Problems ... 429
- Undo ... 430
- The Message Log ... 431
- GNU Emacs: Messages and Lossage ... 431
- XEmacs and Recent Messages ... 432
- Network Problems ... 433
- Automatic File Backup ... 434
- What to Do if You Find a Bug ... 436
- Lisp Package Problems ... 437
- Submitting a Bug Report ... 437
- Bug Reporting Tips ... 438
- Lisp Debugging Tools ... 440
    - The Built-in Debugger ... 440
    - Debugger Mode and the Backtrace Buffer ... 441
    - Debugging Your .emacs File ... 441
    - Lisp Syntax Problems ... 443
- Conclusion ... 444

Chapter 23: Help Resources ... 445
- The Emacs Help System ... 446
    - Apropos ... 447
    - Mode Help ... 450
    - Help with Keybindings ... 451
    - Keystroke Help ... 452
    - Package Help ... 452
    - Lisp Help ... 454
- The Info Help System ... 454
    - Starting Info ... 455
    - Info Navigation ... 456
    - Problems with Info ... 458
    - Adding New Info Directories ... 459
    - The dir File ... 459
- Finding Help on the Net ... 460
    - The Emacs News groups ... 461
    - Useful Web Sites ... 463
- Conclusion ... 464

Part V: Appendixes ... 465

Appendix A: Key Command Reference ... 467
- Essential Commands ... 468
- Movement Commands ... 468
- Windows, Frames, and Buffers ... 469
- Selecting a Region ... 470
- Cut, Copy, and Paste ... 470
- Transposition and Case ... 470
- Searching and Replacing ... 471
- Spelling Correction ... 472
- The Dired File Manager ... 472
- Word Wrapping ... 473
- Keyboard Macros ... 473
- Shell Commands ... 473
- Rectangles and Registers ... 474
- Bookmarks ... 474
- Abbreviations ... 474
- Sending Mail ... 475
- Mouse Commands ... 475
    - Mouse Bindings Shared by GNU Emacs and XEmacs ... 475
    - GNU Emacs-Specific Mouse Usage ... 475
    - XEmacs-Specific Mouse Usage ... 476
- The Help Keys ... 476
- Quitting Emacs ... 477

Appendix B: Minibuffer Commands ... 479
Appendix C: Miscellaneous Mode Commands ... 483
Appendix D: Emacs and Internationalization ... 485
- Setting Up ... 486
- Fonts ... 487
- Input Methods and Language Environments ... 488
- The Mule Project ... 489

Glossary ... 491
Index ... 495

## Introduction

Emacs is one of the few software packages in use today with a history dating back to the early mainframe days. When the early versions of Emacs were being developed (about 16 years ago), they could be used only on expensive proprietary mainframe computers. Today, Emacs is used on just about any machine and operating system you can think of. A worldwide community of thousands of users and developers are continually extending and improving the editor's capabilities.

This is a brief account of how Emacs (and XEmacs) evolved.

### Richard Stallman and the GNU Movement

In the early 1970s, in the days when the only computers were large and inefficient mainframes, the people who used them were an elite group. Confined largely to universities and government research labs, these early computing pioneers shared their work freely. Commercial interests had yet to enter the world of software. Copyrights and patents would arrive eventually, but in those days, most software was written for a specific machine and task.

A certain intellectual camaraderie prevailed at computing hotbeds such as Berkeley and MIT. Richard Stallman was a young MIT programmer excited by the potential of this new world of machine computation.

In those days, text editors were clumsy and difficult to use. There was no real-time display of the file being edited. The user had to type in arcane editing commands, subsequently viewing the pertinent line in the file to see whether the change was achieved. Stallman was using such an editor to write programs under the ITS (*Incompatible Time Sharing*) operating system on Digital PDP-10 machines. This editor, called TECO (*Ta**p**e Ed**i**t**o**r* and Corrector), was powerful for its time; it actually was as much a programming language as an editor. Stallman created a set of macros for TECO that made the editor much easier to use. (A macro in this context is a key sequence that executes a desired routine.) As was the common practice at the time, Stallman shared his enhancement with other programmers at MIT. From there, it began spreading to other computer-science labs.

**A TECO Command**

Here's an example of a TECO command:

```
..: J^PEE8S
J <-.:;; ,( ,S ,D.)EX1 ^P*B $K :L I $ G1 L>$S
```

As you can see, editing a file back then was not a task to be taken lightly!

### TEMACS Evolves into Emacs

Several other people came up with their own packages of TEMACS macros. Stallman incorporated features from several of them into a new editing environment he named Emacs, which stood for “editing macros.”

By 1976, Stallman realized that Emacs really didn't depend on or even have much to do with TEMACS. The concept of a “real-time, extensible, self-documenting editor” (as he described it) could be implemented any number of ways.

In 1978, computer scientist Bernard S. Greenberg worked for Honeywell, just across the street from the MIT computer lab. He was working with another early operating system called Multics. After seeing Stallman's work with Emacs (as a TEMACS enhancement), he decided to develop a Multics version. The difference was his choice of macro language. Greenberg was a proponent of the Lisp language, so he used it as the basis of his Multics version of Emacs.

**What's Lisp?**

Lisp stands for “list processing language”. It is a computer programming language developed in the late '50s at MIT for research in artificial intelligence. An offshoot called Scheme is used as a teaching language in many university computer-science courses.

Guy Steele, also at MIT, synthesized the efforts of those who had created TECO macro sets and came up with the first version of Emacs. Stallman began to work with it and ended up becoming the primary developer.

Emacs history in the late '70s and early '80s isn't well-documented. During this period, the editor became popular with many users around the world, and other developers began helping with the project.
