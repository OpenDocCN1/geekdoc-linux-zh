
## 12.4. Configure the Application for the Performance Hunt

The next step in the investigation is to set up the application for the performance hunt. prelink is a small and self-contained application. In fact, it does not even use shared libraries (it is statically linked). However, it is a good idea to recompile it with all the symbols so that we can examine it in the debugger(gdb) if we need to. Again, this uses the configure command to generate the makefiles. We must download the source to prelink and recompile it with symbols. We can once again download the rms for prelink from Red Hat. The source will be installed in /usr/src/redhat/SOURCES. Once we unpack prelink's source code, we compile it as shown in Listing 12.6.

Listing 12.6.

```
env CFLAGS=-g3 ./configure
gmake
```

After prelink is configured and compiled, we can use the binary compiled to investigate the performance problems.

## 12.5. Install and Configure Performance Tools

The next step in the hunt is to install the performance tools. In this case, neither ltrace nor profile will be of help. profile is used to profile applications that use a significant amount of CPU time, and because preload uses only about 3 percent of the CPU when running, profile will not help us. Because the preload binary is statically linked and does not use any shared libraries, ltrace will also not help us. However, strace, the system call tracer, may help, so we need to install that.

## 12.6. Run Application and Performance Tools

Now we can finally analyze the performance characteristics of the different modes of prelink. As you just said, prelink does not spend much time using the CPU; it spends all its time on disk I/O. prelink must call the kernel for disk I/O, we should be able to trace its execution using the strace tool. Because the quick mode of prelink does not appear to be much faster than the standard full-run, we compare both strace to see whether any behavior shows up.

At first, we use strace to trace the slower run of prelink. This is the run that initializes the cache that is used when prelink is in quick mode. Initially, we use strace to show the summary of the calls that prelink made and see how long each took to complete. The command to do this is in Listing 12.7.

Listing 12.7.

```
[root@localhost prelink]# # strace -c -o af_sum
/usr/sbin/prelink -af

/* 31 vars */ = 0
/usr/sbin/prelink:
/usr/libexec/autopackage/luau-downloader.bin: Could not parse '/usr/libexec/autopackage/luau-downloader.bin: error while loading shared libraries: libau.so.2: cannot open shared object file: No such file or directory'
/..
/usr/sbin/prelink: /usr/lib/mozilla-1.6/regchrome: Could not parse '/usr/lib/mozilla-1.6/regchrome: error while loading shared libraries libxpcom.so: cannot open shared object file: No such file directory'
```

Listing 12.7 is also a sample of prelink's output. prelink is struggling when trying to prelink some of the system executables and libraries. This information becomes valuable later, so remember it.

Listing 12.8 shows the output file that the strace command in Listing 12.7 generated.

Listing 12.8.

```
[root@localhost prelink]# # cat af_sum
execve("/usr/sbin/prelink", "/usr/sbin/prelink", "-af")
% time          seconds         usecs/calls      errors syscall
77.87           151.249181      65 2315836 read
11.93          21.263231      55 421593 pread
3.59           6.976880       63 110585 pwrite
1.70           3.294193       17 196518 mmap
1.02           1.977343       32 61774 stat
0.97           1.897097       40 47820 open
0.12           1.406801       249 5369 vfork
```

## 12.7. Simulating a Solution

The information revealed by strace shows that prelink is spending a lot of time trying to open and analyze binaries that cannot possibly prelink. The best way to test whether caching of linked binaries could improve prelink's performance is to modify prelink so that it adds all linked binaries to its initial cache. Unfortunately, adding code to these "unlinked" binaries could be a complicated process that involves a good amount of knowledge about the internals of prelink. An easier method is to simulate the cache by replacing all linked binaries with a known linked binary. This causes the formerly linked binaries to be ignored when run. This is exactly what would happen if we were having a cache, so we can use it to estimate the performance increase we would see if prelink were to cache and ignore linked binaries.

To start the experiment, we copy all the files in /usr/bin/ to sandbox directory and run prelink on this directory. This directory includes binary, shells, and other libraries that cannot be prelinked. We then run prelink on sandbox directory and let it create a new cache rather than the system cache. This is shown in Listing 12.5.

Listing 12.5.

```
/usr/sbin/prelink -C new_cache -f sandbox/
```

Next, in Listing 12.16 we time how long it takes to cache prelink to run. We had to run multiple times until we got a consistent result (the first run warmed the cache for each of succeeding runs). The baseline time in Listing 12.16 is .983 seconds. We have to beat this time for our optimization (improving the cache) to be worthwhile.

Listing 12.16.

```
time /usr/sbin/prelink -C new_cache -q sandbox/
real    0m.983s
user    0m.597s
sys      0m.386s
```

Next, in Listing 12.17, we run strace on this prelink command. This is to record which files prelink opens in the sandbox directory.

Listing 12.17.

```
strace -o strace_prelink_sandbox /usr/sbin/prelink -new_cache -q/
```

We create a new directory, sandbox2, into which we copy all the binaries in the /usr/bin directory. However, we overwrite all the files that prelink "opened" in the preceding strace output with a known good binary, which can be linked. We copy to all binaries rather than just them, so that both sandbox contain the same number of files. After we set up the second sandbox, we run the full version of prelink on this new directory using the command in

Listing 12.18.

```
[root@localhost prelink]#/usr/sbin/prelink -C new_cache2 -f sandbox/
```

## 12.8. Reporting the Problem

Because we have found a problem and potential solution in a pretty low-level piece of system software, it is a good idea to work with the author to resolve the problem. We must at least submit a bug report so that the author knows a problem exists. Submitting the tests we used to discover the problem helps him to reproduce the problem and hopefully fix it. In this case, we will add a bug report to Red Hat's bug (zilla.redhat.com) tracking system. (Most distributions have similar tracking systems.) Our bug report describes the problem that we encountered and the possible solution that we discovered.

When arriving at bugzilla, we first search for bug reports in preprint to see whether anyone else has reported this problem. In no case one so, we see the bug report in Listing 12.22 and wait for the author or maintainer to respond and fix the bug.

Listing 12.22.

```
From Bugzilla Helper:
User-Agent: Mozilla/5.0 (X11; Linux i686; en-US; rv:1.6) Gecko/20040510

Description of problem:

When running in quick mode, preprint does not cache the fact that some binaries cannot be prelinked. As a result it rescans them every time, even if preprint is running in quick mode. This causes the disk to grind and dramatically slows down the whole system.

There are 3 types of executables that it retry during quick mode:

- 1) Static Binaries
- 2) Shell Scripts
- 3) Binaries that rely on unprelinkable binaries. (Such as OpenGL)

For 1&2, it would be nice if preprint cached that fact that executables cannot be prelinked, and then in quick mode check their ctime & mtime, and don't even try to read them if it already knows that they can't be prelinked.

For 3, it would be nice if preprint recorded which libraries are causing the preprint to fail (Take the OpenGL case for example), and record that
