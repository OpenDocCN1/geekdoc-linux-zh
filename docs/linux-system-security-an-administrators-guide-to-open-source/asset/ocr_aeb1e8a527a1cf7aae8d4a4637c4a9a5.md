# Example 13-17  Sample tigrerc File for Daily Use on a Development Machine

```
```
Tiger_Check_PASSWD=Y
Tiger_Check_GROUP=Y
Tiger_Check_ACCOUNTS=Y
Tiger_Check_RHOSTS=Y
Tiger_Check_NETRC=Y
Tiger_Check_ALIASES=Y
Tiger_Check_CRON=Y
Tiger_Check_ANONFTP=N # we check this weekly in another tigrerc
Tiger_Check_EXPORTS=Y
Tiger_Check_INETD=Y
Tiger_Check_KNOWN=Y
Tiger_Check_PERMS=Y
Tiger_Check_SIGNATURE=YES
Tiger_Check_FILESYSTEM=Y
Tiger_Check_PATH=Y
Tiger_Check_EMBEDDED=Y
Tiger_Run_CRACK=N # we check this weekly in another tigrerc
<remainder of file not shown>
```
```

# RUNNING Crack from tiger

Once you have installed Crack on your system (see Chapter 12), you can have tiger run Crack for you automatically. Example 13-18 shows the variables in the tigrerc file that must be edited, and the values required. You also need to edit your site (or site-hostname) file to specify the paths to the required commands, as shown in Example 13-19.

# Example 13-18  Variables in tigrerc File Needed for Crack

```
```
...
Tiger_Run_CRACK=Y
...
Tiger_Collect_CRACK=Y
...
Tiger_Crack_Local=Y
...
Tiger_Mail_Rcpt=root
...
```
```

# Example 13-19  Variables in site File Needed for Crack

```
```
...
CRACKDIR=/usr/local/src/crack/c50a
CRACK=$CRACKDIR/Crack
REPORTER=$CRACKDIR/Reporter
...
```
```

# DECRYPTING tiger OUTPUT

The output messages that tiger generates are labeled with different severities (INFO, WARN, ALERT, FAIL). In most cases, FAIL will indicate a situation where root or another user's data can be compromised. However, the policy