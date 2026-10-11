
On the other hand, a system that has multiple names (actually, it has one canonical name and one or more aliases) is typically used to allow a single physical machine to provide multiple services, such as a Web server and an FTP server. The box has one IP address but two names.

Regardless of why a system has multiple hostnames or IP addresses, `gethostbyname` and `gethostbyaddr` return the complete list of names and addresses, respectively, in the `h_aliases` and `h_addr_list` members of the `struct hostent`. If the IP address or hostname passed to these functions is invalid or if another error occurs, they return `NULL`.

## Example

![](img/be588b36b489136ce784030a08a1d3d4_441_0.png)

## Example

The sample program that follows, `hostinfo`, accepts a hostname as its command-line argument and displays the contents of its corresponding `hostent` structure.

```c
/*
 *  hostinfo.c -- Show the hostent structure for a hostname
 */
#include <sys/socket.h>
#include <netinet/in.h>

#include <arpa/inet.h>
#include <netdb.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(int argc, char *argv[])
{
   struct hostent *buf;
   struct in_addr **paddr;
   char **palias;

   /* Expect the IP addresses on the command-line */
   if(argc != 2) {
       puts("USAGE: hostinfo <host name>");
       exit(EXIT_FAILURE);
   }

   /* Do the lookup */
   if((buf = gethostbyname(argv[1])) == NULL)
       herr_quit("gethostbyname");
   /* Valid hostname, so . . . */
   printf("host info for %s\n", argv[1]);
   /* The canonical hostname */
   printf("name: %s\n", buf->h_name);
   /* All of the aliases */
   puts("aliases:");
   palias = buf->h_aliases;
   while(*palias) {
       printf("\t%s\n", *palias);
       palias++;
   }
   /* h_addrtype better be AF_INET */
   if(buf->h_addrtype == AF_INET)
       puts("type: AF_INET");
   else
       puts("type: unknown");
   printf("length: %d\n", buf->h_length);
   /* All of the IP addresses */
   puts("addresses:");
   paddr = (struct in_addr **)buf->h_addr_list;
   while(*paddr) {
       printf("\t%s\n", inet_ntoa(**paddr));
       paddr++;
   }
}
```

The following listing shows the output from this program:

![](img/be588b36b489136ce784030a08a1d3d4_442_0.png)

## Output

```
host info for ftp.redhat.com
name: ftp.redhat.com
aliases:
type: AF_INET
length: 4
addresses:
    199.183.24.205
    208.178.165.228
    206.132.41.212
```

After performing a DNS lookup on the hostname, it displays each member of the `hostent` structure. The hairy-looking code that prints the IP addresses is necessary because `buf->h_addr_list` decays to a bare pointer, but `inet_ntoa` expects a `struct in_addr` argument.

## What's Next?

This chapter gave you the nickel tour of socket and TCP/IP programming. It also completes the book's coverage of interprocess communication. The next part, "Linux Programming Utilities," introduces you to several tools and utilities that ease some of a programmer's chores. You begin with Chapter 19, "Tracking Source Code Changes," which teaches you how to use RCS, the Revision Control System. RCS is a tool that automates most of the tasks associated with tracking changes to source code files. Why keep track of source code changes? Read on and see!

# PART V—LINUX PROGRAMMING UTILITIES

- 19 Tracking Source Code Changes: The Revision Control System
- 20 A Debugging Toolkit
- 21 Software Distribution
- 22 Programming Project: A Music CD Database

# 19—Tracking Source Code Changes: The Revision Control System

Version control is a process for keeping track of and managing changes made to source code files. Why bother? Because one day you *will* make that one fatal edit to a source file, delete its predecessor, and forget exactly which line or lines of code you "fixed." Because simultaneously keeping track of the current release, the next release, and eight bug fixes manually *will* become too tedious and confusing. Because frantically searching for the backup tape after one of your colleagues overwrote a source file for the fifth time *will* drive you over the edge. Because, one day, over your morning cappuccino, you will say to yourself, "Version control, it's the Right Thing to Do."

This chapter examines RCS, the Revision Control System, a common solution to the version control problem. RCS is a common solution because it is available on almost all UNIX systems, not just on Linux. RCS is maintained by the GNU project. Two alternatives to RCS are CVS, the Concurrent Version System, also maintained by the GNU project, and SCCS, the Source Code Control System, a proprietary product. Topics covered in this chapter include the following:

- Version control terminology
- Creating a source code repository
- Checking files in and out of the repository
- RCS keywords and the *ident* command
- RCS change logs
- Additional RCS commands and utilities

## Why RCS?

More experienced programmers, and especially programmers familiar with other versions of UNIX or UNIX clones, might ask, "Why discuss RCS when CVS is more popular, has more features, and is better suited for use with large programming projects?" First, I consider RCS the easiest introduction to version control concepts. Few beginning programmers have ever heard of version control, much less used version control software. RCS is easy to learn, requires little setup or configuration, and has a small command set. This makes it the ideal vehicle for introducing people to version control concepts. Nevertheless, because CVS is built on and compatible with RCS, the transition to CVS will be smooth.

Moreover, although CVS definitely has a much richer feature set than RCS, these features are of little benefit to neophyte Linux programmers. Few beginning hackers will need, for example, the ability to browse their source code using a Web browser or to make anonymous read/write access to the repository available.

Finally, most beginning programmers will not be working in an environment in which multiple projects are under development or that have a single source code repository that stores the source code for multiple projects, environments for which CVS was designed.

## Version Control Terminology

Before proceeding, however, Table 19.1 lists a few terms that will be used throughout the chapter. Because they are frequently used, it is important that you understand them in the context of RCS and version control.

**Table 19.1: Version Control Terms**

| Term | Description |
| :--- | :--- |
| RCS file | Any file located in an RCS directory, controlled by RCS and accessed using RCS commands. An RCS file contains all versions of a particular file. Normally, an RCS file has a .v extension. |
| Working file | One or more files retrieved from the RCS source code repository (the RCS directory) into the current working directory and available for editing. |
| Lock | A working file retrieved for editing so that no one else can simultaneously edit it. A working file is locked by the first user against edits by other users. |
| Revision | A specific, numbered version of a source file. Revisions begin with 1.1 and increase incrementally, unless forced to use a specific revision number. |

The Revision Control System manages multiple versions of files, usually but not necessarily source code files. RCS automates file version storage and retrieval, change logging, access control, release management, and revision identification and merging. As an added bonus, RCS minimizes disk space requirements because it tracks only file changes.

> **NOTE**
>
> The examples used in this chapter assume that you are using RCS version 5.7. To determine the version of RCS you are using, type `rcs -V`.

RCS can be used for more than just source code files, however. It is capable of tracking changes to any type of text file, such as reports, book chapters, or HTML code. It does not, however, handle binary files. CVS, the Concurrent Version System, does work with binary files, which is why many people use CVS rather than RCS.

### Using RCS

One of RCS's attractions is its simplicity. With minimal setup and only a few commands, you can accomplish a great deal. This section discusses the `ci`, `co`, and `ident` commands as well as the RCS keywords.

### Checking Files In and Out

You can accomplish a lot with RCS using only two commands, `ci` and `co`, and a directory named RCS. `ci` stands for *check in*, which means storing a working file in the RCS directory; `co` means *check out* and refers to retrieving an RCS file from the RCS repository.

To get started, you must create an RCS directory. By default, all RCS commands assume that a directory named RCS exists in the current working directory. So, your first step is to create this directory. Suppose you have several source files in `/home/gomer/editor`. Make that your current directory and create the directory, RCS, as shown in the following:

```
$ cd /home/gomer/editor
$ mkdir RCS
```

All RCS commands executed in `/home/gomer/editor` will use this directory. The RCS directory is also called *the repository*.

> **TIP**
>
> RCS's default behavior is to use a repository in each working directory. This is usually sufficient for small projects. This highlights one of RCS's shortcomings: It does not make it easy to work with projects that have multiple working directories. Again, this is a reason why many people prefer CVS.
