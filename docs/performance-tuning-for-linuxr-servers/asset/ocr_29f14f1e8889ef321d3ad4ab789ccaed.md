```
I[OS: i686-pc-linux-gnu]
[TIMING_0: 0]
[LMBENCH_VERSION: lmbench-2alpha13]
[USER: ]
[HOSTNAME: herkimer.itc.austin.ibm.com]
[NODENAME: herkimer.itc.austin.ibm.com]
[SYSCNAME: linux]
[PROCESSOR: i686]
[MACHINE: i686]
[RELEASE: 2.6.3]
[VERSION: #1 SMP Wed Mar 10 19:51:47 CST 2004]
[...]
```

This section provides the output of several system calls run for a short period of time in a loop. It also calculates the average time amount of time run divided by the number of system calls successfully executed.

```
Simple syscall: 0.4189 microseconds
Simple read: 0.7907 microseconds
Simple write: 0.6517 microseconds
Simple stat: 67.6274 microseconds
Simple fstat: 1.5631 microseconds

Simple open/close: 54.5922 microseconds
Select on 10 fd's: 6.7662 microseconds
Select on 100 fd's: 34.5312 microseconds
Select on 250 fd's: 82.6312 microseconds
Select on 500 fd's: 189.6176 microseconds
Select on 10 tcp fd's: 8.2204 microseconds
Select on 100 tcp fd's: 52.6321 microseconds
Select on 250 tcp fd's: 127.5116 microseconds
Select on 500 tcp fd's: 248.5455 microseconds
Signal handler installation: 1.742 microseconds
Signal handler overhead: 9.899 microseconds
Protection fault: 1.310 microseconds
Pipe latency: 28.2951 microseconds
AF_UNIX sock stream latency: 97.5933 microseconds
Process fork+exit: 806.4286 microseconds
Process fork+execve: 2265.0000 microseconds
Process fork/bin/sh -c: 10137.0000 microseconds
File /usr/tmp/XXX write bandwidth: 3923 KB/sec
n=2048, usecs=12993
Pagefaults on /usr/tmp/XXX: 6 usecs
```

This section provides the size of an mmap region and the number of microseconds to complete a mapping of that size.

```
"mappings
0.524288 30
1.048576 43
2.097152 71
4.194304 121
8.38988 219
16.777216 412
33.554432 848
67.108864 1691
134.217728 3326
268.435456 6750
536.870912 14383
```

This section shows how long in microseconds it takes to complete a read from a file system.

```
"File system latency
64     1000     5307     10741
1k     1000     3835     7716
4k     1000     3770     7717
16k    1000     2602     6395
```

This section provides latency timings for various network connections and a summary of the bandwidth of several local networking protocols.

```
UDP latency using localhost: 93.2020 microseconds
TCP latency using localhost: 177.5119 microseconds
RPC/tcp latency using localhost: 239.6613 microseconds
RPC/udp latency using localhost: 140.2291 microseconds
```