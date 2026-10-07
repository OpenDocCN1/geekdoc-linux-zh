
# v4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

Instead of repeating the command with -s8, -s24 and -s40, we simply create a loop with $offset and provide the values 8, 24, and 40 in the loop. This gives us the resulting values:

- Last Login Date : Sun Apr 30 21:23:09 2017
- Password Set/Reset Date : Thu Apr 6 01:35:34 2017
- Last Failed Login : Sun Apr 30 21:23:01 2017

Examining Windows registry files in a command line environment may not be the simple efficient method, but it is a great way to learn how registry is parsed, and where information is located.

# Application Analysis - prefetch

Understanding the caveats we provided earlier on the status of many of the libyal projects, be sure to browse some of them and try them out. Documentation can be sparse in places, but that's where experimentation and testing comes in. In many cases, the libraries are provided to add capabilities to other programs – the provided utilities may simply export information from an artifact to XML or text format straight to standard output. This is an example of this and is used to access Windows prefetch files.

Prefetch can be a useful forensic artifact for any number of reasons. They can provide additional execution times for timelines, they can be used to prove program execution even when an executable has been deleted, and they can be used to correlate other artifacts created during execution. More information can be found on the Internet³³⁵.

Let’s have a look at a quick example, after installing libcca:

```
barry@forensic1:~# su -
Password:
root@forensic1:~# apt install libcca
libcca (libYAL Windows Prefetch File parser)
libcca is a library to access the Windows Prefetch File (SCCA) format.
Proceed with libccsa? [y]
...
Cleaning for libcca-20170105...
root@forensic1:~# exit
```

> ³³⁵http://www.forensicswiki.org/wiki/Prefetch is a good standard.

With libssca installed, let's look for a prefetch file to view. We'll search the NTFS image for files ending in .pf. You can see there are quite a few of them (output is truncated).

```
barry@forensic1:-$ fls -o 2048 NTFS_Pract_2017/NTFS_Pract_2017.E01 |
grep .pf*$
r/r 72-128-2:
Windows/Prefetch/58.0.3029.81_CHROME_INSTALLER-F0A66AC.exe
r/r 73-128-2:
Windows/Prefetch/AUDIODG.EXE-BFD3029.pf

r/r 123-128-2:
Windows/Prefetch/NMAP.EXE-69B77167.pf
...
r/r 135-128-2:
Windows/Prefetch/SEARCHFILTERHOST.EXE-77482212.pf
```

Our familiar fls command is executed, looking for files only, recursively (-Fr) in the file system at offset 2048 (- 2048) in our NTFS EWF files. Using **grep**, we are looking for .pf at the end of the line (signed by the $). The list is long, but we'll look at NMAP.EXE prefetch file (MFT entry 123-128-2). We can extract the file from the image with **icat**:

```
barry@forensic1:-$ icat -o 2048 NTFS_Pract_2017/NTFS_Pract_2017.E01 123 >
nmap.pf.123
```

Let's verify quite look at the header of the file with xxd. You can see why with the library we just installed libssca. The prefetch header is 84 bytes with the version at offset 0x00 and the SCCA header at offset 0x04.

```
barry@forensic1:-$ xxd -l 84 nmap.pf.123
00000000: 1700 0000 5343 4341 1100 0000 aaaa 0000      SCCA...
00000010: 4e00 0204 4100 5000 2e00 4500 4800      N.M.A.P..E.E..X.E.
00000020: 0e00 0200 0000 0d35 a3b2 071b 719d      ......5.{q.
00000030: bb36 0382 0100 483d 4087 1100 0000      ......6......H=..).......gq.i
00000040: 0000 0000 0000
```

Some of the features we can find (be careful of byte order):

- prefetch version = 0x617 (Windows 7)
- SCCA header = 0x5343 0x41 (SCCA)
- executable name = 0x4e 0x4d 0x50 0x45 0x58 0x58 (NMAP.EXE)
- prefetch hash = 0x69b771167 (matches the hash in .pf filename)

The last execution time can be found at offset 8 in the prefetch file (8 bytes long), and we can use WinTime again to decipher it: http://www.forensicswiki.org/wiki/Prefetch File Format

Given enough information about the format, you could spend a lot of time parsing the file. There's other information stored within, including libraries and other files accessed when the executable is started. But from here we'll use libssca to view the prefetch contents, which is quite extensive.

```
barry@forensic1:-$ python WinTime.py `xxd -s 8 -l 8 nmap.pf`
Thu Apr 6 15:07 2017
```
barry@forensic1:-$ libssca nmap.pf.123 20170105

- Windows Prefetch File (PF) information:
- Format version : 23
- Prefetch hash : 0x69b77167
- Executable filename : NMAP.EXE
- Run count : 9
- Last run time : Apr 6 15:07 2017
- Filenames:
- Number of filenames : 53
- Filename: 1 : \DEVICE\HARDDISKVOLUME2\SYSTEM32\NTDLL.DLL
- Filename: 2 : \DEVICE\HARDDISKVOLUME2\SYSTEM32\KERNEL32.DLL
- Filename: 3 : \DEVICE\HARDDISKVOLUME2\USERS\DOWNLOADS\NMAP-OS-DB
- Volumes:
- Number of volumes : 1
- Volume: 1:
- Device path : \DEVICE\HARDDISKVOLUME2
- Creation time : Apr 6 04:48:55 2017
- Serial number : 0x501905c

There are numerous utilities available to Linux users that can be found to assist in parsing files, artifacts and other data recovered from computers running systems other than Linux. There are, in fact, too many to list here. Sometimes it's simply a matter of finding a comparable open source project: like using LibreOffice to view Microsoft Office or Visio files. There are also the simple utilities that are either pre-installed or easily installed on your Linux distribution, like catdoc or tools like pdfinfo and exiftool for reading file metadata.

# Integrating Linux with Your Work

This guide covers a myriad of subjects that really just touch the surface of the command line capabilities of Linux as a forensic platform. And while it is a lengthy guide, it still implies a basic set of commands and utilities to allow you to learn and grow as a forensic examiner or digital investigator. The real power of Linux (as an heir of UNIX itself) is in thinking UNIX. The more you use commands and get used to the output they produce, the more you will learn to string them together, solving increasingly complex issues quickly and efficiently. Getting a solid grasp of command line pipes and redirection is a liberating process.

Some of the repeated exercises we've done here were designed to kick start the repetition to anchor the command line into memory. It is not, however, realistic to expect that everyone will suddenly convert to Linux and forget other operating systems for forensic analysis. Linux is, at the end of the day, just another platform and tool set. I maintain that there is some value in every examiner to be familiar with the tools it provides. We've talked about how the command line tools we've encountered (and there are *many*) are unique compared to common Windows tools. Much of this difference arises from the fact that they are generally designed with the UNIX approach of "do one thing and do it well". We see this in tools like grep, head, tail, tr, sed and utilities like icat, blkls and catdoc. They provide discrete output when they run on their output, but as you start piping them, you end accomplishing multiple steps in the same command line. This becomes very powerful not only when you learn what each tool is capable of, but when you also start to think in terms of a modular command line. Learning and remembering all this, means less of a burden on examiner resources. And so, one of the strengths of Linux is also, in fact, one of its weaknesses when it comes to mass appeal in the forensic community.

So do we continue to use Linux, maintain what we've learned and continue learning, while remaining efficient? Let's discuss how you can integrate a Linux platform into your lab or examination processes and continue to use it, if not on a daily basis, at least to maintain (and continue growing) the skills we've introduced.

Validation, in this context, can be seen as comparing the output of different tools to test specific software functions (or in some cases, hardware functions) and hopefully determine that the output is *supposed* to give is actually produced. If your lab or organization
