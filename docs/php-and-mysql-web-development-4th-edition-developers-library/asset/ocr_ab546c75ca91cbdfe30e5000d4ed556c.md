const char *comment; /* comment */
const char *dir; /* character set directory */
unsigned int mbminlen; /* min. length for multibyte strings */
unsigned int mbmaxlen; /* max. length for multibyte strings */
} MY_CHARSET_INFO;

+   •
+   const char *
+   mysql_get_ssl_cipher (MYSQL *conn);
+   
+   Returns a null-terminated string containing the name of the SSL cipher used for the connection, or NULL if there is no cipher.
+   
+   This routine was introduced in MySQL 5.0.23/5.1.11.

+   •
+   MYSQL *
+   mysql_init (MYSQL *conn);
+   
+   Initializes a connection handler and returns a pointer to it. If the parameter points to an existing MYSQL handler structure, mysql_init() initializes it and returns its address:
+   
+   MYSQL conn_struct; *conn;
+   conn = mysql_init (conn_struct);
+   
+   If the parameter is NULL, mysql_init() allocates a new handler, initializes it, and returns its address:
+   
+   MYSQL *conn;
+   conn = mysql_init (NULL);
+   
+   The second approach is preferable over the first; letting the client library allocate and initialize the handler itself avoids problems that may arise with shared libraries if you upgrade MySQL to a newer version that uses a different internal organization for the MYSQL structure.
+   
+   If mysql_init() fails, it returns NULL. This may happen if mysql_init() cannot allocate a new handler.
+   
+   If mysql_init() allocates the handler, mysql_close() deallocates it automatically when you close the connection.

+   •
+   int
+   mysql_options (MYSQL *conn,
+   enum mysql_option option,
+   const void *arg);
+   
+   This function enables you to tailor connection behavior more precisely than is possible with mysql_real_connect() alone. Call it after mysql_init() and before mysql_real_connect(). You may call mysql_options() multiple times if you want to set several options. If you call mysql_options() multiple times to set a given option, the most recent option value applies.