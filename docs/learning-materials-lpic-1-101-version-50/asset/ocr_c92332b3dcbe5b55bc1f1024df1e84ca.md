# # Answers to Guided Exercises

1. Divide the following shared library names into their parts:

| Complete file name | Library name | so suffix | Version number |---|---|---|---| | `linux-vdso.so.1` | `linux-vdso` | `so` | `1` | | `libprocps.so.6` | `libprocps` | `so` | `6` | | `libdl.so.2` | `libdl` | `so` | `2` | | `libc.so.6` | `libc` | `so` | `6` | | `libsystemd.so.0` | `libsystemd` | `so` | `0` | | `ld-linux-x86-64.so.2` | `ld-linux-x86-64` | `so` | `2` |

2. You have developed a piece of software and want to add a new shared library directory to your system ( `/opt/lib/mylib` ). You write its absolute path in a file called `mylib.conf` .

+   o In what directory should you put this file?
+   
+   /etc/ld.so.conf.d

+   o What command should you run to make the changes fully effective?
+   
+   ldconfig

3. What command would you use to enumerate the shared libraries required by `kill` ?

`ldd /bin/kill`