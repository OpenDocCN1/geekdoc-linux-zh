```
## Connecting host must be found in this file; the last match found is
## used, so put defaults first.
##
## <host>          Wildcard name or IP address
## <perm>          R for read; P to post
## <user>          Username for authentication before posting
## <pass>          Password, for same reason
## <groups>        Newsgroup patterns that can be read or not read
## </path/file>    A second file to scan in the same format as this
## To disable posting put a space in the <user> and <pass> fields, since
## there is no way for client to enter one.
##
## Default is no access, no way to authentication, and no groups.
##*:*:*:*:*:*:*
## Foo, Incorporated, hosts have no password, can read anything.
##Foo.com:Read Post:::*
## Bar, Incorporated have a separate access file that they maintain
# *.bar.com:/news/etc/customers/access.bar.com
stdin:Read Post:::*
localhost:Read Post:::*
127.0.0.1:Read Post:::*
```

If you want to allow access to the rest of your domain to all your newsgroups, add the line `*.your.domain.here:Read Post:::*` to the end of the file (substituting your domain name of course).

# Creating the db Files

At this point you need to set up the news database directory (~news/db). To make things easier you should su to your news user; otherwise the files you create will be owned by root and you'll have to change the owner and group IDs on the files manually. You should also have your working directory set to the ~news/db directory, and ~news/bin should be in your PATH so that you can execute INN support commands without typing full pathnames.

To begin, you'll need current active and newsgroups files. These can be downloaded from the following location: `ftp.isc.org:/pub/usenet/CONFIG`

Download the files active and newsgroups and place them in your ~news/db directory.