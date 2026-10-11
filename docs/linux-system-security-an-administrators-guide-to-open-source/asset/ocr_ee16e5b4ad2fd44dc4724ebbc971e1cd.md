**Table 6.1 S/Key and OPIE Command and File Comparison**

| S/Key Commands and Files | OPIE Commands and Files |
| :--- | :--- |
| keyinit | opiepasswd |
| key | opiekey |
| keyinfo | opieinfo |
| /etc/skeykeys | /etc/opiekeys |
| /etc/skey.access (v2.2) | /etc/opieaccess |


Version 1.1b and OPIE offer replacement programs for su, login, and ftpd. OPIE does not provide an equivalent to keysh nor to keyaudit.

# Oh, By The Way...

It is very simple to modify the keyaudit script to work with OPIE, and it is well worth the effort. Change the following lines in keyaudit (in addition to those already mentioned in The keyaudit Script on page 131) from

```
```text
KEYDB=/etc/skeykeys
SECHO "Type \\`keyinit-s' to reinitialize your sequence number."
```
```

to

```
```text
KEYDB=/etc/opiekeys
SECHO "Type \\`opiepasswd' to reinitialize your sequence number."
```
```

and change all references of S/Key to OPIE. You may also want to rename the script to opieaudit. For the tightest security, set the permissions on the script to 500 and make it owned by root. Don't forget to put it in cron!

# Obtaining and Installing OPIE

As of this writing, the current version of OPIE is 2.32. It may be obtained from

```
`ftp://ftp.innert.net/pub/opie/`
```

Unfortunately, once again, there is no digital signature associated with the gzipped tar file. The file you obtain will be named something like opie-2.32.tar.gz. The first step is to apply gunzip, then use tar to extract the files. This will create a subdirectory, opie-2.32. For our examples, we'll assume that the OPIE files are in /usr/src/opie-2.32.

The OPIE Version 2.32 distribution uses the GNU autoconfiguration utility configure which is used to automatically configure a Makefile for your system. For more information about this utility, check your system documentation and the references noted in *For Further Reading* on page 148.