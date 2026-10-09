**standard output**
A file to which a program can send output. Unless you instruct the shell otherwise, it directs this output to the screen (that is, to the device file that represents the screen).

**startup file**
A file that the login shell runs when you log in. The Bourne Again and Z Shells run .profile, and the TC Shell runs .login. The TC Shell also runs .cshrc whenever a new TC Shell or a subshell is invoked. The Z Shell runs an analogous file whose name is identified by the ENV variable.

**status line**
The bottom (usually the twenty-fourth) line of the terminal. The vim editor uses the status line to display information about what is happening during an editing session.

**sticky bit**
Originally, an access permission bit that caused an executable program to remain on the swap area of the disk. Today, Linux kernels do not use the sticky bit for this purpose but rather use it to control who can remove files from a directory. In this new capacity, the sticky bit is called the *restricted deletion flag*. If this bit is set on a directory, a file in the directory can be removed or renamed only by a user who is working with root privileges or by a user who has write permission for the directory *and* who owns the file or the directory.

**streaming tape**
A tape that moves at a constant speed past the read/write heads rather than speeding up and slowing down, which can slow the process of writing to or reading from the tape. A proper blocking factor helps ensure that the tape device will be kept streaming.

**streams**
See *connection-oriented protocol* on page 1244.

**string**
A sequence of characters.

**stylesheet**
See *CSS* on page 1245.

**subdirectory**
A directory that is located within another directory. Every directory except the root directory is a subdirectory.

**subnet**
Subnetwork. A portion of a network, which might be a physically independent network segment, that shares a network address with other portions of the network and is distinguished by a subnet number. A subnet is to a network as a network is to an internet.

**subnet address**
The subnet portion of an IP address. In a subnetted network, the host portion of an IP address is split into a subnet portion and a host portion using a network mask (also subnet mask). See also *subnet number*.

**subnet mask**
See *network mask* on page 1263.

**subnet number**
The subnet portion of an IP address. In a subnetted network, the host portion of an IP address is split into a subnet portion and a host portion using a *network mask*. Also *subnet mask*. See also *subnet address*.

**subpixel hinting**
Similar to *anti-aliasing* (page 1236) but takes advantage of colors to do the anti-aliasing. Particularly useful on LCD screens.

**subroutine**
See *procedure* on page 1267.

**subshell**
A shell that is forked as a duplicate of its parent shell. When you run an executable file that contains a shell script by using its filename on the command line, the shell forks a subshell to run the script. Also, commands surrounded with parentheses are run in a subshell.