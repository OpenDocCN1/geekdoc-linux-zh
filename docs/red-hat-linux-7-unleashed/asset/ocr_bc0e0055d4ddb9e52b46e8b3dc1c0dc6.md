CHAPTER 17

# The [global] Section

The [global] section controls parameters for the entire SMB server. It also provides default values for the other sections:

```
```
[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP

Workgroup= specifies the workgroup. Try to keep it all uppercase, fewer than nine char-
acters and without spaces.

# server string is the equivalent of the NT Description field
server string = Samba Server

server string= specifies a human-readable string used to identify the server in the
client's user interface. server string= goes in the [global] section. Note the similarity
to the comment= option, which identifies individual shares in the client's user interface.

; hosts allow = 192.168.1. 192.168.2. 127.

If uncommented, the hosts allow= line restricts Samba access to certain subnets: a
handy security measure. Multiple subnets are separated by spaces. Class C subnets have
three numbers and three dots, class B two numbers and two dots, and class A one num-
ber and one dot.
```


```

```
```
# if you want to automatically load your printer list rather
# than setting them up individually then you'll need this
printcap name = /etc/printcap
load printers = yes

The preceding enables printing without fuss, and is un commented by default.

# It should not be necessary to spell out the print system type unless
# yours is non-standard. Currently supported print systems include:
# bsd, sysv, plb, lprng, aix, npux, qnx
;
printing = bsd
```


```

It should not be necessary to uncomment the preceding code on a Red Hat Linux server.

```
```
# Uncomment this if you want a guest account, you must add this to /etc/passwd
# otherwise the user 'nobody' is used
;
guest account = pguest
```


```

The preceding, if uncommented, defines a guest account for clients logged in as a user not known to the Samba server.

```
```
# Password Level allows matching of \_n\_ characters of the password for
# all combinations of upper and lower case.
;
password level = 8
username level = 8
```


```