
Lucky for us, Apache developers and supporters made sure an official place was set up for obtaining Apache software. The official Apache Web site is www.apache.org. This site contains the latest stable version of Apache, the latest release version of Apache, patches, contributed Apache modules, and so on. This is where you want to go for all your Apache needs — although you might be directed to a mirror site that is geographically near you to help cut down on bandwidth and network congestion. You can also use the Pretty Good Privacy (PGP) signatures offered on the site to verify the authenticity of the source code. If you do not know how to use PGP, check out www.pgp.net.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_44_0.png)

Windows users: Please read Chapter 20 for details on your platform. This chapter is primarily geared towards Unix installation and uses Linux as the sample platform. Instructions in this chapter apply to most Unix systems.

## System Requirements

Apache runs on just about any platform in use today, including Linux; FreeBSD; OpenBSD; NetBSD; BSDI; Amiga OS 3.x; Mac OS X; SunOS; Solaris; IRIX; HPUX; Digital Unix; UnixWare; AIX; SCO; ReliantUNIX; DGUX; OpenStep/Mach; DYNIX/ptx; BeOS; and Windows.

### Requirements for building Apache from source distribution

If you are planning on building Apache from source, which is what I highly recommend since compiling your own will give you a very lean and mean server, then you need to make sure that your system meets the requirements stated in Table 2-1.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_44_1.png)

These requirements are for building Apache from the source code only. For running Apache on your system, browse the requirements in the next section.

## Table 2-1 Requirements for Building Apache from Source

| Resource | Required? | Requirements |
| :--- | :--- | :--- |
| Disk Space | Mandatory | Approximately 12 MB of disk space is needed to compile and install Apache from source distribution. However, if you add many modules that are not part of the standard source distribution, then your space requirements will increase. After it is installed, Apache only needs approximately 5 MB of disk space. However, I highly recommend that you maintain the source code on your hard disk until you finish reading this book. |
| ANSI C Compiler | Mandatory | ANSI C compiler is required. For most systems, the GNU C Compiler (GCC) from the Free Software Foundation is highly recommended. The version you should have is 2.7.2 or above. GCC can be found at www.gnu.org. Most Linux systems, such as Red Hat Linux, come with the latest stable version of the GCC compiler. |
| Perl 5 Interpreter | Recommended | You do not need Perl for compiling Apache, but some of the support scripts, such as *apxs*, *split-logfile*, *log_server_status*, and *dbmanage*, which are found in the support subdirectory of your source distribution, are Perl scripts. You need Perl only if you plan to use those scripts. I highly recommend that you install Perl on your system. Perl version 5.003 or above will work fine. |

**Table 2-1 (continued)**

| Resource | Required? | Requirements |
| :--- | :--- | :--- |
| Dynamic Shared Object (DSO) support | Optional | Instead of compiling modules in the Apache binary itself, you can create dynamic modules called DSO that can be loaded via the `httpd.conf` file at startup. DSO modules enable you to experiment with modules and configurations more freely than compiling everything in httpd. Currently, DSO support is available for: Linux, FreeBSD; OpenBSD; NetBSD; BSDI; SunOS; Solaris; IRIX; HPUX; Digital Unix, UnixWare, AIX, SCO, ReliantUNIX, DGUX, Darwin/Mac OS, OpenStep/Mach, and DYNIX/ptx. Note that an Apache server using a DSO module may be approximately 20 percent slower at startup and approximately 5 percent slower during run time. On top of that, DSO is not always available in all platforms. Therefore, I do not recommend DSO for a production environment. It is great, however, for experimenting with modules in a development or staging environment. |

### Requirements for running an Apache Web server

Before displaying the Powered by Apache logo on your Web server, you want to make sure your Web server has enough “power” to run it.

Fortunately, Apache does not require massive computing resources to run. It runs fine on a Linux system with 5 to 12MB of hard disk space and 8MB of RAM. However, just being able to run Apache is probably not what you had in mind. Most likely, you want to run Apache to serve Web pages, launch CGI processes, and take advantage of all the wonderful stuff that the Web has to offer. In that case, you want disk space and RAM size figures that reflect your load requirements. You can go about this in two ways: you can ask someone who runs a similar site with Apache and find out what type of system resources they’re using; or, you can try to figure out your realistic needs after you’ve installed Apache on your system.

In the latter case, you can use system utilities such as `ps`, `top`, and so on to display memory usage by a particular Apache process. You can then determine the total memory needed by multiplying a single process’s memory usage by the total number of Apache processes that will be running at peak hours (see the `MaxSpareServers` directive in Chapter 4). This should give you a reasonable estimate of your site's RAM requirements for Apache. If you plan to run several CGI programs on your Apache server, you have to determine memory usage for these programs as well, and take this additional need into account. One of the ways you can determine your CGI program memory requirements is run the CGI program and use the `top` utility to watch how much memory it uses and then multiply that amount of memory by the number of CGI requests you need to be able to fulfill simultaneously.

The disk requirements for Apache source or binary files shouldn't be a concern with most systems because Apache binaries take no more than 1MB of space and the source file is about 5MB. You should really pay attention, however, to the log files that Apache creates, because each log entry takes up approximately 80 bytes of disk space. If you expect to get about 100,000 hits in a day, for example, your Apache access log file may be 8,000,000 bytes. In Chapter 8, you'll learn how to rotate the log files by emptying or archiving the log file and replacing it with a new one.

Finally, consider whether you have appropriate bandwidth for running a Web server. Estimating bandwidth requirement is not an easy task but you can come up with ballpark figures by doing a bit of math. Here is what you will need:

- **The average Web page size for your Web site:** If you don't know this already, you can run the following command in your document root directory to find out the average size of your Web pages:

```text
find_path_to_doc_root -type f -name "*.html" -ls | \
awk 'BEGIN{ FileCNT = 0; T_SIZE = 0;} \
{ T_SIZE += $7; FileCNT++} \
END{print "Total Files:", FileCNT, \
"Total Size:", T_SIZE, \
"Average Size:", T_SIZE / FileCNT;}'
```

**Note** Don't forget to replace `path_to_doc_root` with the actual document root directory of your Web site. For example, for a Web site with document root /www/mystsite/htdocs, the above script returns the following output:

```text
Total Files: 332 Total Size: 5409725 Average Size: 16294.4
```

- **The number of average size Web pages you can serve** (assuming that Apache has no bottlenecks of its own and totally ignoring the bandwidth utilized by incoming requests): For example, say you have an ISDN (128Kbits/sec) connection to the Internet and your average file size is 16K. Because 128 kilobits per second = 128/8 kilobytes per second = 16 kilobytes per second, you can send one average size file per second. If you include the other overhead, such as bandwidth needed for the inbound request traffic, you probably cannot service a request per second. In this case, network overhead becomes a big bottleneck if you wanted to allow *N* (where *N* > 1)
