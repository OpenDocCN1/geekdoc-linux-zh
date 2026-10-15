
Answering the prompt for each file can be a tedious prospect if you plan to download a large number of files, such as those for a system update. In this case, you can turn off the prompt with the prompt command, which toggles the interactive mode on and off. The mget operation then downloads all files it matches, one after the other.

```
ftp> prompt
Interactive mode off.
ftp> mget
(remote-files) * .c
PORT command successful
ASCII data connection
ASCII transfer complete
PORT command successful
ASCII data connection
ASCII transfer complete
ftp>
```

> Note To access a public FTP site, you have to perform an anonymous login. Instead of a login name, you enter the keyword anonymous (or ftp). Then, for the password, you enter your Internet address. Once the ftp prompt is displayed, you are ready to transfer files. You may need to change to the appropriate directory first or set the transfer mode to binary.

## Automatic Login and Macros: .netrc

The ftp client has an automatic login capability and support for macros. Both are entered in a user's ftp configuration file called .netrc. Each time you connect to a site, the .netrc file is checked for connection information, such as a login name and password. In this way, you needn't enter a login name and password each time you connect to a site. This feature is particularly useful for anonymous logins. Instead of your having to enter the username "anonymous" and your e-mail address as your password, they can be automatically read from the .netrc file. You can even make anonymous login information your default so that, unless otherwise specified, an anonymous login is attempted for any FTP site to which you try to connect. If you have sites you must log into, you can specify them in the .netrc file and, when you connect, either automatically log in with your username and password for that site or be prompted for them.

Entries in the .netrc file have the following syntax. An entry for a site begins with the term "machine," followed by the network or Internet address, and then the login and password information.

```
machine system-address login remote-login-name password password
```

The following example shows an entry for logging into the dylan account on the turtle.trek.com system:

```
machine golf.mygames.com login dylan password legogolf
```

For a site you would anonymously log into, you enter the word "anonymous" for the login name and your e-mail address for the password.

```
machine ftp.redhat.com login anonymous password dylan@turtle.trek.com
```

In most cases, you are using ftp to access anonymous FTP sites. Instead of trying to make an entry for each one, you can make a default entry for anonymous FTP login. When you connect to a site, ftp looks for a machine entry for it in the .netrc file. If none exists, ftp looks for a default entry and uses that. A default entry begins with the word "default" with no network address. To make anonymous logins your default, enter anonymous and your e-mail address as your login and password.

```
default login anonymous password dylan@turtle.trek.com
```

A sample .netrc file with a machine definition and a default entry is shown here.

```
.netrc
machine golf.mygames.com login dylan password legogolf
default login anonymous password dylan@turtle.trek.com
```

You can also define macros in your .netrc file. With a macro, you can execute several ftp operations at once using only the macro name. Macros remain in effect during a connection. When you close a connection, the macros are undefined. Although a macro can be defined on your ftp command line, defining them in .netrc entries makes more sense. This way, you needn't redefine them again. They are read automatically from the .netrc file and defined for you. You can place macro definitions within a particular machine entry in the .netrc file or in the default entry. Macros defined in machine entries are defined only when you connect to that site. Macros in the default entry are defined whenever you make a connection to any site.

The syntax for a macro definition follows. It begins with the keyword macdef, followed by the macro name you want to give it, and ends with an empty line. ftp macros can take arguments, referenced within the macro with $n, where $1 references the first argument, and $2 the second, and so on. If you need to use a $ character in a macro, you have to quote it using the backslash, \$.

```
macdef macro-name
ftp commands
empty-line
```

The redupd macro, defined next, changes to a directory where it then downloads Red Hat updates for the current release. It also changes to a local directory where the update files are to be placed. The prompt command turns off the download prompts for each file. The mget command then downloads the files. The macro assumes you are connected to the Red Hat FTP site.

```
macdef redupd
cd pub/redhat/current
lcd /root/redupdate
prompt
mget *
```
