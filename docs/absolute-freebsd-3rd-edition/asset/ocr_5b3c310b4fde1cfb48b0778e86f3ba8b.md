the individual libraries in those directories. My main mail server has 170 shared libraries; my main web server, 244; my desktop, 531.

If a program dies at startup with a complaint that it can't find a shared library, that library won't be on this list. Your problem then amounts to installing the desired library into a shared library directory or adding the library directory to the list of directories searched. You could just copy every shared library you need to /usr/lib, but this makes system management very difficult\u2014much like with a filing cabinet where everything is filed under P for paper. Adding directories to the shared library list is a better idea in the medium to long term.

# **Adding Library Directories to the Search List**

If you've added a new directory of shared libraries, you must add it to the list ldconfig(8) searches. Check these ldconfig(8) entries in /etc/defaults/rc.conf:

```
ldconfig_path="/usr/lib/compat /usr/local/lib /usr/local/lib/compat/pkg" ldconfig_local_dirs="/usr/local/libdata/ldconfig"
```

The ldconfig_paths variable lists common locations for libraries. While out-of-the-box FreeBSD doesn't have the directory /usr/local/lib, most systems grow one shortly after install. Similarly, libraries for compatibility with older versions of FreeBSD go in /usr/lib/compat. The location for storing old versions of libraries installed by packages is /usr/local/lib/compat/pkg. The /lib and /usr/lib directories get searched by default, but the paths in this variable are common locations for shared libraries.

Ports and packages use the ldconfig_local_dirs variable to get their shared libraries into the search list without just dumping everything into /usr/local/lib. Packages can install a file in this directory. The file is named after the package and contains a list of directories with the libraries installed by the package. The ldconfig program checks these directories for files, reads the paths in the files, and treats those as additional library paths. For example, the Perl 5 package installs shared libraries in /usr/local/lib/perl5/5.24/mach/CORE. The port also installs a file called /usr/local/libdata/ldconfig/perl5, containing only a single line