
# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
root@forensic1:~# dc3dd if=/dev/ssd hof=thumb.dc3dd hof=thumbcopy.dc3dd hash=md5
```

dc3dd 7.2.641 started at 2017-04-25 11:06:26 -0400
compiled options:
command line: dc3dd if=/dev/ssd hof=thumbcopy.dc3dd hash=md5
device size: 250879 sectors (probed), 128,450,048 bytes
sector size: 512 bytes (probed)
12850048 bytes ( 122 M ) copied ( 100% ), 18 s, 7 M/s
12850048 bytes ( 122 M ) hashed ( 100% ), 0 s, 611 M/s

input results for device `/dev/ssd`
250879 sectors in
0 bad sectors replaced by zeros
43108c653d4724181cf8eed75c20c2de4 (md5)

output results for file `thumb.dc3dd`
250879 sectors out
[ok] 43108c653d4724181cf8eed75c20c2de4 (md5)

output results for file `thumbcopy.dc3dd`
250879 sectors out
[ok] 43108c653d4724181cf8eed75c20c2de4 (md5)

dc3dd completed at 2017-04-25 11:06:43 -0400

```
root@forensic1:~# ls -lh thumb*
-rw-r--r-- 1 root root 123M Apr 25 11:06 thumb.dc3dd
-rw-r--r-- 1 root root 123M Apr 25 11:06 thumbcopy.dc3dd
```

The demonstration illustrates collects two images simultaneously. You can see we selected to hash the output files (hof) using the md5 algorithm (hash=md5). The output shows the single input stream was hashed, but there are two output streams, and each was hashed and verified separately. This is a very useful feature of dc3dd.

Note that dc3dd outputs raw images. They can be hashed exactly the same as output: Directly hashed with your hashing algorithm of choice (sha1sum, md5sum, etc.), or in case of split files, using the cat command to stream the output of multiple files to the hash program.

Now we'll continue our look at alternative imaging tools with a utility that is used to collect and manage Expert Witness (E01 or EWF) files, one of the more ubiquitous formats used in computer forensics today.

# libewf and ewfacquire

There may be times when you are asked to perform examinations collected by someone else, or perhaps your organization has elected to standardize on a given format for forensic images. In any case, chances you will eventually come across Expert Witness format files (EWF, commonly referred to as "EnCase" format). There are many tools that can read, convert or work with these images. In this section we will learn to acquire and manipulate evidence the EWF format.

We will explore a set of tools belonging to the libewf project. These tools provide the ability to create, view, convert and work with expert witness evidences.

One of the benefits of using libewf before advanced forensic utilities is because it needs to be installed first to support the required libraries for other packages to support EWF image formats. The libewf tools and detailed project information can be found at https://github.com/libyal/libewf/

We will start by installing libewf using sbtools. Check your distribution documentation, or the install instructions at the website above if you are using a distribution other than Slack. Libewf has no additional requirements (you can view the info file with sbind -tei libewf). When you start the installation process be sure to take the time to read the README file that displays.

Cleaning for libewf-20140608...

Once the download, compile, build, and installation of the resulting package is complete, the actual totals are placed in /usr/bin. We will have a closer look at the following:

- ewfacquire
- ewfverify
- ewfinfo
- ewfacquirestream (in a later section)

We'll start with the ewfacquire command used to create EWF files that can be used in other programs. The easiest way to describe how ewfacquire works is to run it. There are a number of options available. To get a list of options (there are many), just run ewfacquire -h. Simply issue the image with the name of the file or physical device you wish to image. Unless you memorize or script the options, this is the easiest way to run. You are prompted for required information, to be stored with the data in the EWF format (the following output is interactive):

```
root@forensic1:-# lsscs
...
[2:0:0:0] disk SanDisk Cruiser Mini 0.2 /dev/sdb
root@forensic1:-# ewfacquire /dev/sdb ewfacquire 20140608
```

Device information:
Bus type: USB
Vendor: SanDisk
Model: Cruiser Mini
Serial:

Storage media information: Device
Media type: Removable
Media size: 128 MB (12845048 bytes)
Bytes per sector: 512

Acquire parameters, please provide the necessary input
Image path and filename without extension: case1.disk2
Case number: 2017-001
Description: Thumb drive seized by guy
Evidence number: 2017-001-002
Examiner name: Barry. Grundy
Notes:
Media type (fixed, removable, memory) [removable]:
Media characteristics (logical, physical) [logical]:

Use EWF format (ewf, ftk, encase, encase2, encase3, encase4, encase5, encase6, ewfx) [encase]:
Compression method (deflate) [deflate]:
Compression level (none, fast, best) [none]:
Start to acquire at offset (<= 12845048) [0]:
Of bytes to acquire (<= 12845048) [12845048]:
Evidence file size in bytes (<= 7.9 MiB) [1.4 GiB]: 32M
Of bytes per sector (<= 429496725) [512]:
Sectors to read at once (16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768) [64]:
Sectors to be used as granularity (<= 64) [64]:
Of retries when a read error occurs (<= 255) [2]:
Zero sectors on read error (like EnCase behavior) (yes, no) [no]:

The following acquisition parameters were provided:
Image path and filename: case1.disk2.E01
Case number: 2017-0081
Description: Thumb drive seized from guy
Evidence number: 2017-081-002
Examiner name: Barry. Grundy
Notes:
Media type: removable disk
Is physical: yes
EWF format: EnCase (.E01)
Compression method: deflate
Compression level: none
Acquire start offset: 0
Number of bytes to acquire: 122 MiB (12845048 bytes)
Segment file size: 32 MiB (3355432 bytes)
Bytes per sector: 512
Block size: 64 sectors
Error granularity: 64 sectors
Retries on read error: 2
Zero sectors on read error: no

Continue acquire with these values (yes, no) [yes]:

Acquire started at: Apr 25, 2017 12:24:45
This could take a while.

Status at 20%:
acquired 25 MiB (26443776 bytes) of total 122 MiB (128450048 bytes).
completion in 16 second(s) with 6.1 MiB/s (6422502 bytes/second).

...
Acquire completed at: Apr 25, 2017 12:27:08

Write: 122 MiB (128450236 bytes) in 2 minute(s) and 23 second(s) with 877 KiB/s (898253 bytes/second).

MD5 hash calculated over data: efacquire: SUCCESS
43108c653d4272418cf8eeed75c20cde24

```
root@forensic:~# ls -lh casel.*
-rw-r--r-- 1 root root 32M Apr 25 12:24 casel.disk2.E01
-rw-r--r-- 1 root root 32M Apr 25 12:27 casel.disk2.E02
-rw-r--r-- 1 root root 32M Apr 25 12:27 casel.disk2.E03
-rw-r--r-- 1 root root 27M Apr 25 12:24 casel.disk2.E04
```

In the above command, user input is shown in bold. Places where there is no input provided by the user, the defaults (shown in brackets) are used. Notice that efacquire gives you several options for image formats that can be specified. The file(s) specified by the user is given an EWF extension and placed in the path directed by the user. Finally, an MD5 hash is provided at the end of the output for verification. As dc3dd, you also get a time stamp for documentation.

You can also issue a single command and specify those options we used above on line. For example, to get similar results, we can issue the following command:

```
root@forensic:~# efacquire -C "2017-001" -d sha1 -D "Thumb drive seized from guy" -"Barry. Grundy" -E "2017-001-002" -m removable -M physical -S 32M -t case1.disk2 -u /dev/sdb
efacquire 20140608
```

Acquired completed at: Apr 25, 2017 12:39:20

Written: 122 MiB (124850392 bytes) in 16 second(s) with 7.6 MiB/s (8028149 bytes/second).

Once acquired, the resulting files from efacquire are compatible with any software that will read EWF format images. We will be using some forensics tools to later do that.
