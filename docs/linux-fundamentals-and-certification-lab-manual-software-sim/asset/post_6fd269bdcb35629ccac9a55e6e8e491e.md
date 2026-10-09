
## netstat

### Routing Table

| Destination | Gateway | Genmask | Flags | MSS | Window | irtt | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 130.160.46.0 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth0 |
| 130.160.46.0 | * | 255.255.255.0 | U | 0 | 0 | 0 | eth1 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | 0 | lo |
| default | 130.160.46.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |

### Group Memberships

| Interface | RefCnt | Group |
| :--- | :--- | :--- |
| lo | 1 | all-systems.mcast.net |
| eth0 | 1 | all-systems.mcast.net |
| eth1 | 1 | all-systems.mcast.net |

### Interface Table

| Iface | MTU | Met | RX-OK | RX-ERR | RX-DRP | RX-OVR | TX-OK | TX-ERR | TX-DRP | TX-OVR | Flg |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| eth0 | 1500 | 0 | 21535333 | 0 | 0 | 0 | 43303405 | 0 | 0 | 0 | EMRU |
| eth1 | 1500 | 0 | 15937127 | 0 | 0 | 0 | 16143 | 0 | 0 | 0 | BMRU |
| lo | 16436 | 0 | 1034128 | 0 | 0 | 0 | 1034128 | 0 | 0 | 0 | LRU |

### Masquerade

netstat: no support for `ip_masquerade` on this system.

One of the more interesting netstat displays is the no option one. The listing below shows a sample listing. Some of the information listed is the users that are connected and the ports they are using. For example, rbrown is connected to the server Styx on port 1521. (1521 is used by the Oracle database.) The connection state is ESTABLISHED, which means that the connection is completed and data can flow between the client (rbrown) and the server (Styx). Common states for connections are:

- **LISTEN**: The socket is listening for incoming connections. (Only displayed if the -a or -l option is used.)
- **ESTABLISHED**: The socket has an established connection.
- **SYN_SENT**: A socket is actively attempting to establish a connection.
- **SYN_RECV**: A connection request has been received from the network.
- **FIN_WAIT1**: The socket is closed, and the connection is shutting down.
- **FIN_WAIT2**: The connection is closed and the socket is waiting for a shutdown from the remote end.
- **TIME_WAIT**: The socket is waiting after close to handle packets still in the network.
- **CLOSED**: The socket is not being used.
- **CLOSE_WAIT**: The remote end has shut down and is waiting for the socket to close.

The netstat command is useful for tracking what is happening with network traffic. If you are having problems with network connections, they can be diagnosed with netstat. For example, a lot of CLOSE_WAIT connections may indicate that a port has become unresponsive and its process may need to be restarted.

### Active Internet connections (w/o servers)

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | Styx:1521 | Styx:32772 | ESTABLISHED |
| tcp | 0 | 0 | Styx:32772 | Styx:1521 | ESTABLISHED |
| tcp | 0 | 0 | Styx:ssh | jsmith.linuxplus.com:4268 | ESTABLISHED |
| tcp | 0 | 0 | Styx:1521 | rbrown.linuxplus.com:2226 | ESTABLISHED |
| tcp | 0 | 0 | Styx:ssh | jsmith.linuxplus.com:4801 | ESTABLISHED |

### Active Unix domain sockets (w/o servers)

| Proto | RefCnt | Flags | Type | State | I-Node | Path |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| unix | 12 | [ ] | DGRAM | | 1401 | /dev/log |
| unix | 2 | [ ] | DGRAM | | 2449506 | |
| unix | 2 | [ ] | DGRAM | | 2449492 | |
| unix | 3 | [ ] | STREAM | CONNECTED | 69589 | /tmp/.X11-unix/X0 |
| unix | 3 | [ ] | STREAM | CONNECTED | 69588 | |
| unix | 3 | [ ] | STREAM | CONNECTED | 69585 | /tmp/.X11-unix/X0 |
| unix | 3 | [ ] | STREAM | CONNECTED | 69584 | |
| unix | 3 | [ ] | STREAM | CONNECTED | 69569 | /tmp/.font-unix/fs7100 |
| unix | 3 | [ ] | STREAM | CONNECTED | 69568 | |
| unix | 3 | [ ] | STREAM | CONNECTED | 69571 | /tmp/.X11-unix/X0 |
| unix | 3 | [ ] | STREAM | CONNECTED | 69467 | |
| unix | 2 | [ ] | DGRAM | | 67537 | |
| unix | 3 | [ ] | STREAM | CONNECTED | 44683 | /var/tmp.oracle/s#1530.1 |
| unix | 3 | [ ] | STREAM | CONNECTED | 44682 | |
| unix | 2 | [ ] | DGRAM | | 17139 | |
| unix | 2 | [ ] | DGRAM | | 1956 | |
| unix | 2 | [ ] | DGRAM | | 1806 | |
| unix | 2 | [ ] | DGRAM | | 1732 | |
| unix | 2 | [ ] | DGRAM | | 1697 | |
| unix | 2 | [ ] | DGRAM | | 1462 | |
| unix | 2 | [ ] | DGRAM | | 1409 | |

## FINDING FILES

Even the best organized Linux user will occasionally displace a file. Finding files could take hours without utilities to help. The Linux commands most often used for finding files are whereis, locate, and find.

- **whereis**: The whereis command locates the source, binary, and manuals for a specified file. It uses a hard coded path to find files, so it may not find every file you are looking for. For example, if you have a user-created script in your home directory, the file will not be found with the whereis command. However, if you move the file to the /bin directory and then execute the whereis command, it will be found.

The whereis syntax is `whereis [-sbmu] [-SBM <directory> -f <filename>]`, where `-sbmu` is source, binary, manual, or unusual and `-SBM` is a change or limit to the directories to be searched. To find the startx command use the following command:

```bash
# whereis startx
startx: /usr/X11R6/bin/startx /usr/bin/X11/startx
#
```

- **which**: The which command looks through the directories listed in the PATH environment variable for the command requested. For example, if whereis is used to find startx, the which command will list which program will be executed if the command is run.

```bash
# whereis startx
startx: /usr/X11R6/bin/startx /usr/bin/X11/startx
# which startx
/usr/X11R6/bin/startx
#
```

In the previous command sequence, the whereis command finds two places where startx resides and the which command lists the one that will be executed if the startx command is executed.

- **locate**: The locate command uses a database of files to find files on the system. If the database is up to date, then locate works well. By default, the **updatedb** command is run in a cron job every night.

The slocate command has replaced locate on many Linux distributions. slocate works the same as locate and uses the permissions and ownership values to determine if the user of the command has access to the files.

The locate command works much faster than the find command. The find command will search through the file system until it finds the file requested, whereas locate searches its database.

locate returns all entries with the search value in it. For example, if ls is searched for, any command with the letters ls within it is listed, resulting in hundreds of lines of output.

```bash
# locate startx
/usr/X11R6/bin/startx
/usr/X11R6/man/man1/startx.1x.gz
#
```

- **find**: The find command is probably the most versatile of file location commands. find lets you write decision-making logic, specify filters, and run commands on the contents of entire directory trees.

A basic use of find is to locate a file by its name. The option to find a name is **-name** or **-iname**. The basic syntax for finding a file by name is `find <starting_directory> -name <filename>`, where starting_directory is the top of a directory tree and filename is the filename to be found. For example, to find the program X in any directory from the root of the file system, use the following command:

```bash
# find / -name X
/etc/X11/X
/usr/lib/python2.2/site-packages/pynche/X
/usr/share/terminfo/X
/usr/X11R6/bin/X
#
```

The find command is constrained by file and directory access permissions. For example, if you are not the root user and you try to search the /root directory, you will get a **Permission denied** error.

```bash
$ find /root -name if_test
find: /root: Permission denied
$
```

Using find from the root ( / ) directory can display hundreds of Permission denied messages, making it easy to miss the entry you want to find. To avoid this problem, you can redirect error messages to the bit bucket ( /dev/null). The 2> in the command causes error messages to be sent to the stderr stream. Output sent to /dev/null disappears.

```bash
$ find / -name startx
find: /lost+found: Permission denied
find: /boot/lost+found: Permission denied
find: /proc/1/fd: Permission denied
find: /proc/2/fd: Permission denied
find: /proc/3/fd: Permission denied
find: /proc/4/fd: Permission denied
find: /proc/5/fd: Permission denied
find: /proc/6/fd: Permission denied
find: /usr/share/ssl/Ca: Permission denied
/usr/X11R6/bin/startx
find: /home/dengle: Permission denied
find: /home/oracle: Permission denied
...
$ find / -name startx 2> /dev/null
/usr/X11R6/bin/startx
$ 
```

You can also find files if you know only part of the filename. For example, if you wanted to find all files with a portable network graphics (png) format in the /opt/oracle directory, you would use the following command.

```bash
# find /opt/oracle -name *png*
/opt/oracle/product/9.2.0/inventory/filemap/ultrashare/webapp/isearch_admin/images/png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png/across.png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png/vertical.png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png/oracle_small_red.png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png/iSearch.png
/opt/oracle/product/9.2.0/ultrashare/webapp/isearch_admin/images/png/oracle_isearch.png
# 
```

The single quotes around the `*png` are necessary. Certain symbols are used by the system for other purposes. Using the single quotes encapsulates the value to be found, and any value may be used within the quotes.

find can locate files by their characteristics. For example, to find files larger than 150 MB, use the following command:

```bash
# find / -size +150000000c
/proc/kcore
find: /proc/27321/fd/4: No such file or directory
/opt/oracle/product/9.2.0/assistants/obca/templates/Data_Warehouse.dfj
/opt/oracle/oradata/students/undotbs01.dbf
/opt/oracle/oradata/students/system01.dbf
/opt/oracle/oradata/students/CS457.dbf
/opt/oracle/oradata/students/CS457TEMP.dbf
/gzipfiles/lnx_920_disk1.cpio.gz
/gzipfiles/lnx_920_disk2.cpio.gz
# 
```

Several options are useful when locating files. Table 13-3 lists a few of these. Use the `man find` command for a more complete listing.
