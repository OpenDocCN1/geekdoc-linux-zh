# 12.6. Run Application and Performance Tools

Now we can finally analyze the performance characteristics of the different modes of prelink. As you just said, prelink does not spend much time using the CPU; it spends all its time on disk I/O. prelink must call the kernel for disk I/O, we should be able to trace its execution using the strace tool. Because the quick mode of prelink does not appear to be much faster than the standard full-run, we compare both strace to see whether any behavior shows up.

At first, we use strace to trace the slower run of prelink. This is the run that initializes the cache that is used when prelink is in quick mode. Initially, we use strace to show the summary of the calls that prelink made and see how long each took to complete. The command to do this is in Listing 12.7.

Listing 12.7.

```
[root@localhost prelink]# # strace -c -o af_sum
/usr/sbin/prelink -af

/usr/sbin/prelink:
/usr/libexec/autopackage/luau-downloader.bin: Could
not parse '/usr/libexec/autopackage/luau-downloader.bin: error
while
loading shared libraries: libau.so.2: cannot open shared
object file: No
such file or directory
..
/usr/sbin/prelink: /usr/lib/mozilla-1.6/regchrome: Could not
parse
'/usr/lib/mozilla-1.6/regchrome: error while loading shared
libraries
libxpcom.so: cannot open shared object file: No such file
directory'
```

Listing 12.7 is also a sample of prelink's output. prelink is struggling when trying to prelink some of the system executables and libraries. This information becomes valuable later, so remember it.

Listing 12.8 shows the output file that the strace command in Listing 12.7 generated.

Listing 12.8.

```
[root@localhost prelink]# # cat af_sum
execve("/usr/sbin/prelink", "/usr/sbin/prelink", "-af\], [/*
31 vars
*/] = 0
% time          seconds         usecs/calls      errors syscall

77.87           151.249181      65 2315836 read
11.93          21.263231      55 421593 pread
3.59           6.976880       63 110585 pwrite
1.70           3.294193       17 196518 mmap
1.02           1.977343       32 61774 stat64
0.97           1.897097       40 47820 1 open
0.12           1.406801       249 5369 vfork
```