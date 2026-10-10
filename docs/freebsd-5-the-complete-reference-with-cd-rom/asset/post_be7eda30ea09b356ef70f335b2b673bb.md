
## Conventions Used in This Book

This book uses certain conventions to help aid comprehension and break up the page into blocks that can be easy to scan. Conventions include fonts applied to specific words and lines, special text elements applied to paragraphs, and uses of IP addresses and hostnames used in networking examples.

## Text and Font Conventions

Writing about computers presents certain pitfalls. Certain words can be rendered ambiguous by the fact that they may be program names, command names, computer names, and so on. When presenting a text-mode interaction between a human and a computer, it may not be clear what the human types and what the computer displays on the screen. For these reasons, this book uses certain typographical conventions to help clarify matters. These include:

- A normal proportionally spaced font like this one is the default font; normal text appears in this font.
- **Bold text** is used at the start of certain bulleted and numbered lists to summarize information contained in the item.
- *Italic text* denotes a new technical term that’s being described for the first time in the chapter. *Italics* are also used for emphasis.
- `Monospaced text` is used for filenames, computer hostnames, uniform resource locators (URLs), the syntax used by a command, complete or partial configuration file contents, and text displayed by a computer in a text-mode display, such as when running a text-mode program. Program names sometimes appear in this font, when the program is most commonly known by the filename used to launch the program.
- **`Bold monospaced text`** denotes text that a user types, usually at a shell command prompt (described shortly). Sometimes you might type this text when interacting with a non-shell program, though.
- `*Italic monospaced text*` indicates a variable—information that’s likely to vary from one system to another or from one situation to another. For instance, a file might be referred to as *file.txt*, meaning any file or a file with a name that I can’t know.
- **`*Bold italic monospaced text*`** has the same meaning as italic monospaced text, but for something you type into the computer.

When you use FreeBSD in text mode, you do so by running a *shell*, which is a program that accepts your commands. FreeBSD launches the shell automatically when you log in. When I present long commands or extended series of interactions, I place these commands on separate lines from the bulk of the text. In these cases, I present a *shell prompt*—a character that the shell uses to tell you it’s ready to receive input. I use a pound sign (#) as the shell prompt for the administrative account (*root*) and a dollar sign ($) as the shell prompt for ordinary user accounts. Thus, you might see something like this:

```text
$ ifconfig | grep vr0
```

This line indicates that the command can be issued from an ordinary user account. (In most cases, *root* can also issue the same command, but you don’t need to be *root* to issue the *command*.) If the line had begun with a pound sign, it would work properly only from the *root* account. For commands specified in the body of the text, I don’t use this convention because it’s potentially more confusing in that context. For instance, I might write “type `ifconfig` to see information on your network interfaces.”

Some example lines are, in reality, longer than can be presented on a single line in this book. In such cases, the first line in this book ends with a special arrow as a line continuation character, thus:

```text
/usr/src -network 172.17.2 -netmask 255.255.255.0 nova nebula\
blackhole brownwarf
```

If you see this symbol, it means that the text should be considered one line. Many FreeBSD configuration files enable you to use a backslash character (\) as a line continuation character, so in the case of configuration files, you may be able to enter long lines on multiple lines and use a backslash in place of the line continuation character used in this book. This feature isn’t universal, though, so if in doubt it’s best to stick with a long line.

## Special Text Elements

Another set of text conventions highlights information that’s important or unusual in some way. These elements are:

**Note** A *Note* provides information that’s interesting or useful, but somewhat peripheral to the main thrust of the discussion. For instance, a *Note* might point out how a command differs from similar commands in other OSS.

**Tip** A *Tip* describes a practice, procedure, or command that can help save you time or that can achieve a goal in some unusual or non-obvious but desirable way.

## IP Address and Hostname Conventions

If you’re familiar with TCP/IP networking, you may know that certain IP addresses are reserved for private networks—those that aren’t connected to the Internet at large. Specifically, the ranges 10.0.0.0-10.255.255.255, 172.16.0.0-172.31.255.255, and 192.168.0.0-192.168.255.255 are so reserved. In order to avoid accidentally using somebody’s real IP address, I use these ranges in most examples that require real IP addresses, even for systems that, in these examples, would be on the Internet.

If you’ve moved in networking circles for a while, you may know that the Internet standards document known as RFC 1918 describes domains whose names are reserved, much as the private network IP address ranges are reserved. In particular, example.com, example.net, and example.org are all reserved for use in documentation. Although I use these domain names in a few examples, they are—well—boring! Also, many examples require the use of multiple domain names, and these three reserved names are too similar to one another to stand out in most peoples’ minds. Thus, I mix things up by using various domains that are not currently registered and probably never will be, such as luna.edu, panga.ae.edu, and three.or.g.com. My apologies if any of these domains ever comes into use and causes confusion. Some examples require the use of real domains because the examples rely upon those specific domains. In such cases, I use the appropriate domain.

## About the CD-ROM

This book includes with it a CD-ROM of FreeBSD 5.0. FreeBSD is a very large OS, so a single CD-ROM doesn’t contain the entire OS. The CD-ROM included with this book is enough to get you started, though; it includes the core OS and the most important tools and utilities. You can boot the CD-ROM (or create a boot floppy from files on the CD-ROM, as described in Chapter 2) and install FreeBSD using nothing but the CD-ROM included with this book. Because FreeBSD is open source software, you may install it on as many computers as you like.

If you want to install software described in this book that's not on the CD-ROM, you can obtain it from the Internet. The easiest way to do so is to specify installation of the additional packages from an FTP site, as described in Chapter 11. In fact, you can also boot the CD-ROM but install FreeBSD itself from an FTP site, which may enable you to install programs initially that aren't on the included CD-ROM. Network installations of FreeBSD work best when you have a fast network connection; if you have only a 56Kbps dial-up modem, it may take hours to download all the packages you choose to install, so using the CD-ROM and then adding more packages from the Internet will be much faster.

## Contacting Me

If you have comments or questions about the book, feel free to contact me at rogers@rogersbooks.com. I maintain a web page about this book at http://www.rogersbooks.com/freebsd/.

## The Complete Reference

![](img/f34d37e3abe9f4517128e54f80ab2616_38_0.png)

## Part I

FreeBSD Installation

## The Complete Reference

![](img/f34d37e3abe9f4517128e54f80ab2616_40_0.png)

## Chapter 1

## FreeBSD Requirements

This book is your guide to the FreeBSD operating system. Before you embark too far on the FreeBSD journey, though, it’s important that you understand some basics: why you might want to run FreeBSD, how it fits into the software world, and how it fits into the hardware world. This chapter addresses these issues. Understanding them can help you avoid costly mistakes, such as attempting to run FreeBSD on inadequate hardware or attempting to use FreeBSD in an inappropriate environment. If you’re new to FreeBSD, this chapter is vitally important. Even if you’re already familiar with FreeBSD (or some other UNIX variant), this chapter can help you plan your FreeBSD installation. (Chapter 2 continues the description of installation planning and execution.)

### Why Run FreeBSD?

Using the right tool for the job is critically important to any undertaking, and your choice of OS is no exception to this rule. FreeBSD is a very capable and flexible OS, and as such, you can use it in many different ways. Despite this fact, though, FreeBSD isn’t the perfect choice for all situations. For this reason, this book begins with a look at the circumstances in which you may want to run FreeBSD.

As a general rule, FreeBSD is used in one of two ways: as a workstation or as a server. This section describes these roles and covers FreeBSD’s strengths and weaknesses with each. FreeBSD is one of a family of OSs that are derived from or modeled after the UNIX OS. In deciding on an OS to use, it’s therefore important that you understand both how FreeBSD (or UNIX generally) compares to non-UNIX OSs and where FreeBSD fits in the family of UNIX-like OSs. This section therefore covers these relationships.

### FreeBSD as a Workstation OS

In this book, the word *workstation* is used primarily to refer to any computer at which a user sits to perform day-to-day work, such as word processing, programming, graphic design, or web development. (Workstations can also be used for playing games.) Some people like to restrict the word *workstation* to high-powered computers used for these functions, or to systems with permanent network connections. When *workstation* is used in this way, the term *desktop computer* is used to refer to lower-powered or non-networked computers that otherwise resemble workstations. Distinctions based on computer power must constantly change with the technology, though, and networking distinctions can be blurry because of the popularity of dial-up network links on low-end systems. Therefore, this book uses the word *workstation* in reference to computers fulfilling the entire range of end-user functions.
