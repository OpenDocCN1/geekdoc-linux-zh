
and another to do on-the-fly compression and expansion of executable files.

It’s worth noting that although serial access of compressed files can be useful, there is quite a performance penalty on random access of such files. There’s also the obvious trade-offs between disk space, latency, and processor cycles.

## Encryption

Normally, all security is lost when the system can be physically accessed by an intruder. Matt Blaze, of Bell Labs, has written a cryptographic file system which can be plugged into several different kinds of operating systems. Such a system offers some security against such an intruder because even if the raw disk is compromised, user data cannot be easily extracted or modified. This security is because, without a password which is provided when the system is mounted, the data on that partition appears to be random bits.

## Automounting

Some systems reside in a large network environment, with many file systems available for mounting under NFS. It is a burden to either mount all these when a system is started or to force the user to mount them as they are needed. An automounter for Linux and other systems has been derived from the 4.4 BSD Automounter. It automatically mounts file systems when they are first referenced and it removes the NFS link when they have not been referenced for some reasonable interval. This program is available by ftp on the Internet.

## Memory mapped files

When address spaces were small, it made sense to extract data from files or write data to files in a piecemeal manner. Now that systems have very large address spaces, a different approach can be considered.

Memory mapped files are files that, when opened, appear in the process' virtual address space in their entirety. This is especially useful when the file holds structured data such as a database being accessed or an object file being created.

Linux offers memory mapped files in its development kernels. While they are not fully implemented nor reliable (reported problems relate to reading and writing shared files), they show great promise for the future. The mmap manpage gives some hint of what this will become when it is completed.

### 5.3.3 Redirection, Pipes and Named Pipes

To restate some points from page 153, the file descriptor returned from the open system call is used to index a table inside the kernel which identifies a process' open files. This file descriptor is the first argument to system calls such as read and write. Since it can refer to either a file or a peripheral device, the I/O system calls refer equally well to file or peripherals.

#### Redirection

“Redirection” is the mechanism whereby a child process’ input and output paths, normally the keyboard and display, are changed to refer to some other path before the child process starts execution.

The Linux (and Unix) model for starting a process supports redirection very nicely.

When a child process is created, using the execve system call, it inherits all the open files of the parent. Since it has only the file descriptors, it cannot tell what they refer to.

Thus the child process has only to change the file descriptors before the execve system call. The code in Figure 5.22 shows how this is done.

```c
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>
/* Error checking has been omitted to simplify code. */

main() {
    int new_out;
    char *arg_list[] = {"cmd_file", 0};
    char *env_list[] = {0};
    new_out = open("substitute_file", O_WRONLY|O_CREAT);
    if (fork() == 0){    /* is this the child process? */
        dup2(new_out, 1);  /* connect std out to file */
        close(new_out);    /* close other access to file */
        execve("cmd_file", arg_list, env_list);
    }
    /* wait for child to finish */
    wait();
    exit(0);
} /* main */
```

![](img/bd9544b8c1ad3b1347c84630c5d698e1_180_0.png)

#### Pipes

Figure 5.23 and the code in Figure 5.24 show the ease with which pipes are implemented in the shell. The shell merely creates a pipe, forks two children, and closes its copy of the pipe. The first child closes the output end of its copy of the pipe and attaches the input end to its standard output; the second child closes the input end of its copy of the pipe and attaches the output end to its standard input. Each child then does an `execve` on the appropriate program and those processes are firmly connected by the pipe.

Without this inheritance, the system call to create a child would be riddled with arguments to deal with input and output ports, memory allocation, etc. The following section shows the power of this philosophy.

**Extended notation**

The start of this subsection showed how Linux shells can easily connect one process to another via pipes. Although the conventional model is that of a linear flow of data through filters, Linux can easily support extensions such as seen in the Georgia Tech new shell.

![](img/bd9544b8c1ad3b1347c84630c5d698e1_181_0.png)

This shell, built nearly twenty years ago, could define a network of pipe-connected programs. By default, each program executed by this shell had three standard input and three standard output ports. An extended syntax allowed one to specify how data were to flow among the programs.

This shell used only the "\>" symbol for redirection. It required that there be no space between the "\>" and the source or destination file, e.g., "program >filename" redirected the process output to a file and "\<filename> program" redirected the process input from a file. An optional port number could be placed opposite the file name, thus "\>2>filename program" and "program filename>3" would redirect the second output and third input ports respectively. A string "\<filename1 > filename2" would be ambiguous because there is whitespace on both sides of the "\>". The pipe symbol "|" joined two programs. This symbol could be modified with port and program numbers, i.e., "2|3.1" or in general "<i>out.port1</i> prog.num.in.port".

A trivial example in Figure 5.25 shows how three programs are used: the *generate daily* program collects normal orders and special orders into a stream of daily transactions; the *update* program builds a journal, a new master file, and a list of rejected transactions from the old master ledger and the stream of daily transactions; and the *duplicate* program copies the journal to a file and to the printer.

```c
#include <unistd.h>
/* Error checking has been omitted to simplify the example.
   Children don't call exec() to perform their duties. */
main() {
  int count, pipes[2];
  char buffer[20];
  pipe(pipes);
  if (fork() == 0){  /* is this the child process? */
    close(pipes[0]);  /* close the read end */
    dup2(pipes[1], 1);  /* connect write end to std out */
    close(pipes[1]);  /* close the extra write end */
    /** replace following line by exec call to do real work **/
    write(1,"hello world\n",12); /* put msg in the pipe */
    exit(0);
  }
  if (fork() == 0){  /* is this the child process? */
    close(pipes[1]);  /* close the write end */
    dup2(pipes[0], 0);  /* connect read end to std in */
    close(pipes[0]);  /* close the extra read end */
    /** replace read & write by exec call to do real work **/
    count = read(0,buffer,20); /* get msg from pipe */
    write(1,buffer,count); /* display on the screen */
    exit(0);
  }
  /* get rid of the parent's copy of the
     pipe by closing both ends of it. */
  close(pipes[0]); close(pipes[1]);
  /* wait for both children to finish */
  wait(); wait();
  exit(0);
}
/** main */
```

The port numbers are shown explicitly in this example, but these same values would have been assigned by default.

```
normal_orders>1
special_orders>2
	normal_daily
		1|.1
	old_master>2
	update
		1| { duplicate 1>journal 2| print }
		2>new_master
		3>rejects
```

![](img/bd9544b8c1ad3b1347c84630c5d698e1_183_0.png)

It is clear that the advanced features were of limited value for an interactive command language, but they could be used quite effectively in shell scripts.

## Named Pipes

Later versions of Unix added the named pipe. Normally pipes are shared between descendents of the process which created the pipe. This invention permits processes to communicate by a pipe which is not created by a common ancestor. Instead, one process can create a pipe and advertise it by an entry in the file system. Another process can open this pipe and read and write to it just as it would a file. This is an especially useful device for communication between a user process and a daemon process which is running in the background.

## 5.3.4 Other File Systems

- read-only access of HPFS (OS/2) file systems is an option built into the kernel
