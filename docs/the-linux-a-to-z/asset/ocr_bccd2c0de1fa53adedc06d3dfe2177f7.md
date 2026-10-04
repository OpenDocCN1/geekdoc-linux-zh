# 2.4 On-line Help

In general, there are many more command line switches available for each command than you have seen so far and certainly more than I have space to include here. If you need to find extra detail about the use and format of anything covered in this book, or any other system facility for that matter, then there is a terrific amount of information available in the form of the on-line manual. Linux has a set of manual pages available that are split into sections. The purpose of the pages in each section is as follows:

+   - **section 1** This part of the manual details the commands that you type in at the keyboard in response to a shell prompt (such as `cat` and `ls`).
- **section 2** When you write programs to be compiled under Linux (in C perhaps), you will often want to call on facilities provided for your programs by the kernel of the operating system. These facilities are accessed via a set of *system calls* and it is these calls that are detailed in this manual section.
- **section 3** In addition to the system calls provided by the operating system, there is also a huge set of programming language function calls collected into libraries and supplied with the compiler. The library function calls are described in manual section 3.
- **section 4** Under Linux, all input and output is made to look as though is goes to or comes from a file. This means that when you are writing a program to read characters from a keyboard or write characters to a screen or printer, you actually open a file which is one of these devices and read or write characters to it. The files which represent the hardware devices of the machine are special files which are stored, by convention, in `/dev`. Any special details about driving the hardware through these files is contained in this manual section.
- **section 5** This section describes the structure and layout of various system data and administrative configuration files (the password file, for example).
- **section 6** This is the manual section which describes the games available on the system.
- **section 7** This is a section for miscellaneous items which don't fit anywhere else.
- **section 8** This is another section of commands to type in at the keyboard, but they are only intended to be used for system administration, and usually only by the system privileged user (called *root*, not to be confused with the directory of the same name).
- **section 9** This section is for descriptions of some of the internal workings of the Linux kernel itself.

A command which allows access to all these manual pages is called man. It is used as follows:

```
$ man ls
```