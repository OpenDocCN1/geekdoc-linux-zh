which can be called with this:

```
xmitemail "Hello" "steev@workaddress.com" "I bet you didn't think this would work!"
```

This command will send the simplistic e-mail shown and can be either invoked by typing it on the command line triggering it from a daily crontab or run as a consequence of some other household event. For example, someone coming through the front door (using the Arduino door mat from Chapter 2) could issue such as e-mail, or it could be sent as a warning when one of the hard disks get too full.

I have subverted the original interface to mail here, because it will be more usual for users to invoke the command in the manner shown earlier. However, there will be times when you want to revert to the original usage of mail by allowing the script to accept any input from STDIN. This requires the three-line replacement shown here to usurp MSG:

```
if [ $# -eq 0 ]; then
    while read LINE ; do
        MSG="$MSG"^M"$LINE"
    done
else
    MSG=$*
fi
```

Note the ^M character, which is entered into editors like vi with Ctrl+V followed by Ctrl+M. Now the message can now be fed in from a file, like this:

```
cat filename | xmitemail "Here's the file" "steev@myworkaddress.com"
```

In Chapter 7, you’ll learn how to extend this functionality to support a basic address book and multiple receivers.

# Autoprocessing E-mails

Accepting e-mails on behalf of a program, instead of a human user, can be summed up in one word: Procmail.⁴ Procmail was a project begun in 1990 by Stephen R. van den Berg to control the delivery of e-mail messages, and although some consider it a dead project, this makes it a stable project and one that’s unlikely to break or introduce new complications any time soon!

Procmail is triggered by the e-mail server (an MTA, such as Exim) by passing each message for further processing to each of a series of recipes. If none of these recipes lays claim to the message, it is delivered as normal.

I’ll begin by creating a simple answer whereby you can e-mail your bedroom light switch. So, create a user with the following, and fill in all the necessary user details:

```
adduser bedroom
```

Then, create a .procmailrc file (note the dot!) in their home directory, and add the following recipe code:

```
:0
* ^From: steev
* ^Subject: light on
|heyu turn bedroom_light on
```

⁴ In the interests of objectiveness, I’ll also admit that maildrop and dovecat exist and perform similar tasks.