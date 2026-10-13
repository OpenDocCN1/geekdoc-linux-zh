# Configure Postfix Authentication

When authentication is configured in Postfix, user limits can apply. But as there are no hints in the standard main.cf configuration file, you'll have to refer to Postfix documentation for clues. As suggested in Chapter 3, most packages include some level of documentation in the /usr/share/doc directory. Fortunately, Postfix documentation in that directory is rather extensive. For RHEL 6, you'll be able to find that documentation in the postfix-2.6.6/ subdirectory.

The directives that you need to add to the main.cf file to set up authentication are shown in the README-Postfix-SASL-RedHat.txt file in that directory. The key excerpt is shown in Figure 13-4.

For the first step listed, it's sufficient to copy the four directives listed to the end of the main.cf file, first to enable SASL authentication for Postfix connections:

```
smtpd_sasl_auth_enable = yes
```

Next, this disables anonymous authentication:

```
smtpd_sasl_security_options = noanonymous
```

# FIGURE 13-4 Quick Start to Authenticate with SASL and PAM:

Directions to set up Postfix authentication

If you don't need the details and are an experienced system administrator you can just do this, otherwise read on.

+   1) Edit /etc/postfix/main.cf and set this:
+   
+   smtpd_sasl_auth_enable = yes
+   smtpd_sasl_security_options = noanonymous
+   broken_sasl_auth_clients = yes
+   
+   smtpd_recipient_restrictions =
+   permit_sasl_authenticated,
+   permit_mynetworks,
+   reject_unauth_destination
+   
+   2) Turn on saslauthd:
+   /sbin/chkconfig --level 345 saslauthd on
+   /sbin/service saslauthd start
+   
+   3) Edit /etc/sysconfig/saslauthd and set this:
+   
+   MECH=pam
+   
+   4) Restart Postfix:
+   /sbin/service postfix restart