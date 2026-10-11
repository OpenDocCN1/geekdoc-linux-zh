If you're using an integrated development environment (IDE), you might not use a Makefile at all. The details will depend on your particular IDE.

# ## 7.2 Connecting to the Server

Our first MySQL client program is about as simple as can be: It connects to a MySQL server, disconnects, and exits. That's not very useful in itself, but you have to know how to do it because you must be connected to a server before you can do anything with a MySQL database. Connecting to a server is such a common operation that code we develop to establish the connection is code you'll use in every client program you write. Besides, this task gives us something simple to start with. The code can be fleshed out later to do something more useful.

Our first client program, connect1, consists of a single source file, connect1.c:

```
```
/*
  connect1.c - connect to and disconnect from MySQL server
*/

#include <cmy_global.h>
#include <cmy_sys.h>
#include <mysql.h>

static char *opt_host_name = NULL;      /* server host (default=localhost) */
static char *opt_user_name = NULL;      /* username (default=login name) */
static char *opt_password = NULL;       /* password (default=none) */
static unsigned int opt_port_num = 0;   /* port number (use built-in value) */
static char *opt_socket_name = NULL;    /* socket name (use built-in value) */
static char *opt_db_name = NULL;        /* database name (default=none) */
static unsigned int opt_flags = 0;      /* connection flags (none) */

static MYSQL *conn;                     /* pointer to connection handler */

int
main (int argc, char *argv[])
{
  MY_INIT (argv[0]);
/* initialize client library */
if (mysql_library_init (0, NULL, NULL))
{
  fprintf (stderr, "mysql_library_init() failed\n");
  exit (1);
}
/* initialize connection handler */
conn = mysql_init (NULL);
if (conn == NULL)
{
  fprintf (stderr, "mysql_init() failed (probably out of memory)\n");
```

```