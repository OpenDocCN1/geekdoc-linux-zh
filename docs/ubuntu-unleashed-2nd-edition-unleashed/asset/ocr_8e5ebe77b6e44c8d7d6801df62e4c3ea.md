If something breaks as a result of you changing the original file, you can always copy the original back into place using the command like this:

```
$ cp file.backup file
```

(You can save many blood-pressure-related medical expenses just by using these two simple commands. Feel free to send us any tokens of appreciation!)

# The sudo command

If you have come across Linux, you are probably aware of the command line. As you will find as you work through this book, Ubuntu puts a lot of reliance upon the sudo command while working at the command line. This command is used in front of other commands to tell Ubuntu that you want to run the specified command with super user powers. This sounds really special, and it actually is. When you work using the sudo command, you can make wide-ranging changes to your system that impact the way it runs. Be extra careful when running any command prefixed with sudo, however; a wrong option or incorrect command can have devastating consequences.

The use of sudo is straightforward. All you have to do is enter it like this:

```
$ sudo command commandoptions
```

Just replace the word command with the command that you want to run, along with any options. For example, the following command opens your xorg.conf file in vi and enables you to make any changes as the super user before being able to save it:

```
$ sudo vi /etc/X11/xorg.conf
```

Whenever you execute a command using sudo, you are prompted for your password. This is the same password that you use to log in to Ubuntu, so it is important that you remember it.

Sometimes, however, you may want to work with a classic root prompt instead of having to type sudo in front of every command (perhaps if you have to work with lots of commands at the command line that require super-user access, for example). sudo enables you to do this by using the sudo -i command. Again, you are prompted for your password, which you should enter, after which Ubuntu gives you the standard root prompt, as follows:

```
#
```

From here, you can execute any command without having to keep entering sudo.

# First Update

As discussed in Chapter 3, you should update your software as soon as you log in to Ubuntu for the first time to benefit from any available security and bug fixes. In that