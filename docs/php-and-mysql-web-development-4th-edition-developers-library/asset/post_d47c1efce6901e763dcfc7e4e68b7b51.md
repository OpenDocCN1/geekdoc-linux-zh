
## 7.6 Writing Clients That Include SSL Support

user wants an SSL connection. Do this by invoking `mysql_ssl_set()` after calling `mysql_init()` and before calling `mysql_real_connect()`. The sequence looks like this:

```c
/* initialize connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
    print_error (NULL, 'mysql_init() failed (probably out of memory)');
    exit (1);
}

#define HAVE_OPENSSL
/* pass SSL information to client library */
if (opt_use_ssl)
    mysql_ssl_set (conn, opt_ssl_key, opt_ssl_cert, opt_ssl_ca,
                   opt_ssl_capath, opt_ssl_cipher);
#if (MYSQL_VERSION_ID >= 50023 && MYSQL_VERSION_ID < 50100) \
    || MYSQL_VERSION_ID >= 50111
    mysql_options (conn,MYSQL_OPT_SSL_VERIFY_SERVER_CERT,
                   (char*)&opt_ssl_verify_server_cert);
#endif
#endif

/* connect to server */
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
                opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, 'mysql_real_connect() failed');
    mysql_close (conn);
    exit (1);
}
```

This code doesn't test `mysql_ssl_set()` to see whether it returns an error. Any problems with the information you supply to that function will result in an error when you call `mysql_real_connect()`. The complicated test to determine whether to invoke `mysql_options()` reflects the addition of `MYSQL_OPT_SSL_VERIFY_SERVER_CERT` occurred in version 5.0.23 for MySQL 5.0 and 5.1.11 for MySQL 5.1.

Compile `exec_stmt_ssl.c` to produce the `exec_stmt_ssl` program and then run it. Assuming that the `mysql_real_connect()` call succeeds, you can proceed to issue statements. If you invoke `exec_stmt_ssl` with the appropriate SSL options, communication with the server should occur over an encrypted connection. To determine whether that is so, issue the following statement:

```sql
SHOW STATUS LIKE 'Ssl_cipher'
```

The value of `ssl_cipher` will be non-blank if an encryption cipher is in use. (To make this easier, the version of `exec_stmt_ssl` included in the sample distribution actually issues the statement for you and reports the result.)

## 7.7 Using the Embedded Server Library

MySQL includes an embedded server library, `libmysql` (which contains the MySQL server in a form that can be linked into applications). This enables you to produce MySQL-based standalone applications, as opposed to applications that connect to a client over a network to a separate server program.

To write an embedded server application, two requirements must be satisfied. First, the embedded server library must be installed:

- If you're building from source, enable the library by using the `--with-embedded-server` option when you run `configure`. This applies equally to MySQL 5.0 and 5.1.
- If you want to use a binary distribution, you must use MySQL 5.1 because 5.0 binary distributions do not include `libmysql`. Current versions of 5.1 do include `libmysql`. However, if you use RPM packages, be aware that there is a separate "embedded" RPM that you must install for `libmysql` support.

Second, you'll need to include a small amount of code in your application to start up and shut down the server.

After making sure that both requirements are met, it's necessary only to compile the application and link in the embedded server library (`-lmysql`) rather than the regular client library (`-lmysqlclient`). The design of the server library is such that if you write an application to use it, you can easily produce either an embedded or a client/server version of the application simply by linking in the appropriate library. This works because the regular client library contains interface functions that perform initialization and finalization appropriate to client/server communication rather than to communication with an embedded server.

### 7.7.1 Writing an Embedded Server Application

Writing an application that uses the embedded server is little different from writing one that operates in a client/server context. In fact, if you begin with a program that is written as a client/server application, you can easily convert it to use the embedded server instead. The following procedure describes how to produce an embedded application named emapp, beginning with `exec_stmt.c`:

- 1. Copy `exec_stmt.c` to `emapp.c`. The remaining steps apply to `emapp.c`. (The reason we begin with `exec_stmt.c` rather than `exec_stmt_ssl.c` is that there is no need to use SSL for connections that are set up internally within a single application.)
- 2. Add `mysql_embed.h` to the set of MySQL header files used by the program:

```c
#include <my_global.h>
#include <mysys.h>
```

```c
#include <m_string.h>   /* for strdup() */
#include <mysql.h>
#include <mysql_embed.h>
#include <my_getopt.h>
```

- 3. An embedded application includes both a client side and a server side, so it can process one group of options for the client, and another group for the server. For example, an application named embapp might read the [client] and [embapp] groups from option files for the client part. To set that up, modify the definition of the client_groups array to look like this:

```c
static const char *client_groups[] =
{
  "client", "embapp", NULL
};
```

Options in these groups can be processed by load_defaults() and handle_options() in the usual fashion. Then define another list of option groups for the server side to use. By convention, this list should include the [server] and [embedded] groups, and also the [appname_server] group, where appname is the name of your application. For a program named embapp, the application-specific group will be [embapp_server], so you declare the list of group names as follows:

```c
static const char *server_groups[] =
{
  "server", "embedded", "embapp_server", NULL
};
```

- 4. Call mysql_library_init() before initiating communication with the server, modifying the call so that it passes any options to be processed by the server. A good place to do this is before you call mysql_init().
- 5. Call mysql_library_end() after you're done using the server. A good place to do this is after you call mysql_close().

After making these changes, the main() function in embapp.c looks like this:

```c
int
main (int argc, char *argv[])
{
int opt_err;

MY_INIT (argv[0]);
load_defaults ('my', client_groups, &argc, &argv);

if ((opt_err = handle_options (&argc, &argv, my_opts, get_one_option)))
exit (opt_err);

/* solicit password if necessary */
if (ask_password) 
    opt_password = get_tty_password (NULL);

/* get database name if present on command line */
if (argc > 0)
{
    opt_db_name = argv[0];
    --argc; **argv;
}

/* initialize embedded server library */
if (mysql_library_init (0, NULL, (char **) server_groups))
{
    print_error (NULL, "mysql_library_init() failed");
    exit (1);
}

/* initialize connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
    print_error (NULL, "mysql_init() failed (probably out of memory)");
    exit (1);
}

/* connect to server */
if (mysql_real_connect (conn, opt_host_name, opt_user_name, opt_password,
    opt_db_name, opt_port_num, opt_socket_name, opt_flags) == NULL)
{
    print_error (conn, "mysql_real_connect() failed");
    mysql_close (conn);
    exit (1);
}

while (1)
{
    char  buff[10000];

    fprintf (stderr, "query> ");       /* print prompt */
    if (fgets (buf, sizeof (buf), stdin) == NULL) /* read statement */
        break;
    if (strcmp (buf, "quit\n") == 0 || strcmp (buf, "\\q\n") == 0)
        break;
    process_statement (conn, buf);      /* execute it */
}

/* disconnect from server */
mysql_close (conn);
/* shut down embedded server library */
mysql_library_end ();
exit (0);
```

### 7.7.2 Producing the Application Executable Binary

To produce the embedded-server executable binary for embapp, link in the `-lmysql-d` library rather than the `-lmysqlclient` library. The `mysql_config` utility is useful here. Just as it can show you the flags to use for linking in the regular client library, it also can display the flags necessary for the embedded server:

```bash
% mysql_config --libmysql-d-libs
-L'/usr/local/mysql/lib/mysql' -lmysql-d-lz-lm
```

Thus, to produce an embedded version of embapp, use commands like these:

```bash
% gcc -c -o'mysql_config --include' embapp.c
% gcc -o embapp embapp.o '`mysql_config --libmysql-d-libs`'
```

> Note
> 
> In these commands, you might find it necessary to use a C++ compiler such as `g++` rather than a C compiler.

At this point, you have an embedded application that contains everything you need to access your MySQL databases. However, be sure when you execute embapp that it does not attempt to use the same data directory as any standalone servers that may already be running on the same machine.

Also, under Unix, the application must run with privileges that give it access to the data directory. You can either run embapp while logged in as the user that owns the data directory, or you can make it a setuid program that changes its user ID to that user when it starts. For example, to set embapp to run with the privileges of a user named `mysql`, issue the following commands as root:

```bash
# chown mysql embapp
# chmod 4755 embapp
```

Alternatively, have the embedded application use a different data directory. You can specify the location by placing a `datadir` option in the `[embapp_server]` group of an option file. (The option group for the server half of the application.)

Should you decide that you want to produce a non-embedded version of the application that operates in a client/server context, link it against the regular client library. You can do so by building it like this:

```bash
% gcc -c -o'mysql_config --include' embapp.c
% gcc -o embapp embapp.o '`mysql_config --libs`'
```
