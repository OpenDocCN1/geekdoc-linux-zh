You can add the new user account for **PPP** (usually called *ppp* for convenience) using any of the user administration scripts you want, or you can simply edit the /etc/passwd file and add the user yourself (only if you do not use password shadowing). Because the PPP login does not have a home directory per se, you don’t need to create mail boxes and other paraphernalia that is normally created by a user administration script. The line you want to add to the /etc/passwd file looks like this:

```
ppp::301:51:PPP account:/tmp:/etc/ppp/pppscript
```

This creates a user account *ppp* with no password. (The asterisk in the second field can’t be matched.) The user ID is **301** in this example, but you can substitute any unused user ID. The group ID is best set to a new group called *p pp*, although this is not necessary. The fourth field is a comment that describes the account’s purpose. The home directory is set to /tmp in this case because you don’t want to keep files in the *pp* account home directory. The last field in the /etc/passwd entry is used for a startup script. In this case, I’ve created a new script called /etc/ppp/pppscript, which takes care of starting PPP properly. You will have to create this script yourself. The contents of pppscript should look like this:

```
#!/bin/sh
mesg n
stty -echo
exec pppd -detach silent modem crtscts
```

The first line invokes the Bourne shell to run the script. The second line suppresses messages for this login. The third line stops the remote from echoing everything back. The fourth line invokes the *pppd* daemon with some options that control its behavior. (You’ll look at the *pppd* daemon in more detail in a few moments.) Make sure the file pppscript is executable.

# ## Setting Up chat

Because you are going to use a modem to connect to your ISP, you need to tell PPP about the modem and how to use it. PPP uses a program called *chat* to handle all these details. (You can use utilities other than *chat*, but experience has shown that *chat* is the most foolproof of the options as well as one of the easiest to set up quickly.) The *chat* utility takes a lot of its features from the UUCP program, which makes it familiar for many veteran system administrators.

The *chat* utility requires a command line that tells it what number to call to connect to your ISP and what types of login responses are required. All of this information is placed on a single-line *chat* script. These lines are often stored in files to prevent you from having to type the commands every time you want to access the Internet.