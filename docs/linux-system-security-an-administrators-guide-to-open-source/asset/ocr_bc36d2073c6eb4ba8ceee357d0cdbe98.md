If keyinit is to be run without the -s flag (see Example 6-6 on page 125), it must be executed locally on the server because it requires the secret password (and, once again, you don't want the secret password passing over the network).

The keyaudit Script The keyaudit script, found in /usr/src/skey/tools, is a bourne shell script that checks on the remaining number of OTP passwords for each user found in /etc/skeykeys. If a user has 11 or fewer remaining one-time passwords, then keyaudit will send an e-mail message to the administrator reminding him or her to generate a new list for the user or users whose lists are growing short. You will need to modify the keyaudit script in order to get it to work on Linux. Change the line

```
HOST='/usr/ucd/hostname'
```

to

```
HOST='/bin/hostname'
```

You will also need to change the ADMIN variable in the script to someone who reads their mail and will act upon a message from keyaudit. For example, if the user bill is the administrator, we would change the line

```
ADMIN=chasin
```

to

```
ADMIN=bill
```

and the keyaudit script will work. The keyaudit script will also accept a numeric argument for the number of OTPs remaining. For example, you could execute keyaudit 15, and it will then look through /etc/skeykeys for all users with a sequence number of 14 or less in the /etc/skeykeys file. Remember, the sequence number in the /etc/skeykeys file is one greater than the actual number of remaining one-time passwords in the user's list. If the sequence number found is strictly less than three, the subject line in the e-mail will reflect the important nature of the message. You may set up keyaudit in cron to run regularly.

Using the Version 1.1b Replacement Programs Up to this point we have looked at using keysh only to ubiquitously invoke the S/Key system. This is a valid approach in many cases. It is also a valid approach for all users who are not allowed to log in at the console.

You may instead or additionally want to use one of the S/Key-aware replacement programs found in the /usr/src/skey/misc directory. As previously noted, they are su, login, and ftpd. If you are using PAM (and you should be), you probably don't want to use these programs. However, if you choose or need to use one or more of them, you may compile them and replace the original binaries. We will not detail this procedure for S/Key Version 1.1b;