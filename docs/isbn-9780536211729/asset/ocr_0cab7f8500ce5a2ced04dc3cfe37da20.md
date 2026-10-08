were also broken into, using the compromised passwords or other data compromised from the original system.

> Back in my student days at Berkeley, an early and experimental UNIX networking facility, that was the forerunner of rsh, required the remote system’s password to be stored in clear text. Yup. Someone broke into one of the Computer Center’s UNIX systems and I had to assume that this password was compromised. Even though it was the one that Ken Thompson could not crack and it was easy to remember, I do not use it to this day!

You must assume that any other data was compromised and take appropriate action. This includes any customer and vendor data, such as credit card numbers. A variety of techniques can make use of this information to commit theft. This one is common and relies on the criminal having enough information to convince the victim that he is who he says he is. “Hi. I’m from Pentacorp and we accidentally deleted our copy of your credit card number on your order of September 29 for 100 widgets to be shipped to you at 123 Maple Street. If you can give it to me now, we can ship today.” Even though you protect customer credit card numbers, this thief got the data anyway and applied charges to your customer’s card.

A failure to notify has liability implications. Publicity has other implications. It is best to have an approved written plan prior to the breach, because you will want to act quickly and do not want to risk being the scapegoat by getting accused of taking the wrong action in the heat of battle.

# 13.14 Finding set-UID Programs

Many crackers will leave behind back doors, so that they may get back into your system more easily. The least sophisticated and most detectable way is to leave behind a set-UID program. This simply is a program owned by root with the set-UID bit set. This can be done by a cracker operating as root in only 10 seconds via

```
cp /bin/sh /tmp/.foo
chmod 4755 /tmp/.foo
```

Is this an effective strategy? How recently have you scanned for set-UID programs? You can (and should) detect if this has been done with a simple compare command:

```
ls -l /bin/sh /tmp/.foo
cmp /bin/sh /tmp/.foo
```

A cracker can prevent this by adding the command

```
date >> /tmp/.foo
```