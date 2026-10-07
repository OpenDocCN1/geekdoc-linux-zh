# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

The options used above are:

+   if=/dev/sld : Our source device, as indicated by the output of lsscsi

+   hofs-thumb.dc3dd.000 : our output file BASE FMT. Using the hofs option indicates that we want hashes and splits of the output file. In this case, the BASE is thumb.dc3dd. and the format of our extension (FMT) is numerical, three

+   ofsz32M : Since we indicated split files (using hofs or of), we need to specify an output size.

+   hash-sha1 md5 : Since we indicated the input and output files (hofs or of), we need to provide the algorithm we want. In this case we are illustrating that we can use TWO algorithms, and both will be calculated and recorded.

+   log-thumb.dc3dd.log : Indicates that we want the output of dc3dd logged to a file that we specify. Note that you can log hashes separately using slog.

The resulting output (shown by command below) shows 4 split image files, with numerical extensions starting with 000. We also have a log file of hashes and error messages, which we can view with less or cat:

```
root@forensic1:~# ls -lh thumb.dc3dd.*
-rw-r--r-- 1 root 32M Apr 25 10:32 thumb.dc3dd.000
-rw-r--r-- 1 root 32M Apr 25 10:33 thumb.dc3dd.001
-rw-r--r-- 1 root 32M Apr 25 10:33 thumb.dc3dd.002
-rw-r--r-- 1 root 27M Apr 25 10:33 thumb.dc3dd.003
-rw-r--r-- 1 root 2.5K Apr 25 10:53 thumb.dc3dd.log
```

As discussed, the log file contains our hashes and our error messages. For the hashes, the output hash from the imaged device is displayed first (for each hash we requested). If the input hash matches the output hash for a given range (or the whole device), the output hash is preceded with [ok] so you do not have to manually compare the output.

The log file with a time stamp for your documentation.

Another useful feature of dc3dd compared to regular dd is the ability (without the use of external pipes or piping programs) to collect multiple images at the same time. If logistics allows, and I need to collect multiple copies on location to distribute multiple parties, I can have additional output files: