# 7.6 Writing Clients That Include SSL Support

exec_stmt_ssl to work properly, MySQL must have been built with SSL support, and the server must be started with the proper options that identify its certificate and key files. You'll also need certificate and key files on the client end. For more information, see Section 13.3, "Setting Up Secure Connections".

The bamp\u0026b distribution contains a source file, exec_stmt_ssl.c, from which the client program exec_stmt_ssl can be built. The following procedure describes how exec_stmt_ssl.c is created, beginning with exec_stmt.c:

+   Copy exec_stmt.c to exec_stmt_ssl.c. The remaining steps apply to exec_stmt_ssl.c.

+   To enable the compiler to detect whether SSL support is available, the MySQL header file my\u005fconfig.h defines the symbol HAVE\u005fOPENSSL appropriately.This means that when writing SSL-related code, you use the following construct so that the code will be ignored if SSL cannot be used:

```
#ifdef HAVE_OPENSSL

SSL-related code here... 

#endif
```

You need not include my\u005fconfig.h explicitly because it is included by my\u005fglobal.h, and exec\u005fstmt\u005fssl.c already includes the latter file.

+   Modify the my\u005fopts array that contains option information structures so that it includes entries for the standard SSL-related options (--ssl-ca, --ssl-key, and so forth). The easiest way to do this is to include the contents of the sslopt- longopts.h file into the my\u005fopts array with an #include directive. After making the change, my\u005fopts looks like this:

```
static struct my_option my_opts[]=  /* option information structures */
{
  {"help", '?', "Display this help and exit", 
   NULL, NULL, NULL},
  GET_NO_ARG, NO_ARG, 0, 0, 0, 0, 0, 0},
  {"host", 'h', "Host to connect to",
   (uchar **) &opt_host_name, NULL, NULL},
  GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"password", 'p', "Password", 
   (uchar **) &opt_password, NULL, NULL},
  GET_STR, OPT_ARG, 0, 0, 0, 0, 0, 0},
  {"port", 'P', "Port number", 
   (uchar **) &opt_port_num, NULL, NULL},
  GET_UINT, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"socket", 'S', "Socket path", 
   (uchar **) &opt_socket_name, NULL, NULL},
  GET_STR, REQUIRED_ARG, 0, 0, 0, 0, 0, 0},
  {"user", 'u', "User_name", 
   (uchar **) &opt_user_name, NULL, NULL},
```