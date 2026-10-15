# The Results

Let's see what happens when you invoke this script without any arguments versus invoking sftp without any arguments. Listing 4-10 shows running sftp.

```
$ sftp
usage: sftp [-1246Cpqrv] [-B buffer_size] [-b batchfile] [-c cipher]
[-D sftp_server_path] [-F ssh_config] [-i identity_file] [-l limit]
[-o ssh_option] [-P port] [-R num_requests] [-S program]
[-s subsystem] sftp_server host
sftp [user@]host[:file ...]
sftp [user@]host[:dir/]
sftp -b batchfile [user@]host
```

Listing 4-10: Running the sftp utility with no arguments yields very cryptic help output.

That's useful but confusing. By contrast, with the mysftp script you can proceed to make an actual connection, as Listing 4-11 shows.

```
$ mysftp
User account: taylor
Remote host: intuitive.com
Connecting to intuitive.com...
taylor@intuitive.com's password:
sftp> quit
```

Listing 4-11: Running the mysftp script with no arguments is much clearer.

Invoke the script as if it were an ftp session by supplying the remote host, and it'll prompt for the remote account name (detailed in Listing 4-12) and then invisibly invoke sftp.

```
$ mysftp intuitive.com
User account: taylor
Connecting to intuitive.com...
taylor@intuitive.com's password:
sftp> quit
```

Listing 4-12: Running the mysftp script with a single argument: the host to connect to

# Hacking the Script

One thing to always think about when you have a script like this is whether it can be the basis of an automated backup or sync tool, and mysftp is a perfect candidate. So a great hack would be to designate a directory on your system, for example, then write a wrapper that would create a ZIP archive of key files, and use mysftp to copy them up to a server or cloud storage system. In fact, we'll do just that later in the book with Script #72 on page 229.