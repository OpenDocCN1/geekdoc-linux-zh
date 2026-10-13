# AN EXAMPLE OF A CLIENT-SIDE PROBLEM

A client cannot contact the fax server. You run the `faxstat` program and see output similar to the following:

```
$ faxstat
Can not reach server at host 'faxhost1.bwc.org', port 4559.
```

Make sure the server name is correct. If not, set the proper name of the server in `/usr/share/hyla.conf`, or `.hylac`, or the environment variable FAXSERVER. General network connectivity problems cannot be ruled out. Use ping and other TCP/IP diagnostics programs to verify the remote fax server can be reached from the client.

After fixing the server name, or any network problems, run `faxstat` again and you should see something like the following:

```
$ faxstat
HylaFAX scheduler on orion.bwc.org: Running
Modem ttyS1 (+972 4 833-1029): Running and idle
```

If the output is as shown below then your client is communicating with the server but there is a problem on the server:

```
HylaFAX scheduler on faxhost.bwc.org: Not running.
```

# AN EXAMPLE OF A SERVER-SIDE PROBLEM

If `faxstat` output shows the scheduler is not running such as shown in the faxstat output below, then the `faxq` daemon is either dead or has a problem:

```
$ faxstat
HylaFAX scheduler on orion.bwc.org: Not running
Modem ttyS1 (+972.4.8331039): Running and idle
```

To fix this problem, do a process listing and check whether the `faxq` process is running. If it is not running you can start it by running the following command as the root user:

```
# /usr/sbin/faxq
```

The program will put itself in the background and change its UID to fax.

If the ps output shows faxq is running, but faxstat reports the scheduler is not running, you should check the server tracing log for faxq to see what the problem is. The faxstat communicates with hfaxd on the fax server to get the status information. hfaxd decides if faxq is running based on whether it can open the FIFO special file `/var/spool/fax/FIFO`. Make sure this file is the correct type and has the appropriate permissions. The proper ownership and permissions of the FIFO file are as shown by the following ls listing:

```
# ls -l /var/spool/fax/FIFO
prw------- 1 uucp uucp 0 Mar 22 17:43 FIFO
```

faxq creates the FIFO file when it starts up if it does not already exist. If there is a problem, stop faxq, stop hfaxd, remove the file, and restart faxq and hfaxd using the following commands: