
# Jtux: A Java/Jython Interface to Standard UNIX Functions

Thirty years ago, when UNIX was new, almost all UNIX application programming was in C, and C is still the "UNIX language," in that the principal UNIX standards use C, UNIX kernels are written in C, and most UNIX programming books, such as this one, show all their examples in C. Today, however, much, if not most, UNIX programming is in anything but C: C++, Java, Perl, Python,[^1] PHP, and so on.

C++ is a special case because you can use the C interface directly, or a very thin C++ class library such as Ux, described in Appendix B. The other languages typically provide interfaces to some classic UNIX system calls that were in POSIX.1990 but not to newer calls like getaddrinfo or msend. So, serious students who want to learn UNIX are forced to learn C or C++, even if they use Java for all their other course work, and developers don't have ready access to system calls they may need.

To solve the problem for Java, I created Java-to-Unix (Jtux). The goals of Jtux are to provide:

- An educational tool for learning UNIX programming with Java or Jython.
- Access to UNIX features that are currently unsupported by Java packages.
- Consistent error handling. An error from a system call, no matter how it's indicated (-1 return, NULL return, error-code return, etc.) always results in throwing a `ErrorException`.

Jtux does not:

- Provide an object-oriented view of the UNIX API.
- Fix any of the inconsistencies in UNIX system-call naming or arguments, or clean up most of the redundancies, as Ux (Appendix B) does. In fact, nearly every Jtux method has the same name and the same arguments as the corresponding POSIX/SUS call because otherwise Jtux wouldn’t work to help students learn to program UNIX. (Jtux does fix the error-handling inconsistencies.)
- Provide portability other than that already provided by POSIX/SUS. Jtux does not work in Java/Jython environments that aren’t hosted on a POSIX/SUS system, such as Windows.
- Work in applets because the Java Native Interface (JNI) that was used to connect Java with the C API does not.

If you want an object-oriented approach to UNIX facilities that’s more in the spirit of Java, you’re better off using other Java packages. For example, use `java.net.Socket`, instead of `jtux.UNetwork`. However, Jtux is the most complete UNIX package for Java or Jython, by a very wide margin.

Jtux covers these 186 system calls:

| abort | getpid | poll | setpgid |
| :--- | :--- | :--- | :--- |
| accept | getrlimit | pread | setrlimit |
| access | getrusage | pselect | setsid |
| alarm | getsid | pthread_sigmask | setsockopt |
| bind | getsockopt | putenv | setuid |
| chdir | getuid | pwrite | shm_open |
| chmod | htonl | read | shm_unlink |
| chown | htons | readdir | shmat |
| chroot | inet_ntop | readlink | shmctl |
| clock | inet_pton | readv | shmdt |
| close | kill | recv | shmget |
| closedir | lchown | recvfrom | sigaction |
| connect | link | recvmsg | sigaddset |
| creat | listen | rename | sigaltstack |
| dup | lockf | rewinddir | sigdelset |
| dup2 | lseek | rmdir | sigemptyset |
| execvp | lstat | S_ISBLK | sigfillset |
| _exit | mkdir | S_ISCHR | siginterrupt |
| exit | mkfifo | S_ISDIR | sigismember |
| fchdir | mknod | S_ISFIFO | sigpending |
| fchmod | mkstemp | S_ISLNK | sigprocmask |
| fchown | mmap | S_ISREG | sigqueue |
| fcntl | mq_close | S_ISSOCK | sigsuspend |
| FD_CLR | mq_getattr | seekdir | sigtimedwait |
| FD_ISSET | mq_notify | select | sigwait |
| FD_SET | mq_open | sem_close | sigwaitinfo |
| FD_ZERO | mq_open | sem_destroy | sleep |
| fdatasync | mq_receive | sem_getvalue | socket |
| fork | mq_send | sem_init | socket |
| freeaddrinfo | mq_setattr | sem_open | stat |
| fstat | mq_timedreceive | sem_open | statvfs |
| fstatvfs | mq_timedsend | sem_post | symlink |
| fsync | mq_unlink | sem_timedwait | sync |
| ftok | msgctl | sem_trywait | system |
| ftruncate | msgrcv | sem_unlink | telldir |
| gai_strerror | msgsnd | sem_wait | times |
| getaddrinfo | msgrcv | semctl | truncate |
| getcwd | mmap | semget | umask |
| getegid | nanosleep | semop | unlink |
| getenv | nice | send | unsetenv |
| geteuid | ntohl | sendmsg | usleep |
| getgid | ntohs | sendto | utime |
| gethostid | open | setegid | wait |
| gethostname | open | setenv | waitpid |
| getnameinfo | opendir | seteuid | write |
| getpgid | pause | setgid | writev |
| getpid | pipe | | |

What's here is all POSIX/SUS calls dealing with files, file systems, directories, sockets, pipes, processes, System V messages/semaphores/shared memory, POSIX messages/semaphores/shared memory, signals, environment, and more. I've tried very hard to be complete; for example, there's not only `write`, but also `pwrite` and `writev`; there's not only `send`, but also `sendmsg` and `sendto`. Every argument of every included function and every field of every structure is supported, except where technically impossible. Functions for terminal I/O, pseudo terminals, interval timers (other than `alarm`), and realtime clocks weren't included, although they could have been. You can add these if you like.

Jython is a terrific system in which to try out UNIX system calls. To show you what Jython and Jtux are like, here's a program that has two processes communicating using datagrams (see Section 8.6):

```python
# Jython example showing use of AF_INET sockets with SOCK_DGRAM.
# System calls used: bind, close, _exit, fork, getaddrinfo,
# recvfrom, sendto, setsockopt, sleep, socket, waitpid
import jtux.UClock as UClock
import jtux.UConstant as UConstant
import jtux.UErrorException as UErrorException
import jtux.UFile as UFile
import jtux.UNetwork as UNetwork
import jtux.UProcess as UProcess
import jtux.Util as UUtil
import java.lang
import jarray

def b_to_s(ba): # convert byte array to string
    s = ''
    for b in ba:
        if b == 0:
            break
        s += chr(b)
    return s

nodename = "localhost"
servername1 = "5431" # unused port for peer 1
servername2 = "5432" # unused port for peer 2
msgsize = 300
hint = UNetwork.s_addrinfo()
hint.ai_family = UConstant.AF_INET
hint.ai_socktype = UConstant.SOCK_DGRAM
infop = UNetwork.AddrInfoListHead()
UNetwork.getaddrinfo(nodename, servername2, hint, infop)
sa_peer2 = infop.ai_next.ai_addr; # both peers need this socket addr
int_opt = UNetwork.SockOptValue.int() # Jtux's way of handling setsockopt values
int_opt.value = 1
pid = UProcess.fork()
if pid == 0: # Peer 1
    msg = jarray.zeros(msgsize, 'b') # jarray is a standard Jython module
    UNetwork.getaddrinfo(nodename, servername1, hint, infop)
    sa_peer1 = infop.ai_next.ai_addr
    UClock.sleep(1); # let peer 2 startup first -- not the best approach
    fd_skt = UNetwork.socket(UConstant.AF_INET, UConstant.SOCK_DGRAM, 0)
    UNetwork.setsockopt(fd_skt, UConstant.SOL_SOCKET, UConstant.SO_REUSEADDR, int_opt, 0)
    UNetwork.bind(fd_skt, sa_peer1, 0)
    sa_sender = UNetwork.s_sockaddr_in()
    sa_len = Util.IntHolder(); # Jtux class for passing ints by reference
    maxmsgs = 4
    for i in xrange(maxmsgs + 1):
        if i == maxmsgs:
            m = "Stop"
        else:
            m = "Message #" + str(i)
        UNetwork.sendto(fd_skt, m, len(m), 0, sa_peer2, 0)
        if i == maxmsgs:
            break
        nrcv = UNetwork.recvfrom(fd_skt, msg, len(msg), 0, sa_sender, sa_len)
        print "Peer 1 got \"" + b_to_s(msg) + "\" from " + str(sa_sender)
    UFile.close(fd_skt)
    print "Peer 1 exiting"
    UProcess._exit(UConstant.EXIT_SUCCESS)
else: # Peer 2
    msg = jarray.zeros(msgsize, 'b') # jarray is a standard Jython module
    fd_skt = UNetwork.socket(UConstant.AF_INET, UConstant.SOCK_DGRAM, 0)
    UNetwork.setsockopt(fd_skt, UConstant.SOL_SOCKET, UConstant.SO_REUSEADDR, int_opt, 0)
    UNetwork.bind(fd_skt, sa_peer2, 0)
    sa_sender = UNetwork.s_sockaddr_in()
    sa_len = Util.IntHolder()
    while 1:
        nrcv = UNetwork.recvfrom(fd_skt, msg, len(msg), 0, sa_sender, sa_len)
        if b_to_s(msg[:4]) == "Stop":
            break
        print "Peer 2 got \"" + b_to_s(msg[:nrcv]) + "\" from " + str(sa_sender)
        msg[0] = ord('m')
        UNetwork.sendto(fd_skt, msg, len(msg), 0, sa_sender, sa_len.value)
    UFile.close(fd_skt)
    UProcess.waitpid(pid, None, 0)
    print "Peer 2 exiting"
```

And here's a Java example:

```java
// Java example that recursively descends the directory tree.
import jtux.*;

class TreeList {
    static void list(String entry, int level) {
        int dir_fd = -1;
        try {
            String tabs = "";
            for (int i = 0; i < level; i++)
                tabs += "\t";
            long dir = -1;
            try {
                dir = UDir.opendir(entry);
            }
            catch (UErrorException e) {
                System.out.println(tabs + entry + " - " + e);
                return;
            }
            dir_fd = UFile.open(".", UConstant.O_RDONLY);
            UProcess.chdir(entry);
            UDir.s_dirent dirent = new UDir.s_dirent();
            UFile.s_stat stbuf = new UFile.s_stat();
        }
    }
}
```

[^1]: Jython is an implementation of Python, written in Java, that runs in the Java environment, so any Java class can be accessed directly. For example, in Jython you write your user interface using AWT or Swing, rather than with Tkinter. That's why Jtux works with Jython just as well as with Java. For more on Jython, go to www.jython.org.
