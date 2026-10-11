# ## Init Process

In addition to the execution of the run control scripts, the `init` process checks the `/etc/initab` file during the boot process. Each entry in the `initab` file has the following format:

```
`id:runlevel:action:process`
```

There is one special line in the `/etc/initab` file that tells the system which default run level it should start up in. The line is similar to this:

```
`is:3:initdefault:`
```

It can be used to tell Solaris to boot to a different run level than 3. For example, 2 would be used if you want to make sure the system comes up without exporting any file systems. The `init` process starts the other processes when the indicated run level is reached. To determine the current run level, type the following command at the command prompt:

```
`who -r`
```

Here is a typical output for this command:

```
`run-level 3 Feb 6 15:25:3 0 0 5`
```

# ## Shutdown Commands

To shut the server down gracefully from the console port, there are several commands you can type. This command will bring the server back down to the OK prompt:

```
`init 0`
```

Another way to shut down the server is to use the following command:

```
`shutdown -y -g60 -i0 'server is coming down'`
```

This command will send the message `Server is coming down` to all the users and designate a 60-second (`g60`) delay before the shutdown process starts. When the server is at the OK prompt, it is safe to turn off the power. No file system or configuration file damage will occur.

> **WARNING** Never power off a server if it is not at run level 0 (the OK prompt). The file system can become badly damaged and need repair if the server "crashes" or has sudden power loss. Also, the configuration files could contain errors. If the file system is damaged beyond repair or the configuration files are badly damaged, a server tape restore or a server partial rebuild may be your only option.