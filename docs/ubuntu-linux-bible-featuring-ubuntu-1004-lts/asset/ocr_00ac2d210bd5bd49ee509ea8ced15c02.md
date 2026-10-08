# Part III: Ubuntu for System Administrators

You'll be prompted for your password and should not see any errors. You can verify that this actually worked by executing the klist command, which provides information about the Kerberos tokens held by the current user and (if all is well) will return something like the following:

```
# klist
Ticket cache: FILE:/tmp/krb5_cc_1000_eVJHEN
Default principal: wnh@VONHAGEN.ORG
```

```
Valid starting Expires Service principal
10/22/08 05:52:52 10/22/08 05:52:52 krbtgt/VONHAGEN.ORG@VONHAGEN.ORG
rew until 10/23/08 05:52:52
```

```
Kerberos 4 ticket cache: /tmp/tkt0
klist: You have no tickets cached
```

If the kinit command returns an error or does not grant valid tickets, you can enable debugging during the Kerberos authentication process to attempt to identify (and then resolve) the problem. To activate debugging, edit your favorite text editor the file /etc/pam.d/common-auth, and add the keyword debug to the end of the corresponding entry, which should then look like the following:

```
auth sufficient pam_krb5.so use_first_pass forwardable debug
```

You can then execute the kinit command and monitor /var/log/auth.log, which should contain information that will help you understand why Kerberos is not working.

Once you have successfully executed the kinit command and see tokens using the klist commands, use the ssh command to try to log in on your Kerberos server via its loopback address as a final test. If this works, log out of the SSH connection, completely log out of your client, and log back in with your Kerberos password. Congratulations—you are using Kerberos!

Kerberos can be very useful as a centralized authentication mechanism, although you will have to create Kerberos principals for every user on your network (i.e., in your Kerberos realm) before they can log in on any client system that you have configured to use Kerberos authentication. Kerberos requires that all of your users have local accounts (because the Kerberos authentication check in /etc/pam.d/common-auth follows the standard pam_unix.so authentication check).

# Summary

This chapter started off explaining the concepts of login users and protection groups on Ubuntu systems. It explained how Linux systems use Pluggable Authentication Modules to verify a user's identity and that a user is authorized to log in at a specific time and perform other authentication-related tasks when logging in on an Ubuntu system. It explained the basics of file