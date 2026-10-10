mation about users who are logged into a remote system, as well. You must know the correct name of the remote system, however.

# Example 3.10 finger

One morning, Don Quixote intends to send a message to Sancho but needs to know whether Sancho is on the system. Here is how he uses **finger** to find out:

```
[username@hostname username]$ finger<Enter>

Login      Name      Tty     Idle    Login Time    Office    Office Phone
root      root      tty1    2       Jul 10 07:30
quixote                   tty     2       Jul 10 11:16
panzasan                  tty6            Jul 10 08:30
```

Using **finger** without options gave him a list of all the currently logged-in users. Luckily, there were not too many. If he had wanted to just check for Sancho, he could have entered

```
$ finger panzasan<Enter>

Login: panzasan Name: (null)
Directory: /home/panzasan Shell: /bin/bash
On since Tue Jul 17 8:32 (CST) on tty6
No mail.
No Plan.
```

So, Don Quixote knows that Sancho is on the system. But what was that other information all about?

A user can create files called _.project_ and _.plan_ (please notice that the file-names must be preceded by a period, which we will call dot to indicate that they are normally hidden) to enhance the responses received when someone inquires about them with the **finger** command. The detailed process is beyond the scope of this book, but we will present a quick outline of it. Suppose that Nicholas the Barber (username *nicholas*) created hidden files called _.plan_ and _.project_ in his home directory by using a text editor such as vi (for details on vi, see Chapter 10, "The vi Editor"). When creating these files, he would have to remember to provide the r permission for others on those files as well as the x permission for others on the *nicholas* home directory. (File and directory permissions are discussed in detail in Chapter 6, "Linux File Permissions.") When users invoke the **finger** command with the *nicholas* username argument, they are provided with all the information Nicholas has written to those files.