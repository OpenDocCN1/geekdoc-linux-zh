# USING CRACKED PASSWORDS TO
CRACK NEW PASSWORDS

One of the best advanced cracking techniques is to use the passwords that were cracked as a wordlist, and then using them in combo attacks or running rules on them. This is easy to do by parsing the Hashcat cracked output file. The output file will have the original hash, a colon, and then the cracked password. All we need to do is remove the hash and colon, and then re-save the file as a new wordlist.

The Linux text manipulation commands are great for parsing wordlists. In particular the "cut" command. All you need to do is figure out where the hash & colon ends and then cut the passwords out and save them in a new file. In the wordlist example below, the passwords start at column 34.

```
cut -c34-128 cracked.txt > crackedwl.txt
```