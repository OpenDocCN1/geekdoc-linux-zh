# 3. vi .bash_profile

Use your favorite editor to open up the file in which you’ll be changing the path.

# 4. PATH=$PATH:$HOME/bin

Add a new path statement immediately below the last path statement. In this example, $PATH inserts the current value of the environment variable definition and inserts it into the directory bin in your home directory (Figure 8.3).

![](bbox=[0.55, 0.1, 0.9, 0.38])

# 5. Save the file and exit from your editor.

Refer to Chapter 4 for help if you need it.

# 6. su - yourid

As you learned back in Chapter 3, this command starts a new log-in shell so you can test your changes before logging out.

# 7. echo $PATH

Display the current path environment variable. This should include the addition you just made. It’s there, right? (See Code Listing 8.12.)

# Tips

+   - If you look through the path statements in your various configuration files, you might find a path statement that includes just a . (dot). For example, you might see something like PATH=/usr/bin:/usr/local/bin:.. The . adds your current directory, whatever it might be, to your path. Keep in mind, though, that it’s often safer not to have the current directory in the path so you don’t unintentionally run a program on which you’re working.

+   - You can use grep to make it easier to find the configuration files that set your path. grep PATH .b* is a good way to start, and grep PATH /etc/* is another goodie.

```
[ejr@Hobbes ejr]$ echo $PATH
/bin:/usr/bin:/usr/local/bin:/usr/bin/X11:/usr/X11R6/bin:/usr/local/games:/home/ejr/bin
[ejr@Hobbes ejr]$
```

Code Listing 8.12 Using echo, you can verify that your new path statement exists.

Your system configuration files will be much less confusing later on if you keep all related changes together. Therefore, you should keep the path statements together, rather than just plug an entirely random PATH statement into your configuration files.