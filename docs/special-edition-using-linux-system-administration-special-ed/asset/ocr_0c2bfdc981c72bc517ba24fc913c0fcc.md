We will describe the process of editing the `sendmail.cf` file to add the address-rewriting rule, and the fax mailer definition. However, there is an easier way of doing this. You can generate a sendmail configuration with HylaFAX mailer support using `m4` macros. An `m4` mailer definition for HylaFAX is included with the sendmail distribution on your Linux system. This process is described further in this chapter in the section “Adding HylaFAX Support to sendmail.cf Using m4.”

# Defining the Address Specification

Fortunately we don’t have to devise a new address specification. One has already been defined and we can just use it. The general format of the email address is `<user>@<number>.<fax>` (`<Full Name of User>`).

For example, to send a fax to user patsmith, whose fax number is 5551212, and full name is Pat Smith, the email address would be `patsmith@5551212.fax` (Pat Smith). The full name between parentheses is optional. It is used on the fax cover sheet. If you send a fax message suppressing the coversheet, the full name is not used.

# Adding an Address-Rewriting Rule

This step requires editing the `sendmail.cf` file. You must add the following address rewriting rule to rule set 0 in `/etc/sendmail.cf`:

```
```text
# forward FAX messages to HylaFAX software
R$+$@.FAX        $#fax $@ $: $1                 user@host.FAX
```
```

In addition, it is necessary to ensure that rule set 3 will not attempt a hostname lookup on FAX addresses. This is achieved by creating a pseudo domain called FAX.

Adding the following line in the `sendmail.cf` file creates the pseudo domain FAX:

```
```text
CPFAX
```
```

# Defining a Fax Mailer

Next edit the `sendmail` configuration file to include the following mailer definition:

```
```text
Mfax, P=/usr/share/fax/mailfax, F=DFMshu, M=100000,
        A=mailfax $u $h $f
```
```

# Writing the mailfax Mailer Script

The last step is to write the mailer script `/usr/share/fax/mailfax`. This is quite simple. This script uses the faxmail program supplied with the HylaFAX distribution. A possible mailfax script is listed below:

```
```sh
#!/bin/sh
/usr/bin/faxmail -n -d "$1" "$2"
```
```

The mailfax script is invoked by sendmail and is passed three arguments: $u, $h, and $f. This default mailfax script does not use the last argument passed by sendmail (the full name). This