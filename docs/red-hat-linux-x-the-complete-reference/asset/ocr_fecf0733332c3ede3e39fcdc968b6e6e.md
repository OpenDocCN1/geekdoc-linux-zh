Certain features require you to enter an option on the command line after the get command. For example, adding the -R command specifies a recursive capability, enabling you to download and create subdirectories and their files. This command is particularly helpful in downloading upgrade directories, such as Red Hat's, which contain several subdirectories. The following example downloads the i386 directory and all its subdirectories:

```
get -R i386
```

If you want to give a file a different name on your local system, use the -z option. Enter the local filename you want after the remote filename. The following example downloads the readme file and renames it calinfo. If you did not use the -z option, both names would be taken as files to be downloaded, instead of only the first.

```
get -z readme calinfo
```

To obtain recent files only, you can use the -n option, which takes as its argument a number of days. Files older than the specified number of days are not retrieved. The following example downloads files posted within the last 30 days:

```
get -n 30 *
```

# Bookmarks and Macros

When you disconnect (close) from a site, NcFTP automatically saves information about it. This includes the site address, the directory you were in, and the login information. This information is placed in a file called bookmarks in your .ncftp directory. The site information is given a bookmark name you can use to access the site easily again. The bookmark name is usually the key name in the site's address. You can use this name to connect to the site. For example, ftp.redhat.com could be named redhat. You could then connect to it with the following command:

```
open redhat
```

You can edit your bookmark entries using the bookmark editor. Enter the command bookmarks to bring up the editor. Remote systems you have accessed are listed on the right side of the screen. Bookmark commands are listed on the left. You can change the bookmark name or edit login information, such as the username or password, the remote directory, or the transfer mode.

The NcFTP program supports macros for simple operations. You create macros by entering macro definitions in the macros file located in your .ncftp directory. Initially, no such file will exist, so you have to create one using any text editor. The macros file is a simple text file you can edit with any text editor. The syntax for a macro definition follows:

```
macro macro-name
ftp-commands
end
```

A macro executes NcFTP commands. Remember, however, the ! is an NcFTP command that enables you to execute any Linux command or script. With a preceding !, you can define an NcFTP macro that executes any shell command or any script you have written. A simple example of a macro is as follows:

```
macro ascii
type ascii
end
```

Macros support parameters similar to those used by shell programs. Arguments entered after a macro name can be referenced in the macro using a $ sign and the number of the argument in the argument list. $1 references the first argument, $2 the second, and so on. $* is a special parameter that references all arguments, and $@ references all arguments, encasing each in double quotes.

```
macro cdls
```