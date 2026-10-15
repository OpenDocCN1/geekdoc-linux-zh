name and where and when I logged in. Try the command on your system to see what results you get.

In this example, my account name is taylor. The pts/2 is the current communication line I’m using to access the system, and you can see that I logged in at 10:11 using a regular communications socket. (The :0.0 is relevant under the X Window System, something we won’t cover for quite a while in this book.)

# Note

Unix is full of oddities that are based on historical precedent. One is tty or pty to describe a computer or terminal line. This comes from the earliest Unix systems, in which Digital Equipment Corporation teletypewriters were hooked up as interactive devices. The teletypewriters quickly received the nickname tty, and all these years later, when people wouldn’t dream of hooking up a teletypewriter, the line is still known as a tty (or pty, for “pseudo terminal”) line.

3. One of the most dramatic influences Unix systems have had on the computing community is the propensity for users to work together on a network, hooked up by telephone lines and modems (the predominant method until the middle to late 1980s) or by high-speed network connections to the Internet (a more common type of connection today). Regardless of the connection, however, you can see that each computer needs a unique identifier to distinguish it from others on the network. In the early days of Unix, systems had unique hostnames, but as hundreds of systems have grown into millions, this has proved to be an unworkable solution.

4. The alternative was what’s called a domain-based naming scheme, where systems are assigned unique names within specific subsets of the overall network. Here’s an example:

mentor.utech.edu

The computer I use is within the .edu domain (read the hostname and domain —mentor.utech.edu—from right to left), meaning that the computer is located at an educational institution. Then, within the educational institution subset of the network, utech is a unique descriptor, and, therefore, if other UTech universities existed, they couldn’t use the same top-level domain name. Finally, mentor is the name of the computer itself.

5. As with learning to read addresses on envelopes, learning to read domain names can unlock much information about a computer and its location. For example, lib.stanford.edu is the library computer at Stanford University, and cegate.infoworld.com tells you that the computer is at InfoWorld, a commercial computer site, and that its hostname is cegate. You’ll learn more about this later when you learn how to use electronic mail to communicate with people throughout the Internet.