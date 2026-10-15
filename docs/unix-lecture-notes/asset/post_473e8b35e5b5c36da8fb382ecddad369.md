
header file, that refer to the standard input and standard output device respectively. By default, the keyboard and display of the associated terminal are the standard input and output devices respectively.

## Listing 1.1: C program using simple I/O model.

```
#include <stdio.h>
/* copy from stdin to stdout */
int main()
{
    int c;
    while ( ( c = getchar( ) ) != EOF )
        putchar(c);
    return 0;
}
```

## Listing 1.2: Simple C++ program using simple I/O model.

```
#include <iostream>
using namespace std;
/* copy from stdin to stdout using C++ */
int main()
{
    char c;
    while ( ( c = cin.get( ) ) && !cin.eof() )
        cout.put(c);
    return 0;
}
```

These programs give us the illusion that they are directly connected to the keyboard and the display device via C library functions getchar() and putchar() and the C++ iostream member functions get() and put(). Either of them can be run on a single-user desktop computer or on a multi-user, time-shared workstation in a terminal window, and the results will be the same. If you build and run them as console applications in Windows, they will have the same behavior as if you built and ran them from the command-line in a UNIX system.

On a personal computer running in single-user mode, this illusion is not far from reality in the sense that the keyboard is indirectly connected to the input stream of the program, and the monitor is indirectly connected to the output stream. This is not the case in a multi-user system.

In a multi-user operating system, several users may be logged in simultaneously, and programs belonging to different users might be running at the same time, each receiving input from a different keyboard and sending output to a different display. For example, on a UNIX computer on a network into which you can login, many people may be connected to a single computer via a network program such as SSH, and several of them will be able to run the above program on the same computer at the same time, sending their output to different terminal windows on physically different computers, and each will see the same output as if they had run the program on a single-user machine.

As depicted in Figure 1.2, UNIX ensures, in a remarkably elegant manner, that each user's processes have a logical connection to their keyboard and their display. (The process concept will be explained shortly.) Programs that use the model of I/O described above do not have to be concerned with the complexities of connecting to monitors and keyboards, because the operating system hides that complexity, presenting a simplified interface for dealing with I/O. To understand how the operating system achieves this, one must first understand several cornerstone concepts of the UNIX operating system: files, processes, users and groups, privileges and protections, and environments.

![](img/edd55012c780b4e999320d08ab27959e_3_0.png)

Figure 1.2: Connecting multiple users to a UNIX system.

## 1.3 Cornerstones of UNIX

From its beginning, UNIX was designed around a small set of clever ideas, as Ritchie and Thompson [2] put it:

> "The success of UNIX lies not so much in new inventions but rather in the full exploitation of a carefully selected set of fertile ideas, and especially in showing that they can be keys to the implementation of a small yet powerful operating system."

Those "fertile ideas" included the design of its file system, its process concept, the concept of privileged and unprivileged programs, the concepts of user and groups, a programmable shell, environments, and device independent input and output. In this section we describe each of these briefly.

```
{
    printf("I am the process with process-id %d\n", getpid());
    return 0;
}
```

### 1.3.3 Users and Groups

Part of the security of UNIX rests on the principle that every user of the system must be authenticated. Authentication is a form of security clearance, like passing through a metal detector at an airport.

In UNIX, a user is a person⁷ who is authorized to use the system. The only way to use a UNIX system is to log into it⁸. UNIX maintains a list of names of users who are allowed to login⁹. These names are called user-names. Associated with each user-name is a unique non-negative number called the user-id, or uid for short. Each user also has an associated password. UNIX uses the user-name/password pair to authenticate a user attempting to login. If that pair is not in its list, the user is rejected. Passwords are stored in an encrypted form in the system’s files.

A group is a set of users. Just as each user has a user-id, each group has unique integer group-id, or gid for short. UNIX uses groups to provide a form of resource sharing. For example, a file can be associated with a group, and all users in that group would have the same access rights to that file. Since a program is just an executable file, the same is true of programs; an executable program can be associated with a group so that all members of that group will have the same right to run that program. Every user belongs to at least one group, called the primary group of that user. The id command can be used to print the user’s user-id and user-name, and the group-id and group-name of all groups to which the user belongs. The groups command prints the list of groups to which the user belongs.

In UNIX, there is a distinguished user called the superuser, whose user-name is root, one of a few predefined user-names in all UNIX systems. The superuser has the ability to do things that ordinary users cannot do, such as changing a person’s user-name or modifying the operating system’s configuration. Being able to login as root in UNIX confers absolute power to a person over that system. For this reason, all UNIX systems record every attempt to login as root, so that the system administrator can monitor and catch break-in attempts.

Every process has an associated (real) user-id and, as we will see later, an effective user-id that might be different from the real user-id. In simplest case, when a user starts up a program, the resulting process has that user’s uid as both its real and effective uid. The privileges of the process are the same as those of the user¹⁰. When the superuser (root) runs a process, that process runs

⁷A user may not be an actual person. It can also be an abstraction of a person. For example, mail, lp, and ftp are each users in a UNIX system, but they are actually programs.

⁸To "login" to a system is to "log into" it. Remember that logging means recording something in a logbook, as a sea captain does. The term "login" conveys the idea that the act is being recorded in a logbook. In UNIX, logins are recorded in a special file that acts like a logbook.

⁹We take this word for granted. We use "login" as a single word only because it has become a single word on millions of "login screens" around the world. To login, as a verb, really means "to log into" something; it requires an indirect object.

¹⁰To be precise, the privileges are those of user with the process’s effective user-id.
