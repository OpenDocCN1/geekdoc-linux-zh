Version information:
/sbin/1p:
1dlib1.so.2 (GLIBC 2.2.5) => /lib64/ldlib1.so.2
libc.so.6 (GLIBC 2.7) => /lib64/libc.so.6
libc.so.6 (GLIBC 2.4) => /lib64/libc.so.6
libc.so.6 (GLIBC 2.3.4) => /lib64/libc.so.6
libc.so.6 (GLIBC 2.2.5) => /lib64/libc.so.6
/lib64/ldlib1.so.2:
ld-linux-x86-64.so.2 (GLIBC PRIVATE) => /lib64/ld-linux-x86-64.so.2
libc.so.6 (GLIBC PRIVATE) => /lib64/libc.so.6
libc.so.6 (GLIBC 2.2.5) => /lib64/libc.so.6
/lib64/libc.so.6:
ld-linux-x86-64.so.2 (GLIBC PRIVATE) => /lib64/ld-linux-x86-64.so.2
ld-linux-x86-64.so.2 (GLIBC 2.3) => /lib64/ld-linux-x86-64.so.2
wsl1: #

One of the key uses for the ldd command is to check for shared library dependencies. It determines whether all of the libraries required by the application in question have been installed. If they have, you won't see any error messages, as shown in the preceding example. If a library file is missing, an error message will be displayed. You can then locate and install the missing library and all will be well with the world.

So, how does an application know which directories to look in when trying to locate a shared library? The applications don't actually check the /etc/ld.so.conf conf file. Instead, they check the library cache and the LD_LIBRARY_PATH environment variables. The library cache is /etc/ld.so.cache. This file contains a list of all the system libraries and is refreshed when the system is initially booted.

This is key. If you add a new dynamic library directory to the /etc/ld.so.conf file, you'll be very frustrated when you try to run the applications that are linked to the libraries in this directory. That's because the library cache hasn't been updated with the new information. To fix this, you have two options:

+   Use **ldconfig**. The `ldconfig` command is used to rebuild the library cache manually.
+   Set **LD_LIBRARY_PATH**. You can also add the path to the `LD_LIBRARY_PATH` environment variable. You probably want to add the new path to the end of the list of directories that may already exist in the variable, so you should use the following commands:
+   
+   ```
+   set LD_LIBRARY_PATH=$LD_LIBRARY_PATH:new_path
+   export LD_LIBRARY_PATH
+   ```

Generally speaking, the first option is the preferred one. This ensures the shared libraries are always available to the applications that need them, even if the system is rebooted. I usually set the value of `LD_LIBRARY_PATH` only in situations where I have two versions of the same shared library installed in different directories and I want to use one version over the other.