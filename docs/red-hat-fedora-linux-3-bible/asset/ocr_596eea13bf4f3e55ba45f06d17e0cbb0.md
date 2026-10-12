| Argument | Description |
| :--- | :--- |
| -t | Perform a syntax check on the configuration files. The results will either be:<br>Syntax OK<br>or an error notification, for example:<br>Syntax error on line 118 of /etc/httpd/conf/httpd.conf |
| -T | Same as -t, except that there is no check of the DocumentRoot value. |
| -V | Print the version information:<br>Server version: Apache/2.0.48<br>Server built: March 17 2004 11:23:11 |
| -V | List the version information and any values defined during compilation:<br>Server version: Apache/2.0.48<br>Server built: March 17 2004 11:23:11<br>Server's Module Magic Number: 20020903:5<br>Architecture: 32-bit<br>Server compiled with...<br>-D APACHE_MPM_DIR="server/mpm/prefork"<br>-D APR_HAS_MMAP<br>-D APR_HAVE_IPV6 (IPV4-mapped addresses enabled)<br><br>-D SERVER_CONFIG_FILE="conf/httpd.conf" |
| -X | Only the single master daemon process is started, and no other httpd processes will be spawned. This should be used only for testing purposes directly from the command line. |

# ## Monitoring Server Activities

Apache provides two unique built-in methods to check the performance of your Web server. The server-status handler can be configured to show information about server processes. The server-info handler can be configured to display a detailed summary of the Web server's