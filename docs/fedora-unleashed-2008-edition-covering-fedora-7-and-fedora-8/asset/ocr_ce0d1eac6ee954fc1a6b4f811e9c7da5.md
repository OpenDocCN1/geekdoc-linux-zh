```
```
service rsync
{
    disable = yes
    socket_type    = stream
    wait           = no
    user           = root
    server         = /usr/bin/rsync
    server_args    = --daemon
    log_on_failure  += USERID
}
```
```

The items are straightforward and vary from service to service. Although you can edit this by hand, it can be configured via the command line or graphical service configuration clients.

# ## Changing Runlevels

After making changes to system services and runlevels, you can use the telinit command to change runlevels on the fly on a running Fedora system. Changing runlevels this way enables system administrators to alter selected parts of a running system to make changes to the services or to put changes into effect that have already been made (such as reassignment of network addresses for a networking interface).

For example, a system administrator can quickly change the system to maintenance or single-user mode by using the telinit command with its S option, like this:

```
```
# telinit S
```
```

The telinit command uses the init command to change runlevels and shut down currently running services. The command then starts services for the specified runlevel; in this example, the single-user runlevel is the same as runlevel 2. The init command can be run only from a console, not from an xterm running in an X session.

After booting to single-user mode, you can then return to multiuser mode without X, like this:

```
```
# telinit 3
```
```

If you have made changes to the system initialization table itself, /etc/initab, use the telinit command's q command-line option to force init to re-examine the table.

> TIP
> 
> Linux is full of shortcuts: If you exit the single-user shell by typing exit at the prompt, you go back to the default runlevel without worrying about using telinit.