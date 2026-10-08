is the command

**-m 0**

designates the type of hash we are attempting to crack
(MD5 in this case) -a 0

designates a dictionary attack -o passwords

is the output file for the passwords 136 | P a g e

```
```
G:\\Users\OT\\Desktop>pwdump?.exe > passwordhashes.txt
Pwdump v7.1 - raw password extractor
Author: Andres Tarasco Acuna
url: http://www.514.es

G:\\Users\OT\\Desktop>type passwordhashes.txt
Administrator:500:NO PASSWORD***************************:FC9D7C3A3A1E86F1BCC35CD887CB7
4D5:::
Guest::501:NO PASSWORD*********************:823893A8DA2CDAD6E1A414F43EBEDF58F?:::
OTHU::500:NO PASSWORD*********************:8846F7EE1EE8FB117A06DBDD83BE756C:::
user4::1001:NO PASSWORD*********************:A9FDF0838C4B75EBC75DC855DD74F0DA:::
```
```

**hashlist.txt**

is the input file of the hashes /root/top10000passwords is
the absolute path and file name of the wordlist Windows
Password Hashes Earlier with john the ripper, we simply
grabbed the passwords from our Kali system. If we have root
access, that's not a problem. How would we do the same in
Windows?

As I mentioned in the introduction, Windows stores its
passwords at: c:\\Windows\\System32\\config\\SAM.

Whenever a process requires the password that process
accesses a DLL (dynamic linked library) that has system
administrator privileges and accesses the protected SAM
file. What if we could control that DLL

and get access to the SAM file?