
# Using telnet and ftp

```
*************************************************
* The Book Store                               *
* 273,481 Titles                               *
************************************************
```

```
<A>author Search <R>view Your Selections
<T>itle Search <O>rder (when done)
<K>eyword Title Search <C>heck Order Status
<I>SBN Search
<S>ub Search \ Just Published
```

```
*************************************************
<P>previous Menu <H>elp <G>oodbyye
```

Command: T

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_511_0.png)

SEARCH DATABASE BY TITLE

Enter the first word(s) of the TITLE.
Omit leading "A", "AN", "THE". The first few letters are enough. 
Only the first 20 characters will be used.

<ENTER> Previous Menu, <?> Help, <ENTER>:: tale of two cities

| # | AUTHOR | PUB/BINDING/BK MARKS/PRICE |
|---|---|---|
| 1 | Tale of Two Cities | Dickens, Charles | 07/90 Paperback S/O $ 7.95 |
| 2 | Tale of Two Cities | Dickens, Charles/Woodcock, George | 06/85 Paperback S/O $ 4.95 |
| 3 | Tale of Two Cities | Dickens, Charles | 05/90 Paperback 12 $ 4.99 |
| 4 | Tale of Two Cities | Dickens, Charles | 08/91 Paperback 6 $ 2.95 |
| 5 | Tale of Two Cities | Dickens, Charles | 12/92 Paperback 12 $ 4.99 |
| 6 | Tale of Two Cities | Dickens, Charles | 09/89 Paperback 6 $ 2.50 |
| 7 | Tale of Two Cities (Longman Classics, Stage 2) | Dickens, Charles | 05/91 Paperback S/O $ 7.25 |
| 8 | A Tale of Two Cities (World Classics) | Dickens, Charles | 11/88 Paperback S/O $ 4.95 |
| 9 | A Tale of Two Cities (Courage Classics) | Dickens, Charles | 03/92 Hardcover S/O $ 5.95 |

<Forward, <B>backward, <P>previous Menu, <1-9> View Book # : 7

YOU HAVE SELECTED THE FOLLOWING TITLE:
Author : Dickens, Charles
Title : Tale of Two Cities (Longman Classics, Stage 2)

| ISBN : 0582030471 |
|---|---|
| Volume : |
| Subject # : General Fiction |
| Dewey # : |
| Publisher : Addison Wesley (Longman) |
| Date Pub : 05/91 |
| Binding : Paperback |
| Edition : |
| Bookmarks: S/O |
| Price : $ 7.25 |

How many copies would you like?, <ENTER> To Exit :

Again, decide not to buy, and back out using the P (previous menu) option until I can use G to say goodbye. These are but hundreds of commercials available on the Internet. One of the best places to learn about the entire range of services available is to read Scott Yanoff's List of Internet Services, available from anonymous FTP at csd4.csd.uwmw.edu/. If you're using fget, enter fget csd4.csd.uwmw.edu/~pub/inet/services.txt.

This wraps the tour of Internet navigational packages and Usenet. In these last two hours, you have learned about archie and gopher, and you have traveled to library computers in Australia and Venezuela, and even watched over my shoulder as I almost ordered a John Coltran CD and a recent edition of A Tale of Two Cities. And there's the wonderful world of the Usenet!

The Internet is an amazing resource, and it's growing each day. By the time you read this, the size of the WAIS database list, the number of archive files in that database, and the number of Usenet newsgroups have expanded further. If there's an Information Highway in your future, the Internet is most certainly going to be a key part of it, and you can't go wrong by spending time learning about it!

![](imgimg/f32f6f53c129de2ebafcd2b4ff01b1c9_512_0.png)

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

**anonymous FTP** A system set up to respond to ftp queries that does not require you to have an account on the system.

**bookmark** A saved gopher menu item through which you can easily build your own custom gopher information screens.

**Request for Comment** An official UNIX design specification, also known as an RFC.

**search string** The pattern specified in a search.

# Questions

- 1. Use telnet and login to log in to one of the sites shown in Table 23.3. You don't have an account, drop the connection once you see a login: prompt.
- 2. Use ftp to connect to ftp.eff.org and see what files the Electronic Frontier Foundation has made available to anonymous FTP users. Copy one onto your system, and read through it to see what you think about the organization itself.
- 3. Using archie, find one or two archive sites that have a copy of the tin newsreading program.

# Preview of the Next Hour

This completes your tour of the Internet. In your final hour, you are introduced to the basics of C, the primary programming language for UNIX.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_513_0.png)

# Hour 24
Programming in C for UNIX

This hour introduces you to the basics of the C programming language. C is the most commonly used language for programming UNIX systems. Other common languages are C++ and Perl, but C is the oldest, and many concepts are derived from there. This chapter introduces a lot of concepts. I assume that you have some math and programming skills, but even if you don't, I encourage you to skim through the material to learn about some of the foundations of the UNIX system and how programmers can extend it in many different directions. With any luck, you'll have your interest piqued and decide to learn how to get the computer to jump through hoops for you by writing your own programs.

# Goals for This Hour

In this hour, you learn to write your first program and about the following:

- Basic data types and operators
- Expressions

# Task 24.1: Your First Program

Conditional statements
Looping statements
Functions
Arrays
Pointers
Structures

First, you learn a simple program and how to make it run. After that, you learn the different data types and how to manipulate the data. Control flow follows, where you learn how to make your program execute alternate statements. You'll wind up with some of the more advanced topics in C programming.

Historically, the first program is called the “Hello, World” program because it simply outputs that sentence. However, with the recent discovery of life on meteoroids from Mars, and the suspicion that the oceans of Europa may also support life, we should instead be greeting the universe.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_515_0.png)

The first program is actually very simple:

```
#include <stdio.h>

main(){
    printf("Hello, universe!\n");
}
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_515_1.png)

The file being included, std.h, is a header file that defines the standard input and output functions. The .h is a naming convention indicating that the file is a header and is meant to be used with the #include statements. Other names used in C are for the source file and .o for an intermediate object file.

The main is the program header. Every program, no matter big or small, must have a main included. This must be followed by a curly brace, {, and any number of statements, followed by a closing curly brace. This is the actual program. In our example, the main has two parentheses following. C treats main as a normal function (described later). You can pass arguments to main from a command line.

The statement is printf("Hello\n"); This calls the printf function, which takes a string, possibly with some arguments, and places the contents of the string on the output. Within the string, there is a pair of characters that you may not understand, \n. The backslash is a C convention indicating that a special character follows. Table 24.1 lists the special

| A compiler is a special program found on any development system. It reads in your program (source code), checks to make certain that it is correct, and creates an executable program. |

Table 24.1. Special C characters.

This is a very simple program. Once you've written it, you need to save it to a file. Let's call that file hello.c. Once the file is saved, you can use the cc command to build the program.

```
% cc hello.c
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_516_0.png)
