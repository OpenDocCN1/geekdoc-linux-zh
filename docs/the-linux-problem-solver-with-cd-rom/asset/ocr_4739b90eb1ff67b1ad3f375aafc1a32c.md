Amanda Backup Client Hosts Check
Client check: 3 hosts checked in 1.029 seconds, 0 problems found.

(brought to you by Amanda 2.4.1p1)

The first part, the server host check, looks at the tape loaded in the tape drive and the configuration to see if the backup will record properly. The client hosts check simply connects to the hosts you're backing up to see if they are ready. Errors involving nonexistent files and directories will probably crop up, so create them (with touch and mkdir) and run amcheck until they go away.

> **PROBLEM 98**
> 
> **Symptom:** Client host denies access.
> 
> **Problem:** Host access.
> 
> **Fix:** By default, Amanda looks at the .rhosts file of the Amanda user's directory on the client machine to see if the client has access. You can use `--with-amandahosts` to configure Amanda to use an .amandahosts file if you don't want it to use the .rhosts file. Make sure that you specify only the tape server in your .amandahosts file and that your server is secure. If you want better authentication, a `--with-krb4-security` option allows Kerberos 4 authentication.

# Backing Up with amdump

Once everything passes amcheck, you're ready to try a backup with amdump.

```
# amdump servers
```

instructs Amanda to dump the directories you specified in the disklist file to tape. If this is the first time you've done this, a full backup takes place, and the process might last a while if you have an extensive disklist file.

If the backup seems to have gone all right, look in the directory to which you set logdir in amanda.conf. You should see at least one log file in there named log.yyyymmdd.n, yyy being the year, mm the month, and dd the day. n is most likely 0 (in different installations log files created by different Amanda runs on the same day). Look at the log file to get familiar with the format and to see if there are any errors.