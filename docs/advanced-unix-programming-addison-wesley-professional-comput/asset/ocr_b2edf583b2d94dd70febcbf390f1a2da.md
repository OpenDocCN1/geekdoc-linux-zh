```
    (void)initscr();
    ec_ERR( raw() )
    while (true) {
        ec_ERR( clear() )
        ec_ERR( mvwaddr( 2, 9, "What do you want to do?" ) )
        ec_ERR( mvwaddr( 3, 9, "1. Check out tape/DVD" ) )
        ec_ERR( mvwaddr( 4, 9, "2. Reserve tape/DVD" ) )
        ec_ERR( mvwaddr( 5, 9, "3. Register new member" ) )
        ec_ERR( mvwaddr( 6, 9, "4. Search for title/actor" ) )
        ec_ERR( mvwaddr( 7, 9, "5. Quit" ) )
        ec_ERR( mvwaddr( 9, 9, "(Type item number to continue)" ) )
        ec_ERR( c = getch() )
        switch( c) {
            case '1':
            case '2':
            case '3':
            case '4':
                ec_ERR( clear() )
                snprintf(s, sizeof(s), "You typed %c", c);
                ec_ERR( mvwaddr( 4, 9, s ) )
                ec_ERR( mvwaddr( 9, 9, "(Press any key to continue)" ) )
                ec_ERR( getch() )
                break;
            case '5':
                ok = true;
                EC_CLEANUP
                default:
                    ec_ERR( beep() )
                }
        }

    EC_CLEANUP_BGN
        (void)clear();
        (void)refresh();
        (void)endwin();
        exit(ok ? EXIT_SUCCESS : EXIT_FAILURE);
    EC_CLEANUP_END
    }
```

Some comments on this program:

+   * Most Curses functions return ERR on an error, so I defined an **ec_ERR** macro just for them. The documentation for Curses doesn't say that it uses errno, but I left it alone, knowing that if I do get a message its value may be meaningless.
+   
+   * Curses requires that you begin with **initscr** and end with **endwin**.
+   
+   * The Curses version of **tc_setraw** is **raw**.