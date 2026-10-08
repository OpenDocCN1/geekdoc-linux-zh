
upon the site, but I think a depth of four subdirectories is sufficient and efficient at capturing most of the keywords. Now we can write our ceWL command to do just that to www.hackers-arise.com and scrape every word longer than eight characters from it.

```bash
kali > cewl -d 4 -m 8 https://www.hackers-arise.com -w cewlpasswords
```

```text
root@kali-2019:~# cat cewlpasswords
Metasploit
Forensics
Training
Subscribers
security
Automobile
Exploits
Facebook
computer
Raspberry
Security
Cracking
Bluetooth
information
Wireless
Password
directory
Engineering
Reconnaissance
Scripting
Forensic
Vulnerability
Investigator
Scanning
Information
Internet
Registration
Networks
Professional
Confessions
Fundamentals
Development
Schedule
Payments
Confidantes
DataBase
Honeypot
```

Note that it’s important to precede the URL of the target website with http or https. Without this preface, ceWL will be unable to scrape the target URL. Depending upon the size of the website, this could take several hours.

When ceWL has completed its scraping of potential passwords, it will place all the potential passwords in a file I have named cewlpasswords (you can name it anything you desire). We can view the contents of this file by using the cat command:

```bash
kali > cat cewlpasswords
```

ceWL was able to find several hundred potential passwords on www.hackers-arise.com, some very specialized to our industry such as Metasploit, exploits, vulnerability, scripting, and others.

To now use that password list in john, we can enter;

```bash
kali > john -wordlist=/root/cewlpasswords -rules passwordhashes
```

john will now use the list of words scraped from the target’s website (cewlpasswords) and apply rules to mangle (-rules) them with character substitution, thereby increasing the chance of cracking the target’s passwords.

## Crunch

Sometimes, to crack a password, we may need to create a specialized list that meets certain known parameters. For instance, maybe we know that the passwords all end in four numbers (eg. password1234) or we know the target’s birthday and suspect they use it in their password. If the target’s birthday were February 29, they might create a password such as “password0229”. Crunch is our tool to create such lists!

To get started with crunch, simply enter crunch in your BASH shell.

```bash
kali > crunch
```

```text
root@kali-2019:~# crunch
crunch version 3.6
Crunch can create a wordlist based on criteria you specify. The output from crunch can be sent to the screen, file, or to another program.
Usage: crunch <min> <max> [options]
where min and max are numbers
Please refer to the man page for instructions and examples on how to use crunch.
root@kali-2019:~#
```

```text
CRUNCH(1)                General Commands Manual                CRUNCH(1)
NAME
crunch - generate wordlists from a character set
SYNOPSIS
crunch <min-len> <max-len> [<charset string>] [options]
DESCRIPTION
Crunch can create a wordlist based on criteria you specify. The output from crunch can be sent to the screen, file, or to another program. The required parameters are:
min-len
The minimum length string you want crunch to start at. This option is required even for parameters that won't use the value.
max-len
The maximum length string you want crunch to end at. This option is required even for parameters that won't use the value.
charset string
You may specify character sets for crunch to use on the command line or if you leave it blank crunch will use the default character sets. The order MUST BE lower case characters, upper case characters, numbers, and then symbols. If you don't follow this order you will not get the results you want. You MUST specify either values for the character type or a plus sign.
NOTE: If you want to include the space character in your character set you must escape it using the \ character or enclose your character set in quotes i.e. "abc ". See the examples 3, 11, 12, and 13 for examples.
OPTIONS
-b number[type]
Specifies the size of the output file, only works if -o START is used, i.e.: 60MB The output files will be in the format of starting letter-ending letter for example: ./crunch45-b 20mb -o START will generate 4 files: aaaa-gfved.txt, gfzee-omgbw.txt, omgbz-wcydu.txt, wcydu-zzzzz.txt valid values for type are kb, mb, gb, kib, mib, and gib. The first three types are based on 1000 while the last three types are based on 1024. NOTE There is no space between the number and type. For example 500mb is correct 500 mb is NOT correct.
```

```text
-t @%,$"
Specifies a pattern, eg: @@@@@@@%@@@ where the only the @'s, ,'s, $'s, and ^'s will change.
@ will insert lower case characters
, will insert upper case characters
% will insert numbers
" will insert symbols
```

Although this displays some basic information on crunch, we really need to view the man page to understand how to use crunch.

```bash
kali > man crunch
```

Here we see all the key options to make efficient use of crunch. If we scroll down a bit, we can see the pattern-specifying wildcards to use with the -t option.

```text
EXAMPLES
Example 1
crunch 1 8
crunch will display a wordlist that starts at a and ends at zzzzzzzz

Example 2
crunch 1 6 abcdefg
crunch will display a wordlist using the character set abcdefg that starts at a and ends at gggggg

Example 3
crunch 1 6 abcdeg\
crunch 1 6 abcdeg\
there is a space at the end of the character string. In order for crunch to use the space you will need to escape it using the \ character. In this example you could also put quotes around the letters and not need the \", i.e. "abcdefg". Crunch will display a wordlist using the character set abcdefg that starts at a and ends at (6 spaces)

Example 4
crunch 1 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt
crunch will use the mixalpha-numeric-all-space character set from charset.lst and will write the wordlist to a file named wordlist.txt. The file will start with a and end with "                "

Example 5
crunch 8 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt -t @dgg@@@ -s cbdogaaa
crunch should generate a 8 character wordlist using the mixalpha-number-all-space character set from charset.lst and will write the wordlist to a file named wordlist.txt. The file will start at cbdogaaa and end at " dog "

Example 6
crunch 2 3 -f charset.lst walpha -s BB
crunch with start generating a wordlist at BB and end with ZZZ. This is useful if you have to stop generating a wordlist in the middle. Just do a tail wordlist.txt and set the -s parameter to the next word in the sequence. Be sure to rename the original wordlist BEFORE you begin as crunch will overwrite the existing wordlist.
```

```text
root@kali-2019:~# crunch 9 9 -t dylan%%%% -o customwordlist.txt
Crunch will now generate the following amount of data: 100000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 10000
crunch: 100% completed generating output
```

Then when we scroll to the bottom of the man page we can see some simple examples.

Now let’s try using crunch to create wordlists. Remember my example above about a target that has a password policy of at least eight characters and at least one number? Let’s create a custom password list that meets those criteria.

Let’s say we know that the target is a Bob Dylan fan. They might use that name and then append it with four numbers (maybe their birth date). We could create such a list in crunch by entering;

```bash
kali > crunch 9 9 -t dylan%%%% -o customwordlist.txt
```

When we hit enter, crunch first calculates how large the file will become before creating it (those of you who are Mr. Robot fans (www.hackers-arise.com/mr-robot) will likely recognize that Elliot cracked his therapist’s password in Season 1 using a similar technique). In this case, crunch estimates it will be 100,000 bytes. This is crucial information as it is possible to create files with crunch that are extraordinarily large and will fill your entire hard drive. For instance, if I wanted to create a wordlist with four letters before and four numbers after the password and up to thirteen characters, I would enter;

```bash
kali > crunch 13 13 -t @@@@dylan%%%% -o customwordlist.txt
```

```text
root@kali-2019:~# crunch 13 13 -t @@@@dylan%%%% -o customwordlist.txt 
Crunch will now generate the following amount of data: 63976640000 bytes 61012 MB 59 GB 0 TB 0 PB
Crunch will now generate the following number of lines: 4569760000
```

```text
root@kali-2019:~# git clone https://github.com/Mebus/cupp 
Cloning into 'cupp'... 
remote: Enumerating objects: 6, done. 
remote: Counting objects: 100% (6/6), done. 
remote: Compressing objects: 100% (6/6), done. 
remote: Total 194 (delta 1), reused 1 (delta 0), pack-reused 188 
Receiving objects: 100% (194/194), 109.18 KiB | 1.13 MiB/s, done. 
Resolving deltas: 100% (100/100), done.
```

As you can see above, crunch is about to create a 59GB wordlist! That’s a bit
