After you’ve got the cache directory set up, you’ll probably need to configure the log files (they’re usually misconfigured by default). You set three basic log file names in squid.conf: with cache_access_log, cache_log, and cache_store_log.

Next, search the squid.conf file for the pid_filename line and change it to the following:

```
pid_filename /var/run/squid.pid
```

Now you need to test squid. To detect any remaining problems, run it with the -N option to prevent it from running in daemon mode:

```
# squid -N -d 1
```

You may also need to specify -f file if you’ve put the squid.conf file in a place other than the default. If there are no errors, squid prints a bunch of debugging information:

```
1999/11/13 17:19:46| Starting Squid Cache version 2.2.STABLE5 for i586-pcLinux-gnu...
1999/11/13 17:19:46| Process ID 10231
1999/11/13 17:19:46| With 256 file descriptors available
1999/11/13 17:19:46| Performing DNS Tests...
1999/11/13 17:19:46| Successful DNS name lookup tests...
1999/11/13 17:19:46| helperOpenServers: Starting 5 'dnsserver' processes
1999/11/13 17:19:46| Unlinkd pipe opened on FD 13
1999/11/13 17:19:46| Swap maxSize 51200 KB, estimated 3938 objects
1999/11/13 17:19:46| Target number of buckets: 78
1999/11/13 17:19:46| Using 8192 Store buckets, replacement runs every 10 seconds
1999/11/13 17:19:46| Max Mem size: 8192 KB
1999/11/13 17:19:46| Max Swap size: 51200 KB
1999/11/13 17:19:46| Rebuilding storage in Cache Dir #0 (CLEAN)
1999/11/13 17:19:46| Set Current Directory to ..
..
```

You’ll get your prompt back if an error occurred. If everything appears to be running properly, press CTRL-C; you’ll need to do one more thing before you set up the clients.

# Client Access Lists in squid.conf

Nothing can connect to your proxy server unless you set up access control. You’ll find a few lines in the squid.conf setting up the access control lists; they start with acl. You’ll find this in the default:

```
acl all src 0.0.0.0/0.0.0.0
```