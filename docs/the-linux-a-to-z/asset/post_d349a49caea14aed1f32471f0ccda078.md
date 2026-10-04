
In order to access the web you will need a web browser. In general, Linux distributions are not supplied with a web browser so you will need to download one if you want to use the world wide web. Currently, the most common web browser is called netscape, versions of which can be found at several of the main Linux archive sites or one of their mirror sites.

Once you have a copy of netscape installed you will need to start up X-windows in order to run it. When you have netscape running, the front page will be displayed, and one of the boxes on the front page is labeled Location:. This box contains the location of the web page you are currently viewing. Web pages are written in a language called hypertext markup language (html). This uses a simple method for marking sections of the document text as headings or ordinary text, or as links to other web pages or links to other places in the current web page.

Every document available on the web has associated with it a link called its uniform resource locator (URL). The URL for a document has the format:

```
http://www.server.hostname/pathname/on/server
```

The URL consists of three sections, as follows:

1. This is the part up to and including the first colon (http: here). This part specifies the communication protocol that will be used to transfer any documents found.
2. This is the part between the double slash (//) and the first single slash (/) characters (www.server.hostname here). It gives the hostname of the machine from which the service is being requested.
3. This part is from the first single slash (/) to the end of the line (which, in this example, is /pathname/on/server). It gives a pathname on the host machine where the required document is to be found.

The big attraction of the web and its browsers is that many different protocols can be used in addition to http such as email, news, ftp, gopher and wais.

When you are reading html documents you will find some words highlighted in the text, by color or by underlining. These highlighted words have hypertext links attached to them and clicking on one of them with the mouse will cause the browser to follow the link and display the contents of the document to which the link points.

Just as with ftp and gopher, the world wide web also has search engines available to help you find the URLs of documents related to particular topics. These include:

| Search Engine | URL |
|---|---|
| yahoo | http://www.yahoo.com/ |
| lycos | http://www.lycos.com/ |
| excite | http://www.excite.com/ |
| altavista | http://altavista.digital.com/ |
| webCrawler | http://webcrawler.com/ |
| inktomi | http://inktomi.berkeley.edu/ |

These systems are quite sophisticated in their search strategies. In general, they take a list of keywords from you and search through their databases looking for documents containing as many of your keywords as possible. The documents retrieved will then be put into order according to some relevance criteria and their titles listed to you a small number at a time, usually with a short extract from the start of the document. The listed titles are made into hypertext links to the documents themselves so that you can click on any titles in which you are interested to retrieve copies of your chosen documents.

In addition to running a world wide web client, if your machine will be attached to the Internet full time, it is also possible to run your own web server under Linux. Once again, most distributions do not include a web server but an archie search for cern-httpd or NCSA-httpd will soon locate a copy of one of these two web servers that you can download with ftp and install. Complete installation and running instructions are included in the same tar file that you download for the server software.

## Running DOS

Despite the best efforts of everyone who has contributed to the Linux development work, there are still one or two of you out there who feel that for one reason or another you cannot get by without access to DOS. Actually, that is quite understandable because there are one or two application packages available for DOS whose functionality has not yet been matched by the free software brigade (not yet...).

Potentially, there are many problems involved in trying to run DOS software in a Linux environment. The majority of these are centered round the fact that DOS is designed to run on 386, and above, processors only by running the CPU in an 8086 backward compatibility mode (called real-mode). Linux on the other hand, whilst it runs on the same processor, switches the CPU into a completely different mode (called protected-mode) where many of the processor's internal registers have different meanings to those that they have in real-mode.

### 13.1 DOSEMU

A package which is available to run under Linux and which will allow you to run a great deal of DOS software from within Linux is called DOSEMU. The name suggests that DOSEMU is a DOS emulator – this is not the case. In fact, DOSEMU just emulates the machine environment in which DOS runs. On top of this environment you actually run a real copy of DOS. Since the various versions of DOS with which DOSEMU will run are proprietary products, the DOSEMU package does not include a version of DOS – this means that you will have to buy and use your own copy.

The way that DOSEMU works is to use the virtual 8086 mode of the 80386 processor to provide a hardware environment in which real-mode software will run, while the processor continues operating in protected-mode. Using this arrangement will allow real-mode software to be run at the same time as the Linux operating system.

![](img/ad36c2db45661d7b3b68db09c8eea0a1_233_0.png)

Figure 13.1 DOSEMU needs to emulate this PC AT memory map.

The DOSEMU software then has the task of providing the functionality of the PCs BIOS, with all of its system calls and entry points. In particular, what this means under Linux is that the DOSEMU library uses Linux facilities to emulate the PCs ROM BIOS including:

- int10 video driver;
- int13 disk driver;
- int14 serial driver;
- int15 I/O subsystem extensions;
- int16 keyboard driver;
- int17 parallel printer driver;
- int1a CMOS real time clock.

If the emulation is sufficiently accurate, then any software (DOS, for instance) will run under the emulator and be unaware that it is not running in the real environment. Similarly, with DOS running, other application programs should be able to run, making use of DOS and emulated BIOS calls. Figure 13.1 shows the memory map that DOSEMU needs to emulate to meet the expectations of DOS and its applications.

### 13.2 Installation

The first thing to remember is that DOSEMU is being modified and upgraded all the time, to add new functionality, take out bugs to improve its reliability and also to keep up with developments and changes in Linux itself. This means that a good idea if you want to install the package is to try to obtain the latest version from the FTP archives.

There are two ways to get hold of the package, one is as a ready-built set of binary, configuration and documentation files, the other is as a set of sources which you need to compile, install and configure yourself. Several Linux distributions arrive with DOSEMU as one of their standard or optional packages, in which case it is usual for the package to be ready-built. This obviously makes the installation of the package a bit easier but may also mean that you won't have the latest version. Assuming now that you have a set of sources to build and install, the procedure runs something like this:

- To start with, even though DOSEMU is only a user level program (i.e. it doesn't run in the kernel) you may still need to build a new kernel in order to get it to run. This is because it uses the shared memory and semaphore inter-process communication (IPC) mechanisms from the System V IPC package. This means that you must build a new kernel with the IPC software configured into it (unless, of course, your existing kernel already has it in). Also make sure that your kernel version number is high enough for the version of DOSEMU you are trying to install.
- Make sure you are logged in as root or you will not be able to complete the installation. Now unpack the software from the archive into a sensible place to build it. This will require about 2Mb of disk space for the sources plus the space that you will use creating all the binaries.
- Building the software, creating the documentation and performing the installation itself couldn't be easier. You just change to the top level directory in which you unpacked the software and type:

```
# make doeverything
```

and, believe me, it does. Or, at least it does if you have the TeX text processing package installed so that make can build the manuals. If you don't have TeX or you don't want to build the manuals, then, instead, you can use the command:

```
# make most
```

You should finish the installation by copying the file that will become your initial DOS C: drive into the appropriate place, as follows:

```
# cp ./hdimage.dist /var/lib/dosemu/hdimage
```

Next you need to configure the package by creating the file:

/etc/dosemu.conf

with appropriate contents. The two ways to do this are either to run the Configure script and answer lots of questions about your machine's configuration, or copy the example configuration file as:
