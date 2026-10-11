![](bbox=[0.13, 0.04, 0.26, 0.1])



0 GB
0 TB
0 PB

Crunch will now generate the following number of lines: 17891328

```
crunch: 100% completed generating output

kali@kali:~$ head crunch.txt
0000
0001
0002
0003
0004
0005
0006
0007
0008
```

*Listing 598 - Generating passwords with a specific character set with crunch*

Notice the file output size is significantly smaller than the previous example, primarily due to the shorter password length as well as the limited character set. However, the wordlist file is impressive, containing over 17 million passwords:

```
kali@kali:~$ wc -l crunch.txt
17891328 crunch.txt
```

*Listing 599 - Counting the number of generated passwords*

In addition, we can generate passwords based on pre-defined character-sets like those defined in /usr/share/crunch/charset.lst. For example, we can specify the path to the character set file (-f /usr/share/crunch/charset.lst) and choose the mixed alpha set mixalpha, which includes all lower and upper case letters:

```
kali@kali:~$ crunch 4 6 -f /usr/share/crunch/charset.lst mixalpha -o crunch.txt
Crunch will now generate the following amount of data: 140712849920 bytes
134193 MB
131 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 20158125312
```

*Listing 600 - Generating password list of lower and upper case letters*

Although this particular command generates an enormous 131 GB wordlist file, it offers rather impressive password coverage.

Spend time with JTR and crunch and think of how each one can be used most effectively. As we will discover in the next section, we need to avoid the temptation to rely on massive and generic wordlists as they can have adverse effects on our client’s production environment.

# *19.2.1.1 Exercise*

(Reporting is not required for this exercise)

+   1. Add a user on your Kali system and specify a complex password for the account that includes lower and upper case letters, numbers, and special characters. Use both crunch