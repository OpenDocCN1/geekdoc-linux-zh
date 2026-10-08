# 374

If you specify the arguments username@hostname2..@hostname or @hostname(@hostname), the request is sent to hostname and forwarded through each hostname-1 to hostname. The program uses the finger information protocol (see RFC 1288) to query the remote host for information about the named user (if you specify a username) or each logged-in user. The information is delivered by server.

As required by RFC 1288, finger passes only printable, 7-bit ASCII data. A system administrator can modify this behavior by using the PASS option in /etc/default/finger. Specifying PASS=low enables all characters less than decimal 32 ASCII. Specifying PASS=high enables all characters greater than decimal 126 ASCII. PASS=low, high or PASS=high, enables both characters less than 32 and greater than 126 to pass.

> Note - The finger user information protocol limits the options that can be used with the remote format of this command.

```
castle% finger winsor@castle
[castle]
Login       Name    TTY      Idle When    Where
winsor      ???     console  Thu 15:38  :0
winsor      ???     pts/3     2 Thu 15:39  :0.0
winsor      ???     pts/4     9 Thu 15:39  :0.0
winsor      ???     pts/5     25 Thu 15:42  :0.0
castle%
```

# Options

+   -b Suppress printing of the user's home directory and shell in a short format print.
-f Suppress printing of the header that is normally printed in a short format print.
-h Suppress printing of the .project file in a long format print.
-i Force idle output format, which is similar to short format except print only the login name, terminal, login time, and idle time.
-l Force long output format.
-m Match arguments only on user name (not first or last name).
-p Suppress printing of the .plan file in a long format print.
-q Force quick output format, which is similar to short format except print only the login name, terminal, and login time.
-s Force short output format.
-w Suppress printing of the full name in a short format print.

# Files

```
$HOME/.plan User's plan.
$HOME/.project
```

User's projects.