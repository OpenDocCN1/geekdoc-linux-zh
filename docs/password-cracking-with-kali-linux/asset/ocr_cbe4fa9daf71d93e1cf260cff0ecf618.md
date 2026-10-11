# # SINGLE WORDLIST

**-a0, Straight Attack or the Single Wordlist Attack - **This is the simplest attack in Hashcat. Hashcat will use a single wordlist against the password hash file. Each word from the wordlist will be directly hashed and compared with the password. If there is a match, the password is “cracked”. If not, hashcat tries the next word in the wordlist and continues until every word in the wordlist is checked against the password hashes.

Example:

```
> ```
> **hashcat -m 0 [Uncracked].txt wordlist.txt -o [Cracked.txt]**
> ```
```

You can also use “Rules” in single attack mode.