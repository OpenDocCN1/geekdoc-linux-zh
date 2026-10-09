
### encapsulation
See *tunneling* on page 1278.

### environment
See *calling environment* on page 1241.

### environment variable (shell)
A variable that was in the environment the shell was called with or a variable that has been marked for export via the environment. An environment variable is available to children of the shell; also called a global variable. As explained on page 357, you can use the `export` builtin; the `-x` option to the `declare` builtin, to mark a variable for export via the environment.

### EOF
End of file.

### EPROM
Erasable programmable readonly memory. A `PROM` (page 1267) that can be written to by applying a higher than normal voltage.

### escape
See *quote* on page 1268.

### Ethernet
A type of `LAN` (page 1257) capable of transfer rates as high as 1,000 megabits per second. Refer to “Ethernet” on page 284.

### Ethernet address
See *MAC address* on page 1259.

### event
An occurrence, or happening, of significance to a task or program—for example, the completion of an asynchronous input/output operation, such as a keystroke or mouse click.

### exabyte
$2^{60}$ bytes or about $10^{18}$ bytes. See also *large number* (page 1257).

### exit status
The status returned by a process; either successful (usually 0) or unsuccessful (usually 1).

### exploit
A security hole or an instance of taking advantage of a security hole.

### expression
See *logical expression* (page 1259) and *arithmetic expression* (page 1237).

### extranet
A network extension for a subset of users (such as students at a particular school or engineers working for the same company). An extranet limits access to private information even though it travels on the public Internet.

### failsafe session
A session that allows you to log in on a minimal desktop in case your standard login does not work well enough to allow you to log in to fix a login problem.

### FDDI
Fiber Distributed Data Interface. A type of `LAN` (page 1257) designed to transport data at the rate of 100 million bits per second over fiberoptic cable.

### file
A collection of related information referred to with a *filename* and frequently stored on a disk. Text files typically contain memes, reports, messages, program source code, lists, or manuscripts. Binary or executable files contain utilities or programs that you can run. Refer to “Ordinary Files and Directory Files” on page 177.

### filename
The name of a file. A filename refers to a file.

### filename completion
Automatic completion of a filename after you specify a unique prefix.

### filename extension
The part of a filename following a period.

### filename generation
What occurs when the shell expands ambiguous file references. See *ambiguous file reference* on page 1236.

### filesystem
A *data structure* (page 1245) that usually resides on part of a disk. All Linux systems have a root filesystem, and many have other filesystems. Each filesystem is composed of some number of blocks, depending on the size of the disk partition that has been assigned to the filesystem. Each filesystem has a control block, named the superblock, that contains information about the filesystem. The other blocks in a filesystem are inodes, which contain control information about individual files, and data blocks, which contain the information in the files.

### filling
A variant of maximizing in which window edges are pushed out as far as they can go without overlapping another window.

### filter
A command that can take its input from standard input and send its output to standard output. A filter transforms the input stream of data and sends it to standard output. A pipeline symbol (|) usually connects a filter's input to standard output of one command, and a second pipeline symbol connects the filter's output to standard input of another command. The **grep** and **sort** utilities are commonly used as filters.

### firewall
A device for policy-based traffic management used to keep a network secure. A firewall can be implemented in a single router that filters out unwanted packets, or it can rely on a combination of routers, proxy servers, and other devices. Firewalls are widely used to give users access to the Internet in a secure fashion and to separate a company's public WWW server from its internal network. They are also employed to keep internal network segments more secure.

Recently the term has come to be defined more loosely to include a simple packet filter running on an endpoint machine.

See also *proxy server* on page 1268.

### firmware
Software built into a computer, often in ROM (page 1270). Might be used as part of the *bootstrap* (page 1240) procedure.

### focus, desktop
On a desktop, the window that is active. The window with the desktop focus receives the characters you type on the keyboard. Same as *active window* (page 1236).

### footer
The part of a format that goes at the bottom (or foot) of a page. Contrast with *header* (page 1252).

### foreground process
When you run a command in the foreground, the shell waits for the command to finish before giving you another prompt. You must wait for a foreground process to run to completion before you can give the shell another command. If you have job control, you can move background processes to the foreground, and vice versa. See *job control* on page 1256. Contrast with *background process* (page 1238).

### fork
To create a process. When one process creates another process, it forks a process. Also *spawn*.

### FQDN
Fully qualified domain name. The full name of a system, consisting of its hostname and its domain name, including the top-level domain. Technically the name that **gethostbyname(2)** returns for the host named by **gethostname(2)**. For example, speedy is a hostname and **speedy.example.com** is an FQDN. An FQDN is sufficient to determine a unique Internet address for a machine on the Internet.

### frame
A data link layer packet that contains, in addition to data, the header and trailer information required by the physical medium. Network layer packets are encapsulated to become frames. See also *datagram* (page 1246) and *packet* (page 1265).

### free list
In a filesystem, the list of blocks that are available for use. Information about the free list is kept in the superblock of the filesystem.

### free space
The portion of a hard disk that is not within a partition. A new hard disk has no partitions and contains all free space.

### full duplex
The ability to receive and transmit data simultaneously. A *network switch* (page 1263) is typically a full-duplex device. Contrast with *half-duplex* (page 1252).

### fully qualified domain name
See *FQDN*.

### function
See *shell function* on page 1272.

### gateway
A generic term for a computer or a special device connected to more than one dissimilar type of network to pass data between them. Unlike a router, a gateway often must convert the information into a different format before passing it on. The historical usage of gateway to designate a router is deprecated.

### GCOS
See *GECOS*.

### GECOS
General Electric Comprehensive Operating System. For historical reasons, the user information field in the */etc/passwd* file is called the GECOS field. Also *GCOS*.

### gibibyte
Giga binary byte. A unit of storage equal to $2^{30}$ bytes = 1,073,741,824 bytes = 1024 *mebibytes* (page 1260). Abbreviated as GiB. Contrast with *gigabyte*.

### gigabyte
A unit of storage equal to $10^9$ bytes. Sometimes used in place of *gibibyte*. Abbreviated as GB. See also *large number* on page 1257.

### global variable (shell)
See *environment variable (shell)* on page 1249.

### glyph
A symbol that communicates a specific piece of information nonverbally. A *smiley* (page 1273) is a glyph.

### GMT
Greenwich Mean Time. See *UTC* on page 1279.

### graphical display
A bitmapped monitor that can display graphical images. Contrast with *ASCII terminal* (page 1237).

### graphical user interface
See *GUI*.

### group (of users)
A collection of users. Groups are used as a basis for determining file access permissions. If you are not the owner of a file and you belong to the group the file is assigned to, you are subject to the group access permissions for the file. A user can simultaneously belong to several groups.
