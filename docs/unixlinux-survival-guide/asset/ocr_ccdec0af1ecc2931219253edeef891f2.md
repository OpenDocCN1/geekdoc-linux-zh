To actually move or copy the directory structure of certain user account, you could use the commands cp, tar, and cpio. Actually you have some more commands that could be used for the task at hand, but the ones mentioned should be sufficient and are available on almost every *NIX system. Which command is the fastest and best suited for the task is the source of debate among system administrators and very well suited to start a lively discussion during a break at a conference. All the mentioned commands support options to make sure the permissions and ownership settings will not be changed during the transfer.

All programs are started from within the directory that contains the directories of the respective user accounts. Let’s have a look at the contenders. Listing 3.30 shows the use of cp.

# LISTING 3.30 The Use of cp

```
root@unixhost> cp -pR silvied /export/adminusers/
```

The $HOME directory of the user account silvied will be copied to /export/adminusers; the option -r instructs the program to recursively copy all enclosed directories as well.

Rumor has it, the program cpio is supposed to be the fastest of all three. Its real purpose in life is the creation of archives, similar to tar. Listing 3.31 shows the usage.

# LISTING 3.31 Moving a Directory with cpio

```
root@unixhost> find silvied -print | cpio -pudm /export/adminusers/
```

Here the output of find is piped to cpio. The options are as follows: p is the so-called pass mode; the program reads from stdin, also known as the pipe. u is just a precaution (with a potential to create some confusion); the program will overwrite a newer file if it exists. d instructs the program to create directories if needed. m ensures that the permissions and the ownership will be retained.