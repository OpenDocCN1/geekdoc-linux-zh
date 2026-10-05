# RUNNING COMMANDS WITH root PRIVILEGES

letters), alias_list is a comma-separated list of one or more elements that make up the aliases. Preceding an element of an alias with an exclamation point (!) negates it.

User_Alias The alias_list for a user alias is the same as the user_list for a user privilege specification (discussed in the previous section). The following lines define three user aliases: OFFICE, ADMIN, and ADMIN2. The alias_list defines the first aliases the usernames mark, sam, and sls; the second includes two users and members of the admin group; and the third includes members of the admin group except Max.

```
User_Alias OFFICE = mark, sam, sls
User_Alias ADMIN = max, zach, %admin
User_Alias ADMIN2 = %admin, !max
```

Runas_Alias The alias_list for a runas alias is the same as the run_list for a user privilege specification (discussed in the previous section). The following SM run aliases includes the usernames and sm:

```
Runas_Alias SM = sam, sls
```

Host_Alias Host aliases are meaningful only when the sudo file is referenced by sudo on more than one system. The alias_list for a host alias is the same as the host_alias for a user privilege specification (discussed in the previous section). The following line defines the LCL alias includes the systems dog and plum:

```
Host_Alias LCL = dog, plum
```

If you want to use fully qualified hostnames (hosta.example.com instead of just hosta) in this list, you must set the fdn flag (next section). However, doing so may slow the performance of sudo.

Cmnd_Alias The alias_list for a command alias is the same as the command_list for a privilege section (discussed in the previous section). The following command alias includes three files and, by including a directory (denoted by its trailing /), incorporates all rates in that directory:

```
Cmnd_Alias BASIC = /bin/cat, /usr/bin/vi, /bin/def, /usr/local/safe/
```

# DEFAULTS (OPTIONS)

You can change configuration options from their default values by using the Defaults keyword. Most values in this list are flags that are implicitly Boolean (either on or off) or strings. Turn on a flag by naming it on a Defaults line, and you turn it off by preceding it with a !. The following line in the sudoers file would turn off the lecture and fdn flags and turn on ty-tickets:

```
Defaults !lecture,tty_tickets, !fdn
```

This section lists some common flags; see the sudoers man page for a complete list.

env_reset Causes sudo to reset the environment variables to contain the LOGNAME, SHELL, USER, USERNAME, and SUDO* variables only. See the sudoers man page for more information.