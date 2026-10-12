n is the number of attempts. For example, the following line disconnects a user from the FTP server after three failed attempts:

```
loginfails 3
```

# ### private

You might find it convenient to share files with other users via FTP without placing the file in a 100% public place or giving these users a real account on the server. The clients use the SITE GROUP and SITE GPASS commands so they can change to privileged groups that require passwords.

To provide your FTP server with this capability, set the private flag by using this command:

```
private switch
```

switch is either YES (to turn it on) or NO (to turn it off).

Because passwords are required for these special groups, you must use the /etc/ftpgroups file. The format of an access group in /etc/ftpgroups follows:

```
access_group_name:encrypted_password:real_group
```

access_group_name is the name the client uses to reference the special group, encrypted_password is the password users need to supply (via SITE GPASS) access the group, and real_group is the actual group referenced in the /etc/group file.

> **Tip**
> 
> To create the encrypted_password entry, use the UNIX crypt function. To simplify generation of the encrypted password, use the following Perl script:

```
#!/usr/bin/perl
srand( time() ^ ($$ + (< $< '15') );
@salts= ('46', .. '57', '65', .. '90', '97', .. '122') ;
print "Enter password to encrypt: ";
chop ($password=<STDIN>);
print "The encrypted password is: ",crypt ( $password,  ( chr ( $salts[int(rand  $salts+1) ] ) .
              ( chr ( $salts[int(rand $salts+1) ] )),  "\n";
```

# ## Controlling Banner Messages

The commands in this section enable you to provide messages to FTP users when they connect to your site or when they specify a special action. These commands are a great way to make your site self-documenting.