done
$
When you run the code, you get a listing of the executable files that you can use from the command line:

```
$ ./test25 | more
/usr/local/bin:
/usr/bin:
/usr/bin/Mail
/usr/bin/Thunar
/usr/bin/X
/usr/bin/Xorg
/usr/bin/[
/usr/bin/a2p
/usr/bin/abiword
/usr/bin/ac
/usr/bin/activation-client
/usr/bin/addr2line
...
```

The output shows all the executable files found in all the folders defined in the `PATH` environment variable, which is quite a few!

# ### Creating multiple user accounts

The goal of shell scripts is to make life easier for the system administrator. If you happen to work in an environment with lots of users, one of the most boring tasks can be creating new user accounts. Fortunately, you can use the `while` loop to make your job a little easier. Instead of having to manually enter `useradd` commands for every new user account you need to create, you can place the new user accounts in a text file and create a simple shell script to do that work for you. The format of the text file we'll use looks like this:

```
`loginname, name`
```

The first entry is the login name you want to use for the new user account. The second entry is the full name of the user. The two values are separated by a comma, making this a comma-separated values (CSV) file format. This is a very common file format used in spreadsheets, so you can easily create the user account list in a