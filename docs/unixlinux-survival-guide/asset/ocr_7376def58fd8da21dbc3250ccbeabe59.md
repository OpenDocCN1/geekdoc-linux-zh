If you execute the program, the output should display the lines contained in the /etc/passwd on your system (the output shown in Listing 2.19 is shortened for this example).

# LISTING 2.19 Output of the Perl Script

```
erikk@unixhost:> ./ulist1.pl
root:x:0:1:Super-User::/sbin/sh
daemon:x:1:1:::
bin:x:2:2::/usr/bin:
sys:x:3:3::
adm:x:4:4:Admin:/var/adm:
lp:x:71:8:Line Printer Admin:/usr/spool/lp:
uucp:x:5:5:uucp Admin:/usr/lib/uucp:
nuucp:x:9:9:uucp Admin:/var/spool/uucppublic:/usr/lib/uucp/uucico
smmsp:x:25:25:SendMail Message Submission Program::
listen:x:37:4:Network Admin:/usr/net/nls:
nobody:x:60001:60001:Nobody::
noaccess:x:60002:60002:No Access User::
nobody4:x:65534:65534:SunOS 4.x Nobody::
erikk:x:101:10::/export/home/users/erikk:/bin/sh
```

The result in Listing 2.19 obviously lacks clarity. It contains information you don't need for the purpose of the program, for example, which shell will be started after the login of the respective user. A colon separates the fields, and the fields containing the information you are looking for are field 1 and field 3. To access the contents of these fields, Perl provides the function split. It requires two parameters: the field-separator, in this case :, and the name of the variable to be split up, $_, as shown in Listing 2.20.

# LISTING 2.20 Splitting the Records into Fields

```
#!/usr/bin/perl
# $Id$
#
################################################################
#
#   file:      ulist1.pl
#
#   purpose:   lists all users
#              and their respective IDs
#
#   author:    Erik Keller
```