# Changing Your ksh Path

The path statement tells the shell where to look for commands, scripts, and programs. For example, if you issue a command, the path statement tells the system to look in the named directories in a specific order.

As the following steps show, you change your ksh path by first identifying where your path statement is located, then editing the file that contains it (Code Listing 8.15).

# To change your ksh path:

+   1. grep PATH ~/.profile ~/.kshrc
+   To begin, check for path statements in the configuration files located in your home directory. If you wanted, you could also review the /etc/profile file, but you cannot edit that one.

+   2. Look through your system configuration files for a path statement. As Code Listing 8.15 shows, it’ll look something like PATH=/usr/bin:/usr/local/bin:/usr/sbin. Remember, if you have more than one path statement, find the last one executed. If you don’t have a path statement in your personal configuration files at all, then add one.

+   3. cp ~/.profile ~/.profile.backup
+   Make a copy of the file containing the path statement so that you can recover if you make mistakes. See Chapter 2 if you need more information on copying files.

+   4. vi ~/.profile
+   Use the editor of your choice to edit the configuration file with the path statement.

```
$ grep PATH ~/.profile ~/.kshrc
/home/users/e/ejray/.profile:PATH=/usr/bin:/usr/local/bin:/usr/sbin:
/home/users/e/ejray/.profile:export PATH
$
```

Code Listing 8.15 First, find out the location of your path statement(s).