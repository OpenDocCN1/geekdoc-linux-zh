
printer (named printer) and a PDF virtual printer (named PDF), we could check their status like this:

```
[me@linuxbox ~]$ lpstat -a
PDF accepting requests since Mon 05 Dec 2011 03:05:59 PM EST
printer accepting requests since Tue 21 Feb 2012 08:43:22 AM EST
```

Further, we could determine a more detailed description of the print system configuration this way:

```
[me@linuxbox ~]$ lpstat -s
system default destination: printer
device for PDF: cups-pdf:
device for printer: ipp://print-server:631/printers/printer
```

In this example, we see that printer is the system's default printer and that it is a network printer using Internet Printing Protocol (ipp://) attached to a system named print-server.
The commonly used options are described in Table 22-5.

## Table 22-5: Common lpstat Options

| Option | Description |
|---|---|
| -a [printer...] | Display the state of the printer queue for printer. Note that this is the status of the printer queue's ability to accept jobs, not the status of the physical printers. If no printers are specified, all print queues are shown. |
| -d | Display the name of the system's default printer. |
| -p [printer...] | Display the status of the specified printer. If no printers are specified, all printers are shown. |
| -r | Display the status of the print server. |
| -s | Display a status summary. |
| -t | Display a complete status report. |

## lpq—Display Printer Queue Status

To see the status of a printer queue, the lpq program is used. This allows us to view the status of the queue and the print jobs it contains. Here is an example of an empty queue for a system default printer named printer:

```
[me@linuxbox ~]$ lpq
printer is ready
no entries
```

If we do not specify a printer (using the -P option), the system's default printer is shown. If we send a job to the printer and then look at the queue, we will see it listed:

```
[me@linuxbox ~]$ ls *.txt | pr -3 | lp
request id is printer-603 (1 file(s))
[me@linuxbox ~]$ lpq
printer is ready and printing
Rank    Owner   Job     File(s)                  Total Size
active  me      603     (stdin)                  1024 bytes
```

## lprm and cancel—Cancel Print Jobs

CUPS supplies two programs used to terminate print jobs and remove them from the print queue. One is Berkeley style (`lprm`), and the other is System V (`cancel`). They differ slightly in the options they support but do basically the same thing. Using our print job above as an example, we could stop the job in this way:

```
[me@linuxbox ~]$ cancel 603
[me@linuxbox ~]$ lpq
printer is ready
no entries
```

Each command has options for removing all the jobs belonging to a particular user, particular printer, and multiple job numbers. Their respective man pages have all the details.

## 23

## COMPILING PROGRAMS

In this chapter, we will look at how to build programs by compiling source code. The availability of source code is the essential freedom that makes Linux possible. The entire ecosystem of Linux development relies on free exchange between developers. For many desktop users, compiling is a lost art. It used to be quite common, but today, distribution providers maintain huge repositories of precompiled binaries, ready to download and use. At the time of this writing, the Debian repository (one of the largest of any of the distributions) contains almost 23,000 packages. So why compile software? There are two reasons:

- Availability. Despite the number of precompiled programs in distribution repositories, some distributions may not include all the desired applications. In this case, the only way to get the desired program is to compile it from source.
- Timeliness. While some distributions specialize in cutting-edge versions of programs, many do not. This means that in order to have the very latest version of a program, compiling is necessary.

Compiling software from source code can become very complex and technical, well beyond the reach of many users. However, many compiling tasks are quite easy and involve only a few steps. It all depends on the package. We will look at a very simple case in order to provide an overview of the process and as a starting point for those who wish to undertake further study.

We will introduce one new command:

- make—Utility to maintain programs.

## What Is Compiling?

Simply put, compiling is the process of translating source code (the human-readable description of a program written by a programmer) into the native language of the computer's processor.

The computer's processor (or CPU) works at a very elemental level, executing programs in what is called machine language. This is a numeric code that describes very small operations, such as "add this byte," "point to this location in memory," or "copy this byte." Each of these instructions is expressed in binary (ones and zeros). The earliest computer programs were written using this numeric code, which may explain why programmers who wrote it were said to smoke a lot, drink gallons of coffee, and wear thick glasses.

This problem was overcome by the advent of assembly language, which replaced the numeric codes with (slightly) easier to use character mnemonics such as CP Y (for copy) and MOV (for move). Programs written in assembly language are processed into machine language by a program called an assembler. Assembly language is still used today for certain specialized programming tasks, such as device drivers and embedded systems.

We next come to what are called high-level programming languages. They are called this because they allow the programmer to be less concerned with the details of what the processor is doing and more with solving the problem at hand. The early ones (developed during the 1950s) included FORTRAN (designed for scientific and technical tasks) and COBOL (designed for business applications). Both are still in limited use today.

While there are many popular programming languages, two predominate. Most programs written for modern systems are written in either C or C++. In the examples to follow, we will be compiling a C program.
