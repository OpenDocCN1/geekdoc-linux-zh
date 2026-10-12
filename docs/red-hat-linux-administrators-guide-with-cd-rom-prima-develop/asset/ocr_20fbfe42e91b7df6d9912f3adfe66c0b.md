# Locating Additional Files

The which command helps to locate files within the available paths. However, this command is only good for locating files found in exported paths. If the directory is not in your path, the system will be unable to find the file in question. Once your shell has reread the contents of /etc/profile, you should be able to see the newly exported files. Had I executed a which command on Netscape before adding it to /etc/profile, it would not have been able to inform me that the executable is located in /opt/netscape/netscape.

To see all the directories currently read by bash and that are in the current path, enter echo $PATH. Do not forget the dollar sign before PATH or forget to type the command in all capital letters. PATH is a variable and as such has several unique features. If you type it without the dollar sign, then the word PATH will be printed to the screen.

# Temporarily Changing Your $PATH

To add more directories to your path, at least temporarily, you would issue the following command:

```
export PATH=" $PATH:/usr/local/bin:/sbin"
```

For the duration of the session that you are logged in, you will be able to see not only the executable files found in your previously defined $PATH, but also the binaries located in /usr/local/bin and /sbin. If you are trying to keep the system secure and limit access to certain files, this feature can be useful for those instances where typing the entire pathname is long and tedious. By combining the export feature with bash's history file, you can potentially cut the amount of required typing in half.

If you want to make these paths a permanent feature for your own use and not allow others access to the same directories, customizing the .bash_profile file will produce the same results, except only on a user-specific basis.

This local file sets the paths only for needed files, however. To start up files automatically upon login or to execute them without manually calling them, you would need to add their paths, or just their binary name if their path is already listed, to the .bash file. It is here that files start up automatically. It can also be