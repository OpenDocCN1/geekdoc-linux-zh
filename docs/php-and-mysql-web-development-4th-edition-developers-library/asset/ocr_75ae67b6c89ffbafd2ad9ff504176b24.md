```
arg 2: --password=secret
arg 3: --host=some_host
arg 4: -h
arg 5: yet_another_host
arg 6: --user=bill
arg 7: x
Connection parameters after calling handle_options():
hostname: yet_another_host
username: bill
password: secret
port number: 0
socket filename: [null]
Argument vector after calling handle_options():
arg 0: x
```

The output shows that the hostname is picked up from the command line (overriding the value in the option file), and that the username and password come from the option file. handle_options() correctly parses options whether specified in short-option form (such as -h yet_another_host) or in long-option form (such as --user=bill).

The get_one_option() helper function is used in conjunction with handle_options(). For show_opt, it is fairly minimal and takes no action except for the --help or -? options (for which handle_options() passes an optid value of '?'):

```
static my_bool
get_one_option (int optid, const struct my_option *opt, char *argument)
{
  switch (optid)
    {
    case '?':
      my_print_help (my_opts); /* print help message */
      exit (0);
    }
  return (0);
}
```

my_print_help() is a client library routine that automatically produces a help message for you, based on the option names and comment strings in the my_opts array. To see how it works, try the following command:

```
% ./show_opt --help
```

You can add other cases to the switch() statement in get_one_option() as necessary (and we'll do so in connect2 shortly). For example, get_one_option() is useful for handling password options. When you specify such an option, the password value may or may not be given, as indicated by OPT_ARG in the option information structure. That is, you can specify the option as --password or --password=your_pass if you use the long-option form, or as -p or -pyour_pass if you use the short-option form. MySQL clients typically allow you to omit the password value on the command line, and then prompt you for it.