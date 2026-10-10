provide the system with your password to confirm that you do, in fact, want to perform that change on the system.
Effectively, then, Sudo is your privilege pass. It is the magic passphrase that tells your system that you are in charge-so long as the privileges on your user account match.

# ### Using Sudo

When you are ready to use Sudo, you do not have to try very hard. Effectively, all you have to do is add sudo before the command that you are trying to push forward. If you do this, your program should then ask you for the account password for the account that you are on. If you provide this password and your credentials check out, it will perform the function.

For example, imagine that you want to reboot your system. As you may recall, the command to trigger your system to reboot is simply reboot.

However, reboot requires sudo privileges. If you were to simply try commanding your system with just reboot, it would tell you that you must be a superuser in order to execute that particular command.

That is where you would then escalate your command. At that point, you can add to your command, creating an input of:

```
$ sudo reboot
```

Your system then asks for the account password, and upon entering the password, it reboots as requested.

# ### Su instead of sudo?

This is perhaps one of the safest ways that you can use to elevate your privilege to trigger the system to obey. There are others, such as the switch user command, known as “su.” However, when you use the switch user command, you are asked for the root password and then given the superuser prompt.

You know that you are in the superuser prompt when you get a # as your input ready signal instead of the typical $ that you are likely used to seeing by now. The # should be your warning sign—if you see this waiting for you in the terminal, you know that you are on the root account, and you need to be careful.