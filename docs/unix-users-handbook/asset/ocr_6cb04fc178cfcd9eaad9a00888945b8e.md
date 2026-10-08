comments
ftp> bye  |  Exit ftp
Goodbye.
$  |

In this example, both systems are running UNIX; however, the commands you issue through **FTP** are operating-system-independent. The `cd` for change directory and `get` commands used above work for any operating system on which **FTP** is running. If you become familiar with just a few **FTP** commands, you may find that transferring information in a heterogeneous networking environment is not difficult.

Because **FTP** is so widely used, I describe some of the more commonly used **FTP** commands.

**ftp** - File Transfer Protocol for copying files across a network.

The following list includes some commonly used `ftp` commands. This list is not complete.

+   *   `ascii` Set the type of file transferred to ASCII. This means that you will be transferring an ASCII file from one system to another. This is the default, so you don't have to set it.
    *   Example: `ascii`