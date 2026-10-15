The following command recursively copies your entire home directory on the 122.147.110.17 host to your current directory on the local machine. Don't forget to type the period after the space character after ~.

```
% scp -r 122.147.110.17:~ .
Password: xxxxxx
temp                          100%    0     0.0KB/s   00:00
.profile                      100%  568     0.6KB/s   00:00
.local.login                  100%  170     0.2KB/s   00:00
welcomesir                    100%  139     0.1KB/s   00:00
known_hosts                   100%  397     0.4KB/s   00:00
scp: /export/home/sarwar/.bash_history: Permission denied
.local.cshrc                  100%  166     0.2KB/s   00:00
ps.man                        100%  28KB   27.9KB/s   00:00
bigdata                       3%  327MB  11.2MB/s   12:35 ETA
<Ctrl+C> Killed by signal 2.
%
```

Note that we terminate the command with <CTRL+C>, as can be seen on the last line of the command output.

# 11.8.10.4 The sftp Command

The sftp command is the secure version of the ftp command. It works just like the ftp command except that stronger authentication takes place before file transfer takes place, and transfer takes place in encrypted sessions. The following sessions show sample commands executed in sftp.

Connecting and getting help

```
% sftp 192.168.0.12
Password: xxxxxx
Connected to 202.147.169.197.
sftp> ?
Available commands:
bye                          Quit sftp
cd path                      Change remote directory to 'path'
chgrp grp path               Change group of file 'path' to 'grp'
chmod mode path              Change permissions of file 'path'
                             to 'mode'
chown own path               Change owner of file 'path' to 'own'
df [-hi] [path]              Display statistics for current
                             directory or filesystem containing
                             'path'
exit                         Quit sftp
get [-Ppr] remote [local]    Download file
reget remote [local]         Resume download file
```