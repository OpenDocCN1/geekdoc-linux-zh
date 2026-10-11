the owner of the Public User Key. So, make sure and enter a passphrase! A good range of characters for the passphrase is 10 to 20; the passphrase should not be simple English (or other language) prose as this might be guessed easily. Be sure to remember it because, if you forget it, you will have to regenerate and redistribute your keys. If you do not enter a passphrase, the Private User Key will not be encrypted. Note that the passphrase typed in at the Enter **passphrase:** and Enter the same **passphrase again:** prompts are not echoed back to the screen. After the passphrase is entered, `ssh-keygen` displays the Public User Key and reports that it has been stored in `$HOME/.ssh/identity.pub`.

# Example 11-19 Generating User Keys with `ssh-keygen`

```
```
[paul@underdog paul]$ ssh-keygen
Initializing random number generator...
Generating p: ................................................++ (distance 290)
Generating q: ...............................................++ (distance 476)
Computing the keys ...
Key generation complete.
Enter file in which to save the key (/home/paul/.ssh/identity): 
Enter passphrase:
Enter the same passphrase again:
Your identification has been saved in /home/paul/.ssh/identity.
Your public key is:
1024 35 1335207311307068462507042445639511042874498441
86406566986825731805304043247943424442556144144289491524
86018821111325025260282857500182674973951902442427943405
99582722108929879051759838273161560684240203955622690399
4541337789898352038347949953081960160334400609557525776712
7348575267198546669644915183889 paul@underdog
Your public key has been saved in /home/paul/.ssh/identity.pub
[paul@underdog paul]$
```
```

Now that paul has a set of User Keys, he needs to copy the Public User Key, exactly as it appears in `/home/paul/.ssh/identity.pub` on underdog, into the file `/home/paul/.ssh/authorized_keys` on the host topcat. Thus, the `/home/paul/.ssh/authorized_keys` file must minimally contain the entry as shown in Example 11-20 on topcat.

# Example 11-20 `/home/paul/.ssh/authorized_keys` File

```
```
1024 35 1335207311307068462507042445639511042874498441
86406566986825731805304043247943424442556144144289491524
86018821111325025260282857500182674973951902442427943405
99582722108929879051759838273161560684240203955622690399
4541337789898352038347949953081960160334400609557525776712
7348575267198546669644915183889 paul@underdog
```
```

> **NOTE**
> 
> Blank lines and lines beginning with # in the `$HOME/authorized_keys` file are treated as comments.