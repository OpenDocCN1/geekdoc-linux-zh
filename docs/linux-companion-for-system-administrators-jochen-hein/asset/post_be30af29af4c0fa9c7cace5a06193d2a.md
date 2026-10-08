
# USER LOGIN 131

| Character sequence | Substitution with |
| :--- | :--- |
| \s | name of the operating system (LINUX) |
| \n | name of the computer (host name) |
| \r | release of the operating systems (for example 1.2.3) |
| \v | additional version information |
| \m | computer architecture (i386) |
| \d | current date |
| \t | current time |
| \b | baud rate |

Table 4.8 Substitutions in the /etc/issue file.

Some distributions generate the /etc/issue file anew at each system start-up in the script /etc/rc.local, entering the current kernel version. In the system-specific adaptation of the /etc/issue file, this ‘feature’ should be disabled.

When connecting a serial terminal, the -L option must be specified to make the getty recognize the terminal as being locally connected. In addition, different baud rates can be specified, separated by commas, which the user can toggle by `Break`.

## 4.9.2 The internal getty of the System V Init

There is a patch for the System V Init which integrates a simple getty, derived from getty, into the init program. A simple login is integrated as well, so that a series of error sources can be excluded. On the one hand, the other, a good portion of RAM can be used for other purposes, particularly if many getty programs be started and the computer has only a small amount of RAM.

To use the internal getty, the new keyword getty was introduced into the inittab configuration. The following example shows its use in the inittab file.

```
11:123456:getty:tty
```

This internal getty is not suited for terminals or modems because it does not include configuration options for baud rates and similar things. It is, however,

132 CONFIGURATION AND ADMINISTRATION

a reasonable alternative for virtual consoles, if many getty programs are going to be started.

## 4.9.3 The program getty_ps

The getty_ps program was originally developed by Paul Sutcliffe and is maintained by Kris Gleason. This program is suited for operation both on virtual consoles and incoming on outgoing connections via modem. Because of its greater flexibility, configuration is slightly more complicated than with the simple getty. Nearly all the configuration takes place at runtime. The only decision to be made for the compilation of getty_ps is whether the program is to be configured and installed according to the file system hierarchy standard. Table 4.9 shows an overview of the paths and files used.

| Function | Default path | FHS path |
| :--- | :--- | :--- |
| gettydefs Configuration | /etc/gettydefs | /etc/conf.getty |
| Local configuration | /etc/defaults/getty.Line | /etc/conf.getty.Line |
| Lock files | /usr/sbin/uucp | /var/lock |

Table 4.9 Paths and files for getty_ps.

First, the getty file must be included in the /etc/initab file. It is important that at the order of parameters is correct. Instructions can be found in the man page; furthermore, it is possible to try out the initab file on a free console without entering it in the initab file by directly inputting the parameter after the third colon as a command. As parameters, the getty program expects at least the tty when the login is to take place. Optional parameters are the specification of the speed and of the terminal type which has an entry in the /etc/termcap file. The following example shows two entries in the /etc/initab file for the System V init, one for a virtual console and one for a serial terminal.

```
1:12345:respawn:/sbin/getty tty1 VC linux-28
1:2345:respawn:/sbin/getty ttyS DT9600 vt220
```

As a second step, the file /etc/gettydefs must be adjusted. The format is documented in the man page gettydefs(5). The getty_ps program sources include an example which can initially be employed without modification. It contains the default configuration for the initialization of the

133 USER LOGIN

connections and the selected speeds. The individual lines have the following format:

speed #init-flags #final-flags #login-string #next-speed

After each entry, an empty line must be inserted; the first line is the default setting if no speed is specified at the call of the getty. Comments are marked by a # at the beginning of a line. When changes have been made to this file, the command getty -c should be used to check the syntax of this file because the event of syntax errors in this file, no login to the system will be possible. speed is the symbolic specification of the speed specified as a parameter the call of getty. If the same value is entered for next-speed, the speed cannot be changed. Otherwise, the Break key can be used to toggle between the different speeds.

The init-flags and final-flags values determine the initial and final TERMIO settings. Usually, no modification is needed. For my terminal, the XON/XOFF protocol had to be switched off; thus I included the additional settings -IXON -IXOFF in the final-flags. The flags to be specified here are exactly the same parameters as the ones known to the stty program. Interested users should refer to the main page for stty(1).

login-string contains the text displayed as the login prompt. As with the output of the /etc/issue file, a series of special character sequences is substituted. Table 4.10 shows a list of these character sequences and their substitutions.

134 CONFIGURATION AND ADMINISTRATION

| Character sequence | Substitution with |
| :--- | :--- |
| @B | Baud rate |
| @D | Current date (MM/DD/YY) |
| @L | Current tty |
| @S | Name of the computer (host name) |
| @T | Current time (HH:MM:SS) |
| @V | Version of the operating system |
| @@ | One single @ character |
| \ | One backslash (\) |
| @b | One backspace (Ctrl-H) |
| @c | Prevents line feed |
| @f | One form feed (Ctrl-L) |
| @n | One new line (Ctrl-J) |
| @r | One carriage return (Ctrl-M) |
| @s | One space |
| @t | One tab (Ctrl-I) |
| @nnn | ASCII character with octal value |
| @ | One @ character |

Table 4.10 Substitutions in getty_ps.

In the last step, the program can be specially configured. This concerns not only the issue, but also speeds. Configurations that apply to all connections are set in the file /etc/getty (or /etc/defaults/getty); With the option -d another file can be specified. This is often done when testing modifications; then, the remaining getty programs will be able to run.

The configuration files contain lines of the form NAME=value; there is a whole series of values that can be changed at runtime. The most important values are presented in the following paragraphs; a more detailed discussion of all possible settings can be found in the man page for getty(1).

## SYSTEM=name
The character sequence @S is usually substituted with the host name. With this setting, a different name for the getty can be set.

135 USER LOGIN

VERSION=string
The character sequence @V is usually substituted with the version of the operating system. Here, the specified text can be used instead. If the text begins with a slash (/), the contents of the file are displayed.

ISSUE=string
At start-up, getty displays the contents of the file /etc/issue. Here, you can either specify another text or, if the string begins with a slash (/), another file.

LOGIN=name
name is the complete path to a program, which is to be used instead of the normal /bin/login. As a parameter, the entered user name is passed.

CLEAR=value
getty deletes the screen before the file /etc/issue is displayed. If the value NO is entered here, the screen is not deleted.

After the general settings, there is a series of configuration options for the use of modems or serial terminals.

INIT=string
At the start of getty, the modem can be initialized with this value, for example, with the very INIT="" ATZ\r. The characters are interpreted as 'Chatscript', beginning with a text which is expected by the modem.

HANG=value
Usually, getty hangs up when it starts, so after three unsuccessful attempts or after logging out, the line is interrupted. If the value NO is entered here, the phone is not hung up, but a new login prompt is displayed. The same function is carried out by the command line option -h.

WAITCHAR=value
getty waits with the display of the login prompt until a character has been entered. This is sensible for directly connected terminals or modems which always display Carrier Detect.

DELAY=seconds
Normally, there is no delay between the first character entered and the display of the login prompt. With this option (or the command line option -r), a delay can be set.
