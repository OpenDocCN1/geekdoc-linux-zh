+   MASTER_PORT = n

The TCP/IP port number to use for connecting to the master server.

+   MASTER_SSL = { 0 | 1 }

```
```
MASTER_SSL_CA = 'dir_name'
MASTER_SSL_CAPATH = 'dir_name'
MASTER_SSL_CERT = 'file_name'
MASTER_SSL_CIPHER = 'str'
MASTER_SSL_KEY = 'file_name'
MASTER_SSL_VERIFY_SERVER_CERT = { 0 | 1 }
```
```

These options specify parameters for establishing an SSL connection to the master. They have the same meaning as the corresponding --ssl-xxx options described in Section F.1.2.1, “Standard SSL Options.” The values are saved to the master.info file but have no effect unless the slave has SSL support enabled.

MASTER_SSL_VERIFY_SERVER_CERT was introduced in MySQL 5.1.18.

+   MASTER_USER = 'user_name'

The username of the account to use for connecting to the master server.

+   RELAY_LOG_FILE = 'file_name'

The slave relay log filename.

+   RELAY_LOG_POS = n

The current position within the slave relay log.

Parameters that are not specified in the statement maintain their current values, with the following exception: Changes to MASTER_HOST or MASTER_PORT normally indicate that you're switching to a different master server, so if you specify either of those options, the MASTER_LOG_FILE and MASTER_LOG_POS values are set to the beginning of the master's first binary log file.

You should not mix the MASTER_LOG_FILE and MASTER_LOG_POS options with the RELAY_LOG_FILE and RELAY_LOG_POS options in the same statement.

The CHANGE MASTER statement deletes any existing relay log files and begins a new one unless the RELAY_LOG_FILE or RELAY_LOG_POS options are specified.

# CHECK TABLE

```
```
CHECK { TABLE | TABLES } tbl_name [, tbl_name] ... [option] ...
```
```