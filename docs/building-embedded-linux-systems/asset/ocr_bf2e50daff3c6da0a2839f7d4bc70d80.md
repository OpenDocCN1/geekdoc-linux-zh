```
```
2.6.22  ->  2.6.22.1-rt9
Downloading patch-2.6.22.1.bz2
--22:16:39--  http://www.kernel.org/pub/linux/kernel/v2.6/patch-2.6.22.1.bz2
               -> `/home/rostedt/.ketchup/patch-2.6.22.1.bz2.partial'
Resolving www.kernel.org... 204.152.191.37, 204.152.191.5
Connecting to www.kernel.org[204.152.191.37]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 538 [application/x-bzip2]

100%[===========================================>] 538         --.-K/s

22:16:39 (38.95 MB/s) - `/home/rostedt/.ketchup/patch-2.6.22.1.bz2.partial' saved [538/538]
```

```

```
```
Applying patch-2.6.22.1.bz2
Downloading patch-2.6.22.1-rt9
--22:16:39--  http://people.redhat.com/mingo/realtime-preempt/patch-2.6.22.1-rt9
               -> `/home/rostedt/.ketchup/patch-2.6.22.1-rt9.partial'
Resolving people.redhat.com... 66.187.233.237
Connecting to people.redhat.com[66.187.233.237]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1,779,906 (1.7M) [text/plain]

100%[===========================================>] 1,779,906   382.30K/s  ETA 00:00

22:16:44 (381.23 KB/s) - `/home/rostedt/.ketchup/patch-2.6.22.1-rt9.partial' saved [1779906/1779906]

Applying patch-2.6.22.1-rt9
Current directory renamed to /home/rostedt/linux-2.6.22.1-rt9
`/tmp5 cd  `
`~/linux-2.6.22.1-rt9$`
```

```

The first two commands made an empty directory and changed into it. Then, we ran `ketchup -G 2.6.22`. The `-G` option caused the command to ignore GPG checksums, and was used because we did not download any checksums. This command automatically downloaded the Linux kernel tarball from the `kernel.org` site and installed the Linux tree in the current directory.

The next command was `ketchup -r -G 2.6.22.1-rt9`. The `-r` has `ketchup` rename the current directory to the Linux version that is installed at completion. You can see from the output that the command first downloaded and installed the `.1` stable patch, then the `-rt9` version of the RT patch.\* Finally, we entered `cd .` to display the current directory and show that `ketchup` renamed it to `linux-2.6.22.1-rt9`. We could have skipped the `ketchup -G 2.6.22` command and simply entered `ketchup -r -G 2.6.22.1-rt9`, but that would have downloaded the `2.6.22.1` stable tarball, and we wanted to show how `ketchup` can do multiple patches in a single step.

\* All the patches and tarballs that `ketchup` downloads are stored in a `~/.ketchup` directory and will be used for subsequent `ketchup` executions.