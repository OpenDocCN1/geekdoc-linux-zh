```
#Dj$w.Foo.COM
```

If the last of the previous lines is uncommented, the line sets the predefined macro j (the host's canonical fully qualified domain name) to be the value of the class w (the host name only), followed by the domain name (alternatively, the class m if it is defined). Of course, you would want to replace Foo.COM with your domain name. It is recommended that you let sendmail determine the canonical name. The next lines let you configure smart relay and other options:

```
CP.
# "Smart" relay host (may be null)
DS
# operators that cannot be in local usernames (i.e. network indicators)
CO @ % !
# a class with just dot (for identifying canonical names)
C..
# a class with just a left bracket (for identifying domain literals)
C[
```

The preceding DS line could be used to define a smart relay host. Though it is more commonly used with UUCP as a transport mechanism, this can also be useful if the machine doesn't have a reliable connection to the entire network (perhaps it's only on a local network). The relay accepts mail from this machine and handles delivering the mail to the appropriate recipients.

The other lines define class macros that become important within the rewriting rules. The CP. and C.. lines define the classes P and ., each of which consists of only a period (.). The CO @ % ! line defines the class O, which lists three characters that are invalid within user names (@, %, and !). The C[[ line defines the class [, which consists of a left bracket. The next lines identify the virtual user table and the access list database:

```
# Virtual user table (maps incoming users)
Kvrituser hash -o /etc/mail/virtualuser

# Access list database (for spam stomping)
Kaccess hash -o /etc/mail/access
```

The previous Kvrituser and Kaccess lines define two key database files. The Virtual user table database (/etc/mail/virtualuser.db) is created from the hashed output of the /etc/mail/virtualuser text file. The Access list (/etc/mail/access.db) database, created from the /etc/mail/access file, lets you discard and reject e-mail from certain users to prevent spamming. See the sidebar "Forwarding E-mail and Stopping Spamming," which describes how to set up the virtual user and access list databases.