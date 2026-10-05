# 4.1 Common Features

For example, all the files that start with the letter a can be represented as a* and all the files that end in .txt can be represented as \*.txt.

# History

The bash and tsh programs have the ability to keep a running history of the commands you have run. The bash shell can store a history across logins, which allows you to see what commands you ran before you logged out.

The history is stored as a “sliding window,” so that if the history command size is 50, and you run 51 commands, command number one is forgotten, and the first entry in history file is command number two.

# Environment Variables

Environment variables store information used by the shell (such as the PATH variable) or information used by specific applications (such as Netscape or man). Here are some of the common variables that get set on login on a typical system:

+   * PATH—Contains a search path for applications. The shell starts on the left side of the search path and searches every item listed in the search path until it reaches the end, or finds the application.
* HOME—Has the location of the user’s home directory, as it’s defined in the /etc/passwd file.
* MANPATH—Used by the man program to search for man pages. This typically contains /usr/man, /usr/local/man, and /usr/X11R/man but may include directories where other manual pages are located.
* TERM—Terminal type, which should relate to an entry in the /etc/termcap file.
* MAIL—Contains the location of a user’s mail spool file, typically /usr/sp/mail/user. In some cases, this can be set to /var/mail/user.
* DISPLAY—Contains the host, monitor, and X server for X applications to display on. See the chapter on X for more information about how the DISPLAY variable works.
* EDITOR—Contains the program used as a user’s default editor. Usually set to /bin/vi.