Because most of the commercial X servers have demo versions of some sort, you can try several of them to see which program best suits your needs. X-Win32 is used in the examples throughout the rest of this chapter.

# X Terminals

If your only reason for having PCs is to use them as X servers for a Linux computer, you might want to consider purchasing X terminals instead. An X terminal is a computer that typically contains no hard disk and very limited RAM and CPU power. It functions exclusively as an X server, so you can think of it as a dumb terminal for X. X terminals often come with large monitors, which means they're often expensive. They are quiet, though, and aside from the monitor size, they are compact. If you have an outdated PC, you can effectively turn it into an X terminal by installing Linux on it and configuring it to function as an X server for another machine. This can be a great way to extend the life of an old PC.

Configuring an X terminal is well beyond the scope of this book. If you want to use one with Linux, I suggest you read the NCD X Terminal Mini-HOWTO, which comes with most Linux distributions. Some of the information in the rest of this chapter applies to X terminals, too, so you can glean some information from this chapter. X terminals generally use the X Display Manager (XDM) logon method described later in the next section.

# Logging On

There are two main ways to use an X server: by a textual login start or by an X Display Manager (XDM) login. Each method has advantages and disadvantages.

# Textual Login

A textual login is generally the easiest way to begin using an X server. The idea is that you log in to your Linux computer by using telnet or a similar program and launch your X-based programs from that telnet session. Here's an outline of what to do to use this method:

+   1. Log in to the Linux computer by using telnet, ssh, or some other text-mode remote-access program.
+   2. Set the DISPLAY environment variable to point to the computer on which you want to run the X server. If you're using the bash shell, you can do this with a command such as export DISPLAY=local.machine.name:0.0

You issue this command on the remote machine (that is, through your telnet login). local.machine.name is the name or IP address of the machine at which you're sitting. The 0.0 part of the DISPLAY variable tells the Linux computer which display to use on the server. If you're using a Macintosh or Windows computer, 0.0 or 0 is almost always correct. If you're using another Linux computer on which you have several virtual X sessions running, you might need to use a higher value, such as 0.1 or 1.