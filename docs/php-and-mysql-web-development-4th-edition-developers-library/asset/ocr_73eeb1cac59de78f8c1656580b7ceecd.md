```
```
{
    print_error (NULL, "mysql_library_init() failed");
    exit (1);
}

/* initialise connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
    print_error (NULL, "mysql_init() failed (probably out of memory)");
    exit (1);
}

/* connect to server */
if [mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
    opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL]
{
    print_error (conn, "mysql_real_connect() failed");
    mysql_close (conn);
    exit (1);
}

/* ... issue statements and process results here ... */

/* disconnect from server, terminate client library */
mysql_close (conn);
mysql_library_end ();
exit (0);
}
```
```

Compared to the connect1 and show_opt programs that we developed earlier, connect2 does a few new things:

+   - It enables a default database to be specified as a command-line argument. This is consistent with the behavior of the standard clients in MySQL distributions.
+   - If a password value is present in the argument vector, `get_one_option()` makes a copy of it and then overwrites the original. This minimizes the time window during which a password specified on the command line is visible to ps or to other system status programs. (The window is only *minimized*, not eliminated. Specifying passwords on the command line still is a security risk.)
+   - If a password option was given without a value, `get_one_option()` sets a flag to indicate that the program should prompt the user for a password. That done in `main()` after all options have been processed, using the `get_tty_password()` function. This is a utility routine in the client library that prompts for a password without echoing it on the screen. You may ask, “Why not just call `getpass()`?” The answer is that not all systems have that function (for example, Windows does not).