set 4 restores the commas. It removes any angle brackets inserted by rule set 3 to focus on the host part of the address. It converts any UUCP addresses modified by rule set 3 back to the original form.

+   - Rule set 5 is applied to all local addresses that do not have aliases. If a local address makes it through aliasing without change, it is given to rule set 5, which may select a new delivery agent. Any special rewriting after aliases have been expanded can be done by rule set 5.

# # DEFINING TRUSTED USERS

Trusted users are defined with the T command. Trusted users are allowed to override the sender address using the mailer -f flag. Normally the trusted users are defined to be the root, uucp, daemon and users. The default sendmail.cf file contains the following T commands:

```
Troot
Tdaemon
Tuucp
```

There is generally no need to modify this default list of trusted users. The concept of trusted users was eliminated in sendmail Version 8. If your system uses version 8, then you do not need to define or use trusted users.

# # DEFINING VERSION NUMBER

The configuration file version number is defined using the DZ command. The default version number does not require any modification. However, if you make changes to your sendmail.cf, it is a good idea to keep track of changes you have made by using the version number.

For example, if the version number is initially defined as the following:

```
DZ8.9.3
```

then after making changes to the sendmail.cf file you could change the version number to 8.9.3-1:

```
DZ8.9.3-1
```

# # CONFIGURING SENDMAIL WITH M4

As seen in the last section, directly configuring sendmail by editing the sendmail.cf file is difficult and attempting to do so from scratch would be nearly impossible. Fortunately, sendmail provides a mechanism for configuration through the m4 macro processor.

Using a collection of macros designed for sendmail, you build your configuration files using more concise and clearer directives than any that you find in the sendmail.cf file. For instance, a basic m4 configuration file for a sendmail server can be less than 10 lines:

```
include('../m4/cf.m4')
OSTYPE('linux')
undefine('UUCP_RELAY')
```