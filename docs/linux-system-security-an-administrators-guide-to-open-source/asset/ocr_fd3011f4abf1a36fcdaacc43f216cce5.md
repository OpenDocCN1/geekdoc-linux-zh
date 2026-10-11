# **Example 14-8 Running tripwire in Compare Mode**

```
```
# tripwire -c /usr/local/ro/etc/tw.config.linux -d \
/usr/local/ro/bin/twdg.topcat
### Phase 1:  Reading configuration file
### Phase 2:  Generating file list.
### Phase 3:  Creating file information database
### Phase 4:  Searching for inconsistencies

###                 Total files scanned:         12512
###                 Files added:                  2
###                 Files deleted:                 0
###                 Files changed:               10657

###              After applying rules:
###              Changes discarded:               10656
###              Changes remaining:                5

changed: drwxr-xr-x root          4096 Mar 29 16:03:50 1999 /usr/sbin
changed: -rwxr-Xr-x root         44530 Mar 29 16:04:04 1999 /usr/sbin/imapd
### Phase 5:  Generating observed/expected pairs for changed files

###     Attr        Observed (what it is)     Expected (what it should be)
/usr/sbin ========... ========... ========... ========... ========... ========
        st_ctime: Mon Mar 29 16:03:50 1999    Thu Mar 11 15:43:10 1999
/usr/sbin/imapd
        st_size:  44530                   504580
        st_ctime: Mon Mar 29 16:04:04 1999  Sun Jan 31 05:03:45 1999
        m5 (sigl): 2EH8ABcB=CqOuhpalJxTT  ZfDCxrJiR;F#i$D#lj$y
        snefru (sig2): 30KgG2dJn3fj.AX3DABOz58     2KqGEGqji#k88eOVdmL3Hw5
```
```

Clearly, if you have many systems, the manual execution of Tripwire in compare mode will not do. Perhaps the best way to manage Tripwire runs is to use scripts and cron. The bash script in Example 14-9 (line numbers added for clarity) illustrates a script that automates Tripwire checks. We assume that the configuration file and database are located on a read-only filesystem that we access locally via NFS. Further, we assume that both the configuration file and database are encrypted with PGP.

# **Example 14-9 Automating Tripwire Compare Runs**

```
```
 1.  #!/bin/bash
 2.  #
 3.  # Decrypt tw database and run tripwire
 4.  #
 5.  # Call me paranoid
 6.  umask 077
 7.  # Set up PGP file descriptor
 8.  PGPPASSFD=0;export PGPPASSFD
 9.  # Set up pipe for encryption
10.  CPIPE=/root/.cpipe
11.  # Set up pipe for config file
12.  TPIPE=/root/.tpipe
13.  # Make & get restrictive permissions for the pipes
14.  mknod -m u=rw,go= $CPIPE p
15.  mknod -m u=rw,go= $TPIPE p
16.  #
```
```