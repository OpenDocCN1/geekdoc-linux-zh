# **—no-wall**

Do not send wall ssage before halt, power-off, reboot.

# **—global**

When used with **enable** and **disable**, operate on the global user configuration directory, thus enabling or disabling a unit file globally for all future logins of all users.

# **—no-reload**

When used with **enable** and **disable**, do not implicitly reload daemon configuration after executing the changes.

# **—no-ask-password**

When used with **start** and related commands, disables asking for passwords. Background services may require input of a password or passphrase string, for example to unlock system hard disks or cryptographic certificates. Unless this option is specified and the command is invoked from a terminal, **systemctl** will query the user on the terminal for the necessary secrets. Use this option to switch this behavior off. In this case, the password st be supplied by so other ans (for example graphical password agents) or the service might fail. This also disables querying the user for authentication for privileged operations.

# **—kill-who=**

When used with **kill**, choose which processes to send a signal to. Must be one of **main**, **control** or **all** to select whether to kill only the main process, the control process or all processes of the unit. The main process of the unit is the one that defines the life-ti of it. A control process of a unit is one that is invoked by the manager to induce state changes of it. For example, all processes started due to the `ExecStartPre=`, `ExecStop=` or `ExecReload=` settings of service units are control processes. Note that there is only one control process per unit at a ti, as only one state change is executed at a ti. For services of type `Type=forking`, the initial process started by the manager for `ExecStart=` is a control process, while the process ultimately forked off by that one is then considered the main process of the unit (if it can be determined). This is different for service units of other types, where the process forked off by the manager for `ExecStart=` is always the main process itself. A service unit consists of zero or one main process, zero or one control process plus any nu er of additional processes. Not all unit types manage processes of these types however. For example, for mount units, control processes are defined (which are the invocations of /usr/bin/mount and /usr/bin/umount), but no main process is defined. If omitted, defaults to **all**.