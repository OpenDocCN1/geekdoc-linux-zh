
- Using Syntax Checking ........................................... 328
- Why Syntax Checking Is Important ................................ 329
- Using Verbose Mode ............................................... 331
- Shell Tracing .................................................... 332
- Finding Syntax Bugs Using Shell Tracing .......................... 333
- Finding Logical Bugs Using Shell Tracing ......................... 335
- Using Debugging Hooks ............................................ 337
- Summary .......................................................... 339
- Questions......................................................... 339
- Terms............................................................. 340
- Hour 21 Problem Solving with Functions ........................... 341
- Library Basics ................................................... 341
- What Is a Library? ............................................... 342
- Using a Library .................................................. 342
- Creating a Library ............................................... 343
- Naming the Library ............................................... 343
- Naming the Functions ............................................. 344
- Displaying Error and Warning Messages ............................ 344
- Asking Questions ................................................. 345
- Checking Disk Space .............................................. 351
- Obtaining a Process ID by its Process Name ....................... 354
- Getting a User's Numeric User ID ............................... 355
- Summary .......................................................... 356
- Questions......................................................... 356
- Terms............................................................. 357
- Hour 22 Problem Solving with Shell Scripts ....................... 359
- Startup Scripts .................................................. 360
- System Startup ................................................... 360
- Developing an Init Script ....................................... 364
- Maintaining an Address Book ..................................... 373
- Showing People ................................................... 375
- Adding a Person .................................................. 377
- Deleting a Person ................................................ 380
- Summary .......................................................... 385
- Questions......................................................... 385
- Terms............................................................. 387
- Hour 23 Scripting for Portability ............................... 389
- Determining UNIX Versions ....................................... 390
- BSD .............................................................. 390
- System V ......................................................... 390
- Linux ............................................................ 391
- Using uname to Determine the UNIX Version ....................... 392
- Determining the UNIX Version Using a Function ................... 394

## Hour 24 Shell Programming FAQs 403
Techniques for Increasing Portability ................ 396
Conditional Execution ................ 396
Abstraction ................ 397
Summary ................ 400
Question ................ 401
Terms ................ 401
Shell and Command Questions ................ 404
Variable and Argument Questions ................ 409
File and Directory Questions ................ 412
Summary ................ 416

## PART IV Appendixes 417

## APPENDIX A Command Quick Reference 419
Reserved Words and Built-in Shell Commands ................ 420
Conditional Expressions ................ 423
File Tests ................ 423
String Tests ................ 424
Integer Comparisons ................ 424
Compound Expressions ................ 424
Arithmetic Expressions (ksh, bash, and zsh Only) ................ 424
Integer Expression Operators ................ 425
Parameters and Variables ................ 426
User-Defined Variables ................ 426
Special Variables ................ 427
Shell Variables ................ 428
Input/Output ................ 428
Input and Output Redirection ................ 429
Here Document ................ 429
Pattern Matching and Regular Expressions ................ 430
Filename Expansion and Pattern Matching ................ 430
Limited Regular Expression Wildcards ................ 430
Extended Regular Expression Wildcards ................ 430

## APPENDIX B Glossary 433

## APPENDIX C Answers to Questions 441

## APPENDIX D Shell Function Library 461

## Index 465

## About the Author
SRIRANGA VEERARAGHAVAN is a material scientist by training and a software engineer by trade. He has several years of software development experience in C, Java, Perl, and Bourne Shell and has contributed to several books, including Solaris 8: Complete Reference, UNIX Unleashed and Special Edition Using UNIX. Sriranga graduated from the University of California at Berkeley in 1997 and is presently pursuing further studies. He is currently employed in the Server Appliance group at Sun Microsystems, Inc. Before joining Sun, Sriranga was employed at Cisco Systems, Inc. Among other interests, Sriranga enjoys mountain biking, classical music, and playing Marathon with his brother Srivaths. Sriranga can be reached via e-mail at ranga@soda.berkeley.edu.

## Dedication
*For my grandmother, who taught me to love the English language.*

*For my mother, who taught me to love programming languages.*

## Acknowledgments
Writing a book on shell programming is a daunting task, due to the myriad UNIX versions and shell versions that are available. Thanks to the hard work of my development editor Steve Rowe, my technical editor Michael Watson, and my copy editor Kezia Endsley, I was able to make sure the book covered the material completely and correctly. Their suggestions and comments have helped enormously.

In addition to the technical side of the book, the task of coordinating and managing the publishing process is a difficult one. The assistance of my acquisitions editor, Kathryn Purdam, in handling all of the editorial issues and patiently working with me to keep this book on schedule was invaluable.

Working on a book takes a lot of time and makes it difficult to concentrate on work and family activities. Thanks to the support of my manager, Larry Coryell, my parents, my brother Srivathsa, and my uncle and aunt Srinivasa and Suma, I was able to balance work, family, and authoring.

Thanks to everyone else on the excellent team at Sams who worked on this book. Without their support, this book would not exist.

## Tell Us What You Think!
As the reader of this book, you are our most important critic and commentator. We value your opinion and want to know what we're doing right, what we could do better, what areas you'd like to see us publish in, and any other words of wisdom you're willing to pass our way.

You can email or write me directly to let me know what you did or didn't like about this book—as well as what we can do to make our books stronger.

*Please note that I cannot help you with technical problems related to the topic of this book, and that due to the high volume of mail I receive, I might not be able to reply to every message.*

When you write, please be sure to include this book's title and author as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

Email: opensource@samspublishing.com

Mail:
Mark Taber
Sams Publishing
800 East 90th Street
Indianapolis, IN 46240 USA

## Introduction
In recent years, the UNIX operating system has seen a huge boost in its popularity, especially with the emergence of Linux. For programmers and users of UNIX, this comes as no surprise: UNIX was designed to provide an environment that's powerful yet easy to use.

One of the main strengths of UNIX is that it comes with a large collection of standard programs. These programs perform a wide variety of tasks from listing your files to reading e-mail. Unlike other operating systems, one of the key features of UNIX is that these programs can be combined to perform complicated tasks and solve your problems.

One of the most powerful standard programs available in UNIX is the shell. The shell is a program that provides a consistent and easy-to-use environment for executing programs in UNIX. If you have ever used a UNIX system, you have interacted with the shell.

The main responsibility of the shell is to read the commands you type and then ask the UNIX kernel to perform these commands. In addition to this, the shell provides several sophisticated programming constructs that enable you to make decisions, repeatedly execute commands, create functions, and store values in variables.

This book concentrates on the standard UNIX shell called the Bourne shell. When Dennis Ritchie and Ken Thompson were developing much of UNIX in the early 1970s, they used a very simple shell. The first real shell, written by Stephen Bourne, appeared in the mid 1970s. The original Bourne shell has changed slightly over the years; some features were added and others were removed, but its syntax and its resulting power have remained the same.

The most attractive feature of the shell is that it enables you to create scripts. Scripts are files that contain a list of commands you want to run. Because every script is contained in a file and every file has a name, scripts enable you to combine existing programs to create completely new programs that solve your problems. This book teaches you how to create, execute, modify, and debug shell scripts quickly and easily. After you get used to writing scripts, you will find yourself solving more and more problems with them.

## How This Book Is Organized
This book assumes that you have some familiarity with UNIX and know how to log in, create, and edit files, as well as how to work with files and directories to a limited extent. If you haven't used UNIX in a while or you aren't familiar with one of these topics, don't worry: the first part of this book reviews this material thoroughly.
