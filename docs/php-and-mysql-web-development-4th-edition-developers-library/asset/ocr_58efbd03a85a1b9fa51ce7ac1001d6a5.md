```
```
case '?':
    my_print_help (my_opts);  /* print help message */
    exit (0);
case 'p':
    if (!argument)            /* password */
        /* no value given; solicit it later */
        ask_password = 1;
    else
        /* copy password, overwrite original */
        {
            opt_password = strdup (argument);
            if (opt_password == NULL)
                {
                    print_error (NULL, "could not allocate password buffer");
                    exit (1);
                }
            while (*argument)
                *argument++ = 'x';
            ask_password = 0;
        }
    break;
}
return (0);


int
main (int argc, char *argv[])
{
int opt_err;

    MY_INIT (argv[0]);
    load_defaults ("my", client_groups, &argc, &argv);

    if ((opt_err = handle_options (&argc, &argv, my_opts, get_one_option)))
        exit (opt_err);

    /* solicit password if necessary */
    if (ask_password)
        opt_password = get_tty_password (NULL);

    /* get database name if present on command line */
    if (argc > 0)
    {
        opt_db_name = argv[0];
        --argc; ++argv;
    }

    /* initialize client library */
    if (mysql_library_init (0, NULL, NULL))
```
```