```
# netstat

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address Foreign Address State
tcp 0 0 Styw:1521 Styw:32772 ESTABLISHED
tcp 0 0 Styw:32772 Styw:1521 ESTABLISHED
tcp 0 0 Styw:ssh jsmith.linuxplus.com:4268 ESTABLISHED
tcp 0 0 Styw:1521 rbrown.linuxplus.com:2226 ESTABLISHED
tcp 0 0 Styw:ssh jsmith.linuxplus.com:4801 ESTABLISHED

Active Unix domain sockets (w/o servers)

Proto RefCnt Flags Type State I-Node Path
unix 12 [ ] DGRAM 1401 /dev/log
unix 2 [ ] DGRAM 2449506
unix 2 [ ] DGRAM 2449492
unix 3 [ ] STREAM CONNECTED 69589 /tmp/.X11-unix/X0
unix 3 [ ] STREAM CONNECTED 69588
unix 3 [ ] STREAM CONNECTED 69585 /tmp/.X11-unix/X0
unix 3 [ ] STREAM CONNECTED 69584
unix 3 [ ] STREAM CONNECTED 69569 /tmp/.font-unix/fs7100
unix 3 [ ] STREAM CONNECTED 69568
unix 3 [ ] STREAM CONNECTED 69571 /tmp/.X11-unix/X0
unix 3 [ ] STREAM CONNECTED 69467
unix 2 [ ] DGRAM 67537
unix 3 [ ] STREAM CONNECTED 44683
/var/tmp.oracle/s#1530.1
unix 3 [ ] STREAM CONNECTED 44682
unix 2 [ ] DGRAM 17139
unix 2 [ ] DGRAM 1956
unix 2 [ ] DGRAM 1806
unix 2 [ ] DGRAM 1732
unix 2 [ ] DGRAM 1697
unix 2 [ ] DGRAM 1462
unix 2 [ ] DGRAM 1409
#
```

# FINDING FILES

Even the best organized Linux user will occasionally displace a file. Finding files could take hours without utilities to help. The Linux commands most often used for finding files are whereis, locate, and find.

+   - **whereis** The whereis command locates the source, binary, and manuals for a specified file. It uses a hard coded path to find files, so it may not find every file you are looking for. For example, if you have a user-created script in your home directory, the file will not be found with the whereis command. However, if you move the file to the /bin directory and then execute the whereis command, it will be found.

The whereis syntax is whereis [-sbmu] [-SBM <directory> -f <filename>], where -sbmu is source, directory, manual, or unusual and -SBM is a change or limit to the directories to be searched. To find the startx command use the following command:

```
# whereis startx
startx: /usr/X11R6/bin/startx /usr/bin/X11/startx
#
```

+   - **which** The which command looks through the directories listed in the PATH environment variable for the command requested. For example, if whereis is used to find