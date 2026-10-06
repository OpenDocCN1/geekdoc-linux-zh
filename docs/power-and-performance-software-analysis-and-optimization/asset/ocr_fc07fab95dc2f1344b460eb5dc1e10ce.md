# 216 CHAPTER 12 Toolchain Primer

While PIC improves security, by keeping the code pages read-only, and can improve memory usage, by preventing the code pages from being dirtied by relocations, it has a negative impact on performance. This impact is caused by all of the indirect calls and data references. The impact is much more significant on 32-bit, where the loss of the EBX register also leads to increased register pressure.

Because dynamic linking allows for an application to be built, or utilize different versions of the same shared library, it can be useful when benchmarking. By default, the dynamic linker searches for shared libraries in the paths configured via /etc/ld.so.conf, or in modern distros, /etc/ld.conf.d. The configured paths can be overridden by setting the LD_LIBRARY_PATH environmental variable. As such, a user performing benchmarking can modify this environmental variable to run the benchmark with multiple revisions of the same library, in order to measure the differences. For instance:

```
$ ls
project1 bench
$ export LD_LIBRARY_PATH=project0/
$ ldd bench
linux-vdso.so.1 -> (0x00007ffaffe0000)
libc.so.6 -> /lib64/liblibc.so.6 (0x0000000371a00000)
lib64/ld-linux-x86-64.so.2 (0x0000000319c00000)
project0.so => /home/jkt/jpa/project0/libproject.so
(0x000000392ae00000)
$ ./bench > result_version
$ export LD_LIBRARY_PATH=project1/
$ ldd bench
linux-vdso.so.1 -> (0x00007ffaffe0000)
libc.so.6 -> /lib64/liblibc.so.6 (0x0000000371a00000)
lib64/ld-linux-x86-64.so.2 (0x0000000319c00000)
project1.so => /home/jkt/jpa/project1/libproject.so
(0x000000392ae00000)
$ ./bench > result_version1
```

The LD_PRELOAD environment variable can be defined as a colon-separated list of libraries the dynamic linker should load first. To see how this can be used to intercept and instrument functions in a shared library, refer to the buGL and Apitrace tools described in Sections 10.2 and 10.3 of Chapter 10.

# 22.2.2 ABI

The Application Binary Interface (ABI) standardizes the architectural interactions between various system components. The ABI defines items, such as the calling conventions, structure layout and padding, type alignments, and other aspects that must remain consistent between various software components to ensure compatibility and interoperability. This section focuses on dealing with the C ABI.