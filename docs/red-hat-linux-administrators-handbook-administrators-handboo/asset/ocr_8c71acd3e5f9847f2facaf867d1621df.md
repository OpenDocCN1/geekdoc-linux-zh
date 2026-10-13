@client-b.com @home-town-isp.com

4. Now that you have two virtual user map files, create the final /etc/mail/virtusertable file by using the following commands:

```
touch /etc/mail/virtusertable
```

```
cat *.ftr > /etc/mail/virtusertable
```

The first command creates the /etc/mail/virtusertable file (if it doesn't already exist). The second command concatenates all the FTR files to /etc/mail/virtusertable. This effectively creates the final /etc/mail/virtusertable file.

5. Run the makemap program to create the database version of the file, as follows:

```
makemap hash /etc/mail/virtusertable <
/etc/mail/virtusertable
```

As this example demonstrates, creating multiple virtual user map files can help you keep track of individual domains quite easily. Any time you want to change a domain-specific map, just modify the domain's FTR file and create the final /etc/mail/virtusertable file using the technique just discussed.

Because most mail client programs allow users to set outgoing From: lines to whatever they wish, you may not need to do anything to map outgoing traffic for virtual sites. However, if you want to make sure outgoing mail from users of virtual mail sites translates to their virtual domains, you can use the /etc/mail/genericstable file.

For example, suppose you have a virtual mail site called classified works.com, for which you have an FTR file such as /etc/mail/classified works.ftr, which has the following line:

```
sales@classifiedworks.com sheila
```

The sales@classifiedworks.com address is mapped to a local user called sheila. When sheila sends mail using the sendmail server, you want her mail to appear as sheila@classifiedworks.com, not sheila@your domain.com. In such a case, create a /etc/mail/genericstable file with the following line:

```
sheila sales@classifiedworks.com
```