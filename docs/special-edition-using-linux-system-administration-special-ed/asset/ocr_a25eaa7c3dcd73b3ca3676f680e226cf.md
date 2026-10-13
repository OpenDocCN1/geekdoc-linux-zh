These directories all need to have their permissions set to being readable by all users:

```
```bash
# mkdir /var/spool/fax
# cd /var/spool/fax
# mkdir recvq sendq docq log result
# chmod 755 recvq sendq docq log result
```
```

# Create a Fax Configuration Directory

Qfax needs a directory to store its configuration files. Possible locations for this directory include `/conf/fax` and `/etc/conf/fax`. We will use the latter.

Create the directory and then copy the `fax.rc`, `fax.db`, and `cover-template.ps` files from the Qfax source directory to the new configuration directory.

# Configure Qfax

Before compiling Qfax, customize the `config.h` file in the Qfax source directory to meet the specific requirements of your system. This file contains a series of entries of the form:

```
```c
#define variable_name> <value>
```
```

Table 17.1 outlines the variables that need to be set in the `config.h` file.

**Table 17.1 — Variables in the QFAX `config.h` File**

| Variable Name | Description |
|---|---|
| `DATABASE` | The location of the `fax.db` file. If you copied the file to `/etc/conf/fax`, then the value should be `/etc/conf/fax/fax.db`. |
| `CONFIG` | The location of the `fax.rc` file. If you copied the file to `/etc/conf/fax`, then the value should be `/etc/conf/fax/rc`. |
| `TEMPLATE` | The location of the `cover-template.ps` file. If you copied the file to `/etc/conf/fax`, then the value should be `/etc/conf/fax/cover-template.ps`. |
| `FAXQUEUE` | The directory created for storing outgoing faxes (in this case, `/var/spool/fax/sendq`). |
| `STOREDIR` | The directory for storing inactive faxes (in this case, `/var/spool/fax/docq`). |
| `FAXSCRIPT` | The location of the `Elax` fax script (usually, `/usr/bin/fax`). |
| `RESULT` | The filename which should contain the status of the last attempt to send a fax (in this case, `/var/spool/fax/result/result`). |
| `LS` | Your `ls` command (usually this is just `ls`). |
| `MAXFAXES` | The maximum number of faxes which should be stored in the outgoing fax queue (the default value is 15). |
| `MAXTRIES` | The maximum number of times to attempt sending a failed fax before giving up (the default value is 3). |