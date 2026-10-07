# smail

The **sma il** mail system is similar to the **sendmail** system in most of its actions, although the configuration process is different. In some ways, **sma il** is easier to work with than **sendmail** and can be a good choice for smaller systems. If you choose to use **sma il** as your mailer, you will have to make some manual modifications to configuration files because there are few automated or scripted routines available.

The **sma il** system has many options and configuration details, most of which are never used. We'll look at the primary controlling parameters that most Linux users will need, and essentially ignore those that are very seldom (if ever) used in real situations. For more information on the options and configuration controls we skip over in this chapter, see the man pages or **sma il** documentation. We'll focus this chapter on showing you how to get **sma il** up and running quickly and easily to handle the situations most Linux systems will find themselves working with.

# Setting Up smail

The **sma il** system requires several links to exist so **sma il** can execute properly. The two most important links are to the files `/usr/bin/rmail` and `/usr/lib/sendmail` (sometimes located as `/usr/sbin/sendmail`, depending on the version of Linux). These links are necessary because most user mail applications send outgoing mail to either **rmail** or **sendmail** (depending on the mail software), and this has to be redirected to **sma il**. Links allow this redirection to occur transparently without altering the user mail applications.

You should verify that the **rmail** and **sendmail** files are linked to **sma il**, and if not, establish the links. Usually, the links established are symbolic and will show in a directory listing with an entry like this:

```
lrwxrwxrwx 1 root root 6 Sep 16:35 file1 -> file2
```

The arrow (->) shows that a symbolic link exists. (For more information on links and symbolic links, see Chapter 8, “Using the File System.”) Check both the **rmail** and **sendmail** binaries for these symbolic links. If the symbolic links do not exist already, create them with the following commands:

```
ln -s /usr/local/bin/sma il /usr/bin/rmail
ln -s /usr/local/bin/sma il /usr/lib/sendmail
```

Of course you should substitute whatever directory pathnames are valid on your system for **sma il**, **sendmail**, and **rmail**. After you have created the links, verify that they exist by displaying the directories and look for the symbolic link notation shown earlier.