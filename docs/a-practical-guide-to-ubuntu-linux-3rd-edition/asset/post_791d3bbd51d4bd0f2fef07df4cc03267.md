
## Reference to `stty` and `setserial`

a sane state after it has been corrupted. In this sense, it is similar to an *stty sane* command.

-   *setserial*
    Gets and sets serial port information. When run with *root* privileges, this utility can configure a serial port. The following command sets the input address of /dev/ttyS0 to 0x100, the interrupt (IRQ) to 5, and the baud rate to 115,000 baud:

    ```bash
    $ sudo setserial /dev/ttyS0 port 0x100 irq 5 spd_vhi
    ```

    You can also check the configuration of a serial port with *setserial*:

    ```bash
    $ sudo setserial /dev/ttyS0
    /dev/ttyS0, UART: 16550A, Port: 0x0100, IRQ: 5, Flags: spd_vhi
    ```

    Normally the system calls *setserial* as it is booting if a serial port needs custom configuration. This utility is part of the *setserial* package.

-   *stat*
    Displays information about a file or filesystem. Giving the *-f* (filesystem) option followed by the mount point for a filesystem displays information about the filesystem, including the maximum number of characters allowed in a filename (*NameLen* in the following example). See the *stat* man page for more information.

    ```bash
    $ stat -f /dev/sda
    File: "/dev/sda"
    ID: 0           NameLen: 255     Type: tmpfs
    Block size: 4096      Fundamental Block size: 4096
    Blocks: Total: 127271  Free: 127207   Available: 127207
    Inodes: Total: 127271  Free: 126600
    ```

-   *umask*
    A shell builtin that specifies the mask the system uses to set up access permissions when you create a file. A *umask* command has the following format:

    ```bash
    umask [mask]
    ```

    where *mask* is a three-digit octal number or a symbolic value such as you would use with *chmod* (page 216). The *mask* specifies the permissions that are *not* allowed. When *mask* is an octal number, the digits correspond to the permissions for the owner of the file, members of the group the file is associated with, and everyone else. Because *mask* specifies the permissions that are *not* allowed, the system subtracts each of the three digits from 7 when you create a file. The result is three octal numbers that specify the access permissions for the file (the numbers you would use with *chmod*). A *mask* that you specify using symbolic values specifies the permissions that *are* allowed.

    Most utilities and applications do not attempt to create files with execute permissions, regardless of the value of *mask*; they assume you do not want an executable file. As a result, when a utility or application (such as *touch*) creates a file, the system subtracts each of the three digits in *mask* from 6. An exception is *mkdir*, which assumes you want the execute (access in the case of a directory) bit set.

    The following commands set the file-creation mask and display the mask and its effect when you create a file and a directory. The mask of 022, when subtracted from 666 or 777, gives permissions of 644 (*rw-r--r--*) for a file and 755 (*rwxr-xr-x*) for a directory.

    ```bash
    $ umask 022
    $ umask
    0022
    $ touch afile
    $ mkdir adirectory
    $ ls -ld afile adirectory
    drwxr-xr-x 2 sam sam 4096 2010-05-02 23:57 adirectory
    -rw-r--r-- 1 sam sam 0 2010-05-02 23:57 afile
    ```

    The next example sets the same mask using symbolic values. The -S option displays the mask symbolically:

    ```bash
    $ umask u=rwx,g=rx,o=rx
    $ umask
    0022
    $ umask -S
    u=rwx,g=rx,o=rx
    ```

-   *uname*
    Displays information about the system. Without arguments, this utility displays the name of the operating system (Linux). With the -a (all) option, it displays the operating system name, hostname, version number and release date of the operating system, and type of hardware you are using:

    ```bash
    $ uname -a
    Linux lync1 2.6.32-22-generic #33-Ubuntu SMP Wed Apr 28 13:27:30 UTC 2010 i686 GNU/Linux
    ```

## Setting Up a Server

This section discusses issues you may need to address when setting up a server: how to write configuration files; how to specify hosts and subnets; how to use portmap, rpcinfo, and TCP wrappers (hosts.allow and hosts.deny); and how to set up a chroot jail. Chapters 14 and 18-2.6 cover setting up specific servers; Chapter 17 discusses setting up a LAN.

### Standard Rules in Configuration Files

Most configuration files, which are typically named *.conf, rely on the following conventions:

-   Blank lines are ignored.
-   A # anywhere on a line starts a comment that continues to the end of the line. Comments are ignored.
-   When a name contains a SPACE, you must quote the SPACE by preceding it with a backslash (\) or by enclosing the entire name within single or double quotation marks.
-   To make long lines easier to read and edit, you can break them into several shorter lines. To break a line, insert a backslash (\) immediately followed by a NEWLINE (press RETURN in a text editor). When you insert the NEWLINE before or after a SPACE, you can indent the following line to make it easier to read. Do not break lines in this manner while editing on a Windows machine, as the NEWLINES may not be properly escaped (Windows uses a RETURN-LINEFEED combination to end lines).

Configuration files that do not follow these conventions are noted in the text.

### Specifying Clients

Table 11-2 shows some common ways to specify a host or a subnet. Most of the time you can specify multiple hosts or subnets by separating their specifications with SPACES.

#### Table 11-2 Specifying a client

| Client name pattern | Matches |
| :--- | :--- |
| n.n.n.n | One IP address. |
| name | One hostname, either local or remote. |
| Name that starts with . | Matches a hostname that ends with the specified string. For example, .example.com matches the systems named kudos.example.com and speedy.example.com, among others. |
| IP address that ends with . | Matches a host address that starts with the specified numbers. For example, 192.168.0. matches 192.168.0.0–192.168.0.255. If you omit the trailing period, this format does not work. |
| n.n.n.n/m.n.m.m or n.n.n.n/mm | An IP address and subnet mask specifying a subnet. |
| Starts with / | An absolute pathname of a file containing one or more names or addresses as specified in this table. |
| **Wildcard** | **Matches** |
| * and ? | Matches one (?) or more (*) characters in a simple hostname or IP address. These wildcards do not match periods in a domain name. |
| ALL | Always matches. |
| LOCAL | Matches any hostname that does not contain a period. |
| **Operator** | **Matches** |
| EXCEPT | Matches anything in the preceding list that is not in the following list. For example, a b c d EXCEPT c matches a, b, and d. Thus you could use 192.168. EXCEPT 192.168.0.1 to match all IP addresses that start with 192.168, except 192.168.0.1. |

Examples. Each of the following examples specifies one or more systems:

-   **10.10.** Matches all systems with IP addresses that start with **10.10.**
-   **.ubunto.com** Matches all named hosts on the Ubuntu network
-   **localhost** Matches the local system
-   **127.0.0.1** The loopback address; always resolves to **localhost**
-   **192.168.*.1** Could match all routers on a network of /24 subnets (discussed in the next section)

### Specifying a Subnet

When you set up a server, you frequently need to specify which clients are allowed to connect to it. Sometimes it is convenient to specify a range of IP addresses, called a subnet. The discussion on page 385 explains what a subnet is and how to use a subnet mask to specify a subnet. Usually you can specify a subnet as

`n.n.n.n/m.m.m.m`

or

`n.n.n.n/maskbits`

where *n.n.n.n* is the base IP address and the subnet is represented by *m.m.m.m* (the subnet mask) or *maskbits* (the number of bits used for the subnet mask). For example, *192.168.0.1/255.255.255.0* represents the same subnet as *192.168.0.1/24*. In binary, decimal *255.255.255.0* is represented by 24 ones followed by 8 zeros. The /24 is shorthand for a subnet mask with 24 ones. Each line in Table 11-3 presents two notations for the same subnet, followed by the range of IP addresses that the subnet includes.

#### Table 11-3 Different ways to represent a subnet

| Bits | Mask | Range |
| :--- | :--- | :--- |
| 10.0.0.0/8 | 10.0.0.0/255.0.0.0 | 10.0.0.0–10.255.255.255 |
| 172.16.0.0/12 | 172.16.0.0/255.240.0.0 | 172.16.0.0–172.31.255.255 |
| 192.168.0.0/16 | 192.168.0.0/255.255.0.0 | 192.168.0.0–192.168.255.255 |

### rpcinfo: Displays Information About portmap

The *rpcinfo* utility displays information about programs registered with *portmap* and makes RPC calls to programs to see if they are alive. For more information on *portmap*, refer to “RPC Network Services” on page 406. The *rpcinfo* utility takes the following options and arguments:

```bash
rpcinfo -p [host]
rpcinfo [-n port] [-u | -t] host program [version]
rpcinfo -b |-d program version
```
