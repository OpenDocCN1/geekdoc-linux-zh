any of three ways: by manually editing the account's entry in /etc/passwd or /etc/
group, by using Linux command-line utilities that pass the relevant information to those
files, or by using a GUI tool like Linuxconf to enter the same information.

# User Accounts

Different types of users have different needs and may be assigned different types of\accounts. Selecting the right type of account will ensure that the user has the needed
access without allowing access beyond his or her scope. Common account types include:

+   - TCP/IP network access accounts (PPP and SLIP) to link users to the server (and per-
haps beyond) via TCP/IP networking protocols
- UUCP network accounts, which allow for networking using older protocols
- Normal login accounts (also called shell accounts)
- Mail accounts (POP, virtual POP, or IMAP) for mail retrieval

The special account types you'll encounter frequently are Point-to-Point Pro-
tocol (PPP) and Post Office Protocol (POP) accounts. Both of these account types obviate
a need for a user's home directory. Both PPP and users never directly log
to a user on the system, so such users have no need for a home directory. Using
Linuxconf, POP users' login shells are set to /bin/f/alse. This way, if the user
ntempted to log in a console or through a protocol such as Telnet, the session would
immediately terminate with an error exit code of -1in other words, the login attempt
would fail, if the user presented a correct password.

The POP user's Mail User Agent (MUA) authenticates with the mailer system itself. The
PPP user does a login shell of sorts, though. The login shell is effectively the PPP da-
mon, and authentication is performed when the connection is created. Under Red
Hat 7.0, Linuxconf creates a home directory for the PPP user at /home/loginwhere
loginname the user's login. The PPP user's login shell is set to /usr/lib/linuxconf-
lib/pplogin.

# The /etc/passwd File

Information about each user is contained in the /etc/passwd file. As a system admin-
istrator, it is critical that you clearly understand this important file. In the excerpt
in Listing 6.1, you'll notice that root is always assigned the
user ID (UID) 0 and group ID (GID) 0. Other special users and accounts associated with
services and daemons are listed after root and always have UID and GID values below
500. Last, regular and special accounts for individual users are listed.