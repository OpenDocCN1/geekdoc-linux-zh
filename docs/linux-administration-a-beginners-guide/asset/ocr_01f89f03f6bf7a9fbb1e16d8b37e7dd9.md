| Field | Description |
| --- | --- |
| Options | This field decides whether this filter is going to compress, uncompress, or tar files. Each option is represented by O_COMPRESS, O_UNCOMPRESS, and O_TAR, respectively. You can do multiple things to a file at once by using the pipe (I) symbol between commands. For example, O_COMPRESS|O_TAR means that this filter will both compress and tar a client request. |
| Desc | This is a freeform field that allows you to describe what the filter does. |

Table 13-2 Fields of the /etc/tftp/conversions File (continued)

The first two parameters (strip prefix and strip postfix) are not necessary since we are not taking anything away from the filename. The third parameter (add-on prefix) doesn’t apply since we do not want to add anything to the beginning of the filename. The fourth parameter, gz (add-on postfix), specifies that the filename should have .gz appended to it after this filter is done executing. The fifth parameter (external command) specifies the exact invocation of the gzip program in order to perform the file compression. Notice that %s is used instead of a filename. The sixth parameter (type of file) tells wu-ftpd that it can perform compression on both straight ASCII as well as regular files. The seventh parameter, O_COMPRESS (the options field), tells the server that the file action being performed is compression. Finally, the last field is a simple human readable reminder of what this filter does: run gzip.

Although this appears intimidating, don’t worry about it! It is unlikely you’ll need to change the default configuration file that comes with wu-ftpd since it covers the most popular conversions.

# Configuring Host Access

The /etc/ftphosts file allows you to explicitly allow or deny users based on their originating IP address. Each line in the file can take the form

```
```
allow username address
```
or
```
deny username address
```
```

Where username is the login they use when connecting to the FTP service, and address is the originating IP address. You can list multiple addresses in a comma-separated list.