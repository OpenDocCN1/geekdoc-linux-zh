
## NOTE

UNIX-style remote printing also functions on a trusted host model, but you can use a separate file, /etc/hosts.lpd, to provide a list of trusted print clients. Because you can separately authenticate print clients in this way, you minimize the risk; short of a bug or some additional misconfiguration, a cracker can't use printer access to do more than waste some of your printing supplies.

Some access methods require that you enter authentication in the client program. For instance, Figure 18.4 shows ZOC's method of initiating an SSH connection. You enter the username and password locally, and ZOC handles the SSH connection and sends that information in an encrypted form.

![](img/5d4d3092919d1d16884788127447cc6d_453_0.png)

## FIGURE 18.4

Depending upon the Device selection, ZOC enables or disables other fields to allow or disallow entry of information such as your username and password.

## NOTE

Most programs that ask for passwords either don't echo them or replace the password characters with asterisks or bullets to protect the password from snooping by passersby.

When you use ssh from Linux, the program doesn't require a username because ssh acquires that information from your local login name; but the program does require a password or passphrase in most configurations. You can configure ssh to use a number of authentication methods, though, each of which presents somewhat different password options.

As a security precaution, Red Hat Linux 6.0 comes configured to prevent root logins via Telnet. This configuration makes a cracker's job more difficult. For instance, suppose that a cracker somehow obtains the root password for your computer. To break in using telnet, the cracker would still require an ordinary user's password because telnetd refuses connects for root. (The same isn't true of all other connection methods; for instance, by default sshd allows root logins.) If you want to perform root operations remotely, then, you need to log in as an ordinary user and run su to obtain root privileges.

## Tip

If you use SSH for remote logins, I strongly encourage you to disallow root logins by SSH. You can do so by editing the /etc/ssh/sshd_config file. Add the line DenyUsers root to that file. (You might want to ensure that DenyUsers isn't already in use. If it is, you can add root to the list of users already denied.)

## Capabilities of a Terminal Session

In general, you can do anything from a terminal session that you can do in an xterm or at a text-mode local login. There are some exceptions, though:

- Sound—You can use audio software remotely; however, the sounds play on the speakers directly connected to the Linux computer. This could be disconcerting or annoying to a local user, so you might want to consider whether you really need a login sound if you'll be using the computer remotely with any frequency.
- Video—Most non-X Linux programs use plain text. A few, though, like some games and graphics viewers, use the computer's VGA hardware to display images. You can't use such programs remotely—or, more precisely, you can start them, but you don't see any useful output from them.
- Hardware access—If somebody local to the computer has inserted a floppy, CD-ROM, Zip disk, or similar device in the computer, you can access this device remotely. Unless you possess telekinetic powers, however, you can't insert a disk or tape remotely. If you have the need to access a variety of such devices on a regular basis, a changer may do the trick. Changers are variant versions of conventional devices that allow you to access several CDs, tapes, or other media by using one piece of hardware. Alternatively, you could use a large hard disk to store image files of the media in question, and mount them by using Linux's loopback device.
- X Window System—You can't access X-based programs from a terminal program alone. You can, however, run an X server locally to access X programs run on a remote Linux system. This topic is covered in Chapter 19.

You might also encounter problems and limitations depending on the specific program you use remotely. For instance, many Linux programs can use color to improve their displays. Even the lowly ls program can use this feature to display program files in one color, directories in another, and ordinary text files in a third. If your terminal program isn't capable of displaying color, you can't see these colors. Similarly, some programs use more or less sophisticated means of controlling cursor positioning and other text-formatting tasks, and some combinations of server-side application programs and client-side terminal programs don't work very well together.

Linux uses a special environment variable to communicate to programs what terminal type is in use. Normally, Linux queries the terminal program at the time of login to determine how to set this environment variable. Occasionally you might be asked to set it yourself when you log in remotely. To find out what you're using now, type env | grep TERM at an xterm, text-mode login, or network login. You should see a response such as TERM=vt220 or TERM=ANSI. Linux uses entries in the /etc/termcap file to determine what features each terminal type supports and how to activate them. Because different terminal programs may implement these features with varying degrees of fidelity, you might find that one terminal program works best when set to one terminal emulation and another works best with another emulation, even though both programs claim to support both emulations. You have to experiment to find what works best for you.

## Advantages of ssh and telnet

As mentioned previously, Linux provides several means of remote login. The two that are discussed in most detail in this chapter are SSH and Telnet. As mentioned earlier, the rlogin program and associated protocol can be convenient in some cases, but they are quite insecure, so I recommend against using them except on small networks that are isolated from the Internet as a whole.

## Using telnet for Convenience

The Telnet protocol is extremely popular and convenient. Because most modern OSs come with a telnet implementation, you can use it from almost any computer that's connected to the Internet to log on to any computer that has a Telnet daemon running to accept connections. This level of ubiquity is telnet's greatest strength.
