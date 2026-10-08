
system (see the 4-way handshake in Wi-Fi hacking) and take them offline and commit the resources to cracking them.

Here, we will examine tools and techniques for first, offline password cracking and then second, online password cracking.

### A Word about Wordlists

Both online and offline password cracking require a list of words to try.

These wordlists don’t necessarily include all words. Some may be combinations of characters that are often used as passwords such as qwerty, asdfghjk, or 123456. Choosing the proper wordlist may become the most important decision you make in attempting to crack a password.

Kali has a large number of wordlists built into it. You can locate them by entering `locate wordlists`:

```
root@kali:~# locate wordlists
/usr/share/wordlists
/usr/share/applications/kali-wordlists.desktop
/usr/share/d/irb/wordlists
/usr/share/d/irb/wordlists/big.txt
/usr/share/d/irb/wordlists/catala.txt
/usr/share/d/irb/wordlists/common.txt
/usr/share/d/irb/wordlists/euskera.txt
/usr/share/d/irb/wordlists/extensions_common.txt
/usr/share/d/irb/wordlists/indexes.txt
/usr/share/d/irb/wordlists/mutations_common.txt
/usr/share/d/irb/wordlists/others
/usr/share/d/irb/wordlists/small.txt
/usr/share/d/irb/wordlists/spanish.txt
/usr/share/d/irb/wordlists/stress
/usr/share/d/irb/wordlists/vulns
/usr/share/d/irb/wordlists/others/best1050.txt
/usr/share/d/irb/wordlists/others/best110.txt
/usr/share/d/irb/wordlists/others/best15.txt
/usr/share/d/irb/wordlists/others/names.txt
/usr/share/d/irb/wordlists/stress/alpha_num_case.txt
/usr/share/d/irb/wordlists/stress/alpha_num_case_extra.txt
/usr/share/d/irb/wordlists/stress/char.txt
/usr/share/d/irb/wordlists/stress/double_uri_hex.txt
```

These wordlists are usually linked to an application and contain words that are particular to that application. For instance, the wordlist for the web directory cracking tool, **dirb**, contains commonly used words for website directories. Very often, the key to effective password cracking is selecting the appropriate wordlist.

In addition, there are numerous wordlists that can be found online. At such places as [www.skullsecurity.org](www.skullsecurity.org) and www.hackers-arise.com/password-lists.

Finally, you might consider creating your own wordlist, one that should be customized for the task.

### Password Cracking Strategy

When attempting to crack passwords, you will be well served to have a strategy before attempting the password crack, unless you are brute-forcing (and then, your strategy is patience). I always start with a small list with the most commonly used passwords. Remember, although there are 7.5 billion people on this planet and 1.5 billion speak English (although not all natively), and people tend to think and act similarly. Lazy people (or those who simply don’t take information security seriously) will use common words or common keystroke combinations (i.e. qwerty, 123456) and others will take an additional step and create slightly more complex passwords including their name, initials, birthdays, anniversary dates, favorite TV show, children and spouse, among other things.

From the email dumps on the dark web, we can construct lists of the most commonly used passwords. In 2018, these were:

1. 123456
2. password
3. 123456789
4. 12345678
5. 12345
6. 111111
7. 1234567
8. sunshine
9. qwerty
10. iloveyou
11. princess
12. admin
13. welcome
14. 666666
15. abc123
16. football
17. 123123
18. monkey
19. 654321
20. !@#$%^&*
21. charlie
22. aa123456
23. donald
24. password1
25. qwerty123

Yes, believe it or not, the most common passwords are “123456” and “password”!

These passwords comprise about 10 percent of all user accounts! And “123456” was used by almost 3 percent of accounts! Although my analysis is less than scientific, I estimate that the top 5,000 passwords are used on nearly one-third of accounts. With that information, it would be foolish to attempt a wordlist with millions of passwords and cost you days, weeks, or months of work. Instead, start strategically by attempting the top 5,000 or so most-common passwords first and, only if they fail, try using incrementally larger and more complex wordlists. If you have all the password hashes on, say, a 1000-user domain, by simply attempting the top 5,000 passwords, you are likely to find over 300 of them. Remember, you only need one password to compromise the network.

### Cracking Passwords with John the Ripper

John the Ripper is one of the oldest continuously maintained password crackers. Having first appeared on the hacking scene in 1996, Solar Designer maintains this excellent Unix/Linux password cracker. Here we will use it to learn password-cracking principles and strategy using this simple, yet elegant tool.

We can view John’s help file by simply entering the command **john** in a terminal.

```
root@kali-2019:~# john
John the Ripper 1.8.0-1.j3-bluemoon-1-bleeding-973a245b96 2018-12-17 20:12:51 +0100 [linux-gnu 64-bit x86_64 AVX2 AC]
Copyright (c) 1996-2018 by Solar Designer and others
Homepage: http://www.openwall.com/john/

Usage: john [OPTIONS] [PASSWORD-FILES]
--single[-SECTION[,...]]	"single crack" mode, using default or named rules
--wordlist[=FILE]		wordlist mode, read words from FILE or stdin
--stdin			like --stdin, but bulk reads, and allows rules
--loopback[=FILE]		like --wordlist, but extract words from a .pot file
--duplicate-suppression		suppress all dupes in wordlist (and force preload)
--prince[=FILE]		PRINCE mode, read words from FILE
--encoding=NAME		input encoding (eg. UTF-8, ISO-8859-1). See also doc/ENCODINGS and --list-hidden-options
--rules[=SECTION[,...]]		enable word mangling rules (for wordlist or PRINCE modes), using default or named rule(s)
--rules=rule[,...]		same, using "immediate" rule(s)
--rules-stack=SECTION[,...]	stacked rules, applied after regular rules or to modes that otherwise don't support rules
--rules-stack=rule[,...]	same, using "immediate" rule(s)
--incremental[=MODE]	"incremental" mode (using section MODE)
--mask[=MASK]		mask mode using MASK (or default from john.conf)
--markov[=OPTIONS]	"Markov" mode (see doc/MARKOV)
--external=MODE		external mode or word filter
--subsets[=CHARSET]	"subsets" mode (see doc/SUBSETS)
--stdout[=LENGTH]		just output candidate passwords [cut at LENGTH]
--restore[=NAME]		restore an interrupted session [called NAME]
--session=NAME		give a new session the NAME
--status[=NAME]		print status of a session [called NAME]
--make-charset=FILE		make a charset file. It will be overwritten
--show[=left]		show cracked passwords [if --left, then uncracked]
--test[=TIME]		run tests and benchmarks for TIME seconds each
--users[~]LOGINS[UID[,...]	[do not] load this (these) user(s) only
--groups[~]GID[,...]		load users [not] of this (these) group(s) only
--shells[~]SHELL[,...]		load users with[out] this (these) shell(s) only
--salts[~]COUNT[~MAX]		load salts with[out] COUNT [to MAX] hashes
--costs[~]COST[,...]		load salts with[out] cost value [to MIN]. For tunable cost parameters, at LEVEL 1-3
--save-memory=LEVEL		enable memory saving, at LEVEL 1-3
--nodes=MIN[-MAX]/TOTAL	this node's number range out of TOTAL count
--fork=N		fork N processes
--pot=NAME		pot file to use
--list=WHAT		list capabilities, see --list-help or doc/OPTIONS
--format=NAME		force hash of type NAME. The supported formats can be seen with --list-formats and --list=subformats
```

```
root@kali-2019:~# useradd hacker
root@kali-2019:~# passwd hacker
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
root@kali-2019:~#
```

Let’s begin this journey into password cracking by cracking the passwords on our own Kali Linux system. First, let’s create some new accounts on our system using the Linux command `useradd`. This simple command requires a username and then enter the command `passwd` and then the account name.

It will then prompt you twice for the password.

Create five new accounts. On the first two accounts, use short dictionary words. Then, on the next three, use increasingly longer and more complex passwords (add numbers, special characters, etc.).

Now that we have six user accounts on our Kali (five new and our root account), let’s try cracking them with John the Ripper.

The first step to cracking these passwords is to extract the /etc/shadow file (where the hashes reside) and strip out everything but the password hashes. We can do this with John’s `unshadow` command. This command requires that both the /etc/shadow and the /etc/passwd files be in the same directory.

```
root@kali-2019:~# cp /etc/passwd ./
root@kali-2019:~# cp /etc/shadow ./
root@kali-2019:~# unshadow passwd shadow > passwordhashes
```

```
root@kali-2019:~# john passwordhashes
Using default input encoding: UTF-8
Loaded 5 password hashes with 5 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Remaining 4 password hashes with 4 different salts
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Wordlist
Press 'q' or Ctrl-C to abort, almost any other key for status
```
