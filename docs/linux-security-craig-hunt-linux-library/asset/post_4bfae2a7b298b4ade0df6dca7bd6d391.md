
## NOTE
If you choose to accept the installation directory default of `/usr/TSS`, you should at least include `/usr/TSS/bin` in your `PATH` environment variable if you want to execute `tripwire` commands without supplying a fully qualified file path. Do not include this path in root’s `PATH` variable, however. You may also want to include `/usr/TSS/man` in your `MANPATH` environment variable so you can display the supplied man pages.

# Configuring Tripwire

Once the package has been installed in the appropriate directory, you must create a configuration file, as well as a default policy, that will also be stored in a text file. After these two files are created, use the `twadmin` utility to encode and sign both files to ensure that their contents are not modified. The next step is to initialize the signature database, which allows you to run your first integrity check.

The following sections explain in more detail the process of creating a `tripwire` configuration file and a policy file.

# The Tripwire Configuration File

The `tripwire` configuration file is typically found at the following location:

`${ROOT}/bin/twcfg.txt`

The purpose of this configuration file is to control the location of all the other files in the `tripwire` distribution after it has been installed. Listing 3.6 contains the default contents of the file.

### Listing 3.6 Initial contents of the tripwire configuration file (twcfg.txt)

```text
ROOT           =/usr/TSS
POLFILE        =/usr/TSS/policy/tw.pol
DBFILE         =/usr/TSS/db/${HOSTNAME}.twd
REPORTFILE     =/usr/TSS/report/${HOSTNAME}-${DATE}.twr
SITEKEYFILE    =/usr/TSS/key/site.key
LOCALKEYFILE   =/usr/TSS/key/redhat.example.com-local.key
EDITOR         =/bin/vi
LATEPROMPTING  =false
LOOSEDIRECTORYCHECKING =false
MAILNOVIOLATIONS =true
EMAILREPORTLEVEL =3
REPORTLEVEL    =3
MAILMETHOD     =SENDMAIL
SYSLOGREPORTING =false
MAILPROGRAM    =/usr/lib/sendmail -oi -t
```

If you specified a custom value for TWROOT before the installation, the paths in this file should reflect that fact. Note that the first six variables in the twcfg.txt file are needed for tripwire operation, while the rest are optional. Table 3.3 contains a description of the environment variables in this file that are different from the ones in the installation configuration (see Table 3.2 for those). Unless you have a very specific need to do so, I recommend that you do not change the default contents of this configuration file.

### Table 3.3 tripwire twcfg.txt Environment Variables

| Variable | Description |
| :--- | :--- |
| EDITOR | Editor for interactive reports. |
| LATEPROMPTING | Delay the prompting of the passphrase to minimize exposure. |
| LOOSEDIRECTORYCHECKING | Don't check file for properties that are likely to change often. |
| MAILNOVIOLATIONS | Send e-mail report even if no violations occurred. |
| EMAILREPORTING_LEVEL | Default verbosity level of e-mail report (0 through 4). |
| REPORTLEVEL | Default verbosity level of printed report (0 through 4). |
| MAILMETHOD | Choice of mail transport (SMTP or Sendmail). |
| SYSLOGREPORTING | Send user.notice reports through syslog. |
| MAILPROGRAM | Program invoked for mailing Tripwire violation reports. |

The next section describes the syntax and maintenance of the policy file and the last steps needed to get tripwire up and running.

# The Tripwire Policy File

Now that you have defined the operational parameters of tripwire, you're ready to tell it which files to watch. This is done in the policy file, which is located by default in `/usr/TSS/policy/twpol.txt`.

A typical tripwire policy file has three distinct sections:

- Global definitions of variables whose scope includes the entire policy file
- File severity levels that allow you to prioritize the execution of policies
- Rules or group of properties to be checked for each file or object

Consider the sample (partial) policy of the tripwire policy file (twpol.txt) in the examples in this section. This example contains the global variables that determine the location of the tripwire root directory (TWROOT), binary directory (TWBIN), policy (TWPOL), database (TWDB), key files (TWKEY, TWLKEY), and report (TWREPORT).

```
@section GLOBAL
  TWROOT="/usr/TSS";
  TWBIN="/usr/TSS/bin";
  TWPOL="/usr/TSS/policy";
  TWDB="/usr/TSS/db";
  TWKEY="/usr/TSS/key";
  TWLKEY="/usr/TSS/key";
  TWREPORT="/usr/TSS/report";
  HOSTNAME=redhat.example.com;
```

The next example shows the file security level section of the tripwire policy file. This example defines a number of macros to be used later in the policy. It uses several built-in property masks that tell the policy which events to examine or ignore (IgnoreNone, ReadOnly, Dynamic, Growing), as well as some user-defined property masks (#ug, 33, 66, 100). These masks direct tripwire to look for certain types of changes in a given file or directory. (See Table 3.4 for a complete list of the characters used in tripwire’s property masks.)

```
@section FS
SEC_CRIT = $(IgnoreNone)-Sha; # Critical files - we can't
# afford to miss any changes.
SEC_SUID = $(IgnoreNone)-Sha; # Binaries with the SUID or SGID
# flags set.
SEC_TCB = $(ReadOnly); # Members of the Trusted
# Computing Base.
SEC_BIN = $(ReadOnly); # Binaries that shouldn't
# change.
SEC_CONFIG = $(Dynamic); # Config files that are changed
# infrequently but accessed
# often.
SEC_LOG = $(Growing); # Files that grow, but that
```

```
SEC_INVARIANT = +pg;

SIG_LOW = 33;  # Non-critical files that are # of minimal security impact.

SIG_MED = 66;  # Non-critical files that are # of significant security impact.

SIG_HI = 100;  # Critical files that are # significant points of # vulnerability.
```

### Table 3.4 tripwire Policy File Property Mask Characters

| Property | Description |
| :--- | :--- |
| - | Ignore properties |
| + | Record and check properties |
| p | File permissions |
| I | Inode number |
| n | Number of links |
| u | User id of file owner |
| g | Group id of file owner |
| t | File type |
| s | File size |
| l | File is expected to grow |
| d | Device number of disk |
| I | Device number to which inode points |
| b | Number of blocks allocated |
| a | Access timestamp |
| m | Modification timestamp |
| c | Inode creation/modification timestamp |
| c | Cyclic redundancy check |

The Tripwire Binaries rule instructs *tripwire* to watch the binaries themselves and tag any violation with the highest severity value:

```
# Tripwire Binaries

(rulename = "Tripwire Binaries", severity = $(SIG_HI))
{
  $(TWBIN)/sigs    -> $(ReadOnly);
  $(TWBIN)/tripwire    -> $(ReadOnly);
  $(TWBIN)/twadmin    -> $(ReadOnly);
  $(TWBIN)/twprint    -> $(ReadOnly);
}
```

The Tripwire Data Files rule also instructs *tripwire* to watch the policy configuration and key files. Note that in the file severity section earlier, SEC\_BIN was defined to be ReadOnly, so you're telling *tripwire* that the policy, configuration, and key files should not change at all. Here's an example of the Tripwire Date Files rule:

```
# Tripwire Data Files - Configuration Files, Policy Files, Keys, Reports, Databases

(rulename = "Tripwire Data Files", severity = $(SIG_HI))
{
  $(TWDB)    -> $(Dynamic) -i;
  $(TWPOL)/tw.pol    -> $(SEC_BIN) -i;
  $(TWBIN)/tw.cfg    -> $(SEC_BIN) -i;
```

```
$ (TWLKEY) / $(HOSTNAME) -local.key -> $(SEC_BIN) ;
$ (TWSKEY) /site.key -> $(SEC_BIN) ;

#don't scan the individual reports
$ (TWREPORT) -> $(Dynamic) (recurse = 0) ;
}
```

Make sure to define rules to monitor the integrity of the policy directory, the key files, and the reports, as in the previous example. Note that the content of the report files is considered to be dynamic, and the recurse=0 directive instructs tripwire not to go into any of the report subdirectories.

The following is an example of a medium severity rule that defines a set of files that can change on a regular basis, but must retain their user and group ownership:

```
# Commonly accessed directories that should remain static with regards to owner and group

(rule name = 'Invariant Directories' , severity = $(SIG_MED))
{
/ -> $(SEC_INVARIANT) (recurse = 0) ;
/home -> $(SEC_INVARIANT) (recurse = 0) ;
/etc -> $(SEC_INVARIANT) (recurse = 0) ;
}
```

After you have edited the textual policy file to make any necessary additions or modifications, encrypt it and sign it with the following command:

```
[ramon]$ sudo /usr/TSS/bin/twadmin --create-policy
/usr/TSS/policy/twpol.txt
```

This results in the creation of a binary file called `/usr/TSS/policy/tw.pol`. At this point, you have a valid configuration file and an initial policy file in place.

The next section explains how to initialize the tripwire database and how to start using the application.

# Running Tripwire

You're almost ready, but before you start comparing file signatures to look for tampering, you need to snap a baseline of what the signatures should look like on all the files in your policy. This takes place when you first initialize the signature database using the following command:

```
[ramon]$ /usr/TSS/bin/tripwire --init
```
