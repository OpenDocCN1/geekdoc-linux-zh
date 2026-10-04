extra terminals connected to them via serial ports – and this can be the source of another problem. Traditionally, the permissions set on a terminal will allow write access to the terminal special file by anyone. This allows simple messages to be passed around between users using the write command. However, this is precisely the source of the problem with some serial terminals.

For many terminals, it is possible to send simple escape and command character sequences to them which can program them to perform simple actions. It is not uncommon for one of these actions to be to send characters from the terminal back to the host machine, just as though the characters had been typed on the terminal’s keyboard. Given this scenario it is simple to see that a hacker, using the write command, could send a sequence of characters to your terminal which make the terminal send programmed commands back to the computer. These commands will then be executed just as though you had typed them yourself. If you happen to be logged in as root at the time... well, you get the picture.

The only way to protect yourself against an attack of this kind is to remove the public write permission from your terminal line. This can be done with the command:

```
$ mesg n
```

Sadly, removing this potential problem also prevents other users from using write to send you messages, but you can’t have it both ways.

# 14.3 Passwords

It is a true statement that no system can be any more secure than its passwords. When a user attempts to login to your system, a password will be requested. This password will then be encrypted and compared with the previously encrypted version in the file /etc/passwd. If the two encrypted passwords match, the user will be allowed to login to the system. Since the information contained in the password file is generally useful for all sorts of reasons, and since the password itself is securely encrypted, the file has public read access.

So far, so good, but now add the human factor. Most users want a password that is easy to remember – something meaningful to them – their partner’s name, their birthdate, or something similar. Passwords like these are just asking for trouble. They are easy to guess by anyone with only a vague knowledge of you and your friends. When you choose a password, it should be something which includes a mixture of upper and lower case characters, digits and punctuation marks and is hence less likely to be discovered by someone trying to guess what it is. In cases where security is particularly strict the important system passwords should be changed quite frequently and should be shared between as few people as is realistically possible. Obviously, for a system with several users on it, the minimum number of privileged users should take into account the fact that you may be away or ill when one of the users needs something done that requires root access.