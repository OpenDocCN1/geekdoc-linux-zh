# NOTE

You will want to save the ds1-dpkg.ds1 extension so you can create more extensions the next time you reboot DSL. Use the standard methods as described in Chapter 4. Later, when you need this system extension, you can use the MyDSL desktop icon Load Local and not have to keep downloading this extension.

# Step 3: Install and Test Desired Package

Now, open a regular shell (ds1 user) to enter the further commands:

```
$ sudo apt-get install zile
```

Because DSL does not normally use Debian packages, there are no updates to the system menu. So, you must know the command to start the newly installed package. So, for this example, type zile from the shell prompt.

# NOTE

In case you are not familiar with Zile/Emacs, you may find yourself stuck and unable to exit this program. If that is the case, you can simply press Ctrl-x Ctrl-c to exit.

The whereis command is very useful in determining the full path to the zile command. You will need this full path later in your configuration.

Thoroughly test the application. You will then be ready to repackage the application and all of its dependencies into a ds1 type extension.

# Step 4: Create the Extension

From the open shell, enter the following :

```
$ deb2ds1
```

Enter the full name for your DSL extension.
Example: rox.ds1 zile.ds1

Enter the MyDSL menu name for your program.
Example: Rox Filer Zile Emacs
Is this an X application: (y/..) n

Enter the full path to the executable.
Example: /usr/bin/rox /usr/bin/zile