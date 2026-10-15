```
/usr/include/architecture/i386/cpu.h
/usr/include/cpio.h
/usr/include/gcc/darwin/3.3/c++/bits/cpp_type_traits.h
/usr/include/gcc/darwin/4.0/c++/bits/cpp_type_traits.h
/usr/include/netinet/tcp.h
/usr/include/netinet/tcp_fsm.h
/usr/include/netinet/tcp_seq.h
/usr/include/netinet/tcp_timer.h
/usr/include/netinet/tcp_var.h
/usr/include/netinet/tcpip.h
/usr/include/tcpd.h
```

lots of output omitted

```
/usr/X11R6/lib/X11/fonts/encodings/microsoft-cp1258.enc
/usr/X11R6/lib/X11/locale/ibm-cp1133
/usr/X11R6/lib/X11/locale/microsoft-cp1251
/usr/X11R6/lib/X11/locale/microsoft-cp1255
/usr/X11R6/lib/X11/locale/microsoft-cp1256
```

# Note

This type of search can take a long time on a busy system. When I ran this command on a loaded server, it took almost 5 minutes to complete!

5. To find a list of the directories I’ve created in my home directory, I can use the –type specifier with one of the values shown in Table 22.2. Here’s one example:

```
$ find . -type d -print
.
./OWL
./OWL/Doc
./OWL/WordMap
./elm
./Archives
./InfoWorld
./InfoWorld/PIMS
./Mail
./News
./bin
./src
./temp
$
```

| Letter | Meaning |
| --- | --- |
| d | Directory |
| f | File |
| l | Link |

# TABLE 22.2 Helpful find -type File Types

6. To find more information about each of these directories, I can use the -exec option to find, which specifies a subcommand to execute against each file in the result set. Unfortunately, I cannot simply enter the command; the exec option must be used with {} , which will be replaced by the matched filename, and \; at the end of the command. (If the \ is left out, the shell will interpret the ; as the end of the