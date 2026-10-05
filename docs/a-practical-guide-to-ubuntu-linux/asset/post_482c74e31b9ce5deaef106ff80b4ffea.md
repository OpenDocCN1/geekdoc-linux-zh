
# GLOSSARY 1139

# BSD

See Berkeley UNIX on page 1137.

# buffer

An area of memory that stores data until it can be used. When you write information to a file on a disk, Linux stores the information in a disk buffer until there is enough to write to the disk or until the disk is ready to receive the information.

# bug

An unwanted and unintended program property, especially one that causes the program to malfunction.

# builtin (command)

A command that is built into a shell. Each of the three major shells—the Bourne Again, Tc, and Z Shells—has its set of binaries. Refer to “Builtins” on page 261.

# byte

A component in the data hierarchy, much larger than a bit and smaller than a word; now most often eight bits and the smallest addressable unit of storage. A byte typically has one character.

# C programming language

A modern language that has high-level features for efficient, modular programming as well as lower-level features to make it suitable for systems programming language. It is machine independent so that carefully written C programs can be easily transported to different machines. Most of the Linux operating system is written in C, and Linux provides an ideal environment for programming C.

# C Shell

the C Shell command processor was developed by Bill Joy for BSD UNIX. It was named for the C programming language because its programming constructs are similar to those of C. *See* on page 1171.

# cable modem

A type of modem that allows you to access the Internet by using your cable television connection.

# cache

Holding recently accessed data, a small, fast memory designed to speed up subsequent access to the same data. Most often applied to processor-memory access but used for a local copy of data accessible over a network, from a hard disk, and so on.

# calling environment

A list of variables and values that is made available to a called program. Refer to “Executing a Command” on page 330.

# cascading stylesheet

See CSS on page 1143.

# cascading windows

An arrangement of windows such that they overlap, generally with at least part of the title bar visible. Opposite of *tied windows* (page 1177).

# case sensitive

Able to distinguish between uppercase and lowercase characters. Unless you set the ignorecase parameter, yum performs case-sensitive searches. The *grep* utility performs case-sensitive searches unless you use the -i option.

# catenate

To join sequentially, or to end. The Linux *cat* utility concatenates files: It displays them one after the other. Also *concatenate*.

The technique used by a boot loader to load unsupported operating systems. Used for loading such operating systems as DOS or Windows, it works by loading another boot loader.

A program, utility, or interface that works only with ASCII (page 1135) characters. This set of characters includes some simple graphics, as lines and corners, and can display colored characters. It cannot display true graphics. Contrast with GUI (page 1150).

A terminal that displays only characters and very limited graphics. See character-based.

In a regular expression, a group of characters that defines which characters can occupy a single character position. A character-class definition is usually rounded by square brackets. The class defined by [abc] represents a character position that can be occupied by a, b, c, or r. See list operator.

In POSIX, used to refer to sets of characters with a common characteristic, or by the notation [:class]; for example, [:upper]: denotes the set of uppercase letters.

This book uses the term class as explained under "Brackets" on page 101.

A terminal, printer, or modem. A character device stores or displays characters one at a time. A character device is represented by a character device (character special) file. Contrast with block device (page 1137).

A GUI widget, usually the outline of a square box with an adjacent caption, that a user can click to display or remove a tick (page 1177). When the box holds a tick, the option described by the caption is on or true. Also tick box.

A computed value that depends on the contents of a block or data and is stored or with the data to detect corruption of the data. The receiving system recomputes the checksum on the received data and compares this value with the one it sent. If the two values are the same, the receiver has some confidence that the data was correctly received.

The checksum may be 8, 16, or 32 bits, or some other size. It is computed by summing the bytes and words of the data, ignoring overflow. The checksum may be negated so that the total of the data plus the checksum is zero.

A process that is created by another process, the parent process. Every process is a child except the first, which is started when Linux begins. When you run a command from the shell, the shell spawns a child to run the command. See process on page 1166.

Classless Inter-Domain Routing. A scheme that allocates blocks of Internet addresses in a way that allows summarization into a smaller number of routing table entries. A CIDR block is a block of Internet addresses assigned to an ISP. Refer to "CIDR: Classless Inter-Domain Routing" on page 386.

chain loading
character-based
character class
character device
checksum
child process
CIDR

GLOSSARY 1141

Common File System. A protocol based on SMB (page 1172). CIFS runs on top of TCP/IP, uses DNS, and is optimized to support slower dial-up connections. SMB and CIFS are used interchangeably.

Encapsulation (page 1147). This protocol (page 1166) is lightweight and simple, and works over dynamic addresses, NAT (page 1161), and SOCKS (page 1173) proxies (page 1166).

cipher (cipher) A cryptographic system that uses a key to transpose/substitute characters within a message, the key itself, or the message.

ciphertext That is encrypted. Contrast with plaintext (page 1165). See also “Encryption” page 1110.

Classless Inter-Domain Routing See CIDR on page 1140.

cleartext Text is not encrypted. Also plaintext. Contrast with ciphertext. See also “Encryption” page 1110.

CLI Command-line interface. See also character-based (page 1140).

client A computer or program that requests one or more services from a server.

codec Coder/decoder or compressor. A hardware and/ software that codes and decodes data. MPEG is a popular codec for video device.

color depth The number of bits used to generate a pixel—usually 8, 16, or 32. The number of colors that can be generated is 2 raised to the color-depth power. Thus a 24-bit video adapter can generate about 16.7 million colors.

color quality See color depth.

combo box A combination of a drop-list (page 1146) and text box (page 1176). You can enter text in a combo box. Or, you can click a combo box, cause it to expand and display a list of selections for you to choose from.

command What you give the shell in response to a prompt. When you give the shell command, it executes a utility, another program, or a shell script. Utilities are often referred to as commands. When you are using an interactive interface, such as vim or mail, you use commands that are appropriate to that utility.

command line A line containing instructions and arguments that executes a command. This term usually refers to a line that you enter in response to a shell prompt on a character-based terminal or terminal emulator (page 125).

command substitution Replacing a command with its output. The shells perform command substitution when you enclose a command between $( ) or between a pair of backticks (``), also called grave accents.

1142 GLOSSARY

component architecture** A notion in object-oriented programming where "components" of a program are completely generic. Instead of having a specialized set of methods and fields, they have generic methods through which the component can advertise the functionality it supports to the system to which it is loaded. This strategy enables dynamic loading of objects. JavaBeans is an example of a component architecture.

**concatenate** See caten on page 1139.

**condition code** See exit status on page 1147.

**connection-oriented protocol** A type of transport layer data communication service that allows a host to guarantee that data in a continuous stream to another host. The transport service guarantees all data will be delivered to the other end in the same order as sent and without duplication. Communication proceeds through well-defined phases: connection establishment, data transfer, and connection release. The most common example is TCP (page 1176).

Also called connection-based protocol and stream-oriented protocol. Contrast with connectionless protocol and datagram (page 1144).

**connectionless protocol** The data communication method in which communication occurs between hosts with no previous setup. Packets between two hosts may take different routes. There is no guarantee that packets will arrive as transmitted or that they will arrive at the destination at all. UDP (page 1178) is a connectionless protocol. Also called packet switching. Contrast with circuit switching and connection-oriented protocol.

**console** The main system, usually directly connected to the computer and the one that receives system error messages. Also system console and console terminal.

**console terminal** See console.

**control character** A character that is not a graphic character, such as a letter, number, or punctuation mark. Such characters are called control characters because they frequently act to control a peripheral device. RETURN and FEED are control characters that control a terminal or printer.

The word CONTROL is shown in this book in THIS F because it is a key that appears on most terminal keyboards. Control characters are represented by ASCII codes less than 32 (decimal). Some nonprinting character on page 1162.

**control structure** A statement to change the order of execution of commands in a shell script or other program. Each shell provides control structures (for example, if and while) as well as other commands that alter the order of execution (for example, exec). Also control flow commands.

**cookie** Data stored on a client system by a server. The client system browser sends the cookie back to the server each time it accesses that server. For example, a catalog shopping service may store a cookie on your system when you place your first
