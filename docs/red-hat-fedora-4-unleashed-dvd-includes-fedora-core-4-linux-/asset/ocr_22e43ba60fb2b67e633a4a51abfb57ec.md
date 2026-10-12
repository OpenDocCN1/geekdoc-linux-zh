One of the most important environment variables is $PATH, which defines the location of executable files. For example, if as a regular user, you try to use a command that is not located in your $PATH, such as the `ifconfig` command, you'll see something like this:

```
$ ifconfig
-bash: ifconfig: command not found
```

However, you might know that `ifconfig` is definitely installed on your system, and you can verify this using the `whereis` command like so:

```
$ whereis ifconfig
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
```

You can also run the command by typing its full *pathname*, or complete directory specification like this:

```
$ /sbin/ifconfig
```

As you can see in this example, the `ifconfig` command is indeed installed. What happened is that by default, the `/sbin` directory is not in your `$PATH`. One of the reasons for this is that commands under the `/sbin` directory are normally intended to only be run by root. You can add `/sbin` to your `$PATH` by editing the file `.bash_profile` in your home directory (if you use the bash shell by default, like most Linux users). Look for the following line:

```
PATH=$PATH:$HOME/bin
```

You can then edit this file, perhaps using the `vi` editor (discussed in this chapter), to add the `/sbin` directory like so:

```
PATH=$PATH:/**sbin**:$HOME/bin
```

Save the file. The next time you log in, the `/sbin` directory will be in your `$PATH`. One way to use this change right away is to read in the new settings in `.bash_profile` by using the bash shell's `source` command like so:

```
$ source .bash_profile
```

You'll now be able to run `ifconfig` without the need to explicitly type its full pathname. Some Linux commands also use environment variables, for example, to acquire configuration information (such as a communications program looking for a variable such as `BAUD_RATE`, which might denote a default modem speed).

To experiment with the environment variables, you can modify the `PS1` variable to manipulate the appearance of your shell prompt. If you are working with `bash`, you can use its built-in `export` command to change the shell prompt. For example, if your default shell prompt looks like

```
[andrew@laptop -]$
```