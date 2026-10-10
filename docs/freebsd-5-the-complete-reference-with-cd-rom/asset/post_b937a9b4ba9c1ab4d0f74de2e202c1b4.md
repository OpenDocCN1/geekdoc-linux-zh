
## Chapter 29: System Security Considerations

### Password Creation

The best passwords, from the point of view of being unbreakable should a password database fall into the wrong hands, are random collections of letters, digits, and punctuation. Unfortunately, such passwords are not very memorable to mere mortals. Administrators who force their users to cope with such passwords discover that this requirement backfires: Users write down their difficult-to-remember passwords. Once on paper, the passwords can be misplaced or a missscented-tom1gh find a password in a desk or even read it over a user's shoulder. Thus, truly random passwords, although theoretically a good idea, in practice are not so great.

A good compromise is to perform a two-step process. First, begin with a *password base*, which is memorable and might by itself make a poor password. Second, modify that base in various ways to turn it into something that won't be likely to appear in any cracker's dictionary. Two common types of bases are unrelated word pairs and acronyms that are personally relevant. For instance, a two-word base might be **bun** and **pen**. A personal acronym might be yiwtt (for yesterday I went to the dentist). Neither combination is likely to appear in a dictionary, although a two-word base might be found by a procedure of combining short words.

**Note** These examples use fairly short (six-letter) bases because some systems impose eight-character limits on password length, and subsequent modifications expand the length by two or more characters. FreeBSD, however, takes longer passwords, and the longer a password, the better. As a general rule, eight characters should be considered the minimum safe size for a password.

**Caution** Do not use the example bases presented here. As they've been published, they may well already appear in crackers' dictionaries. Create your own personal base from two words or an acronym.

Once you've generated a base, you should apply modifications to the base to increase its size and make it less likely that it will be discovered through a dictionary attack. Possible modifications include, but are not limited to

- **Adding characters** Add numbers or punctuation to the password, preferably at random locations. For instance, bunpen might become b#un7pen, and yiwtt might become y1owtt<d.
- **Mixing case** You can randomize the case of letters, such as b#Un7pEN or YIowTT<d. Some systems use case-insensitive passwords, so this technique isn't always effective. FreeBSD's normal PAM-mediated passwords are case-sensitive, but SMB/CIFS encrypted passwords are not.
- **Reversing letter order** If you use a two-word base, reverse the order of one word. For instance, b#Un7pEN might become b#NN7pENd.

The idea behind these modifications is to move the base further away from words that might be in a cracker’s dictionary. For instance, a cracker might use a dictionary that includes combinations of common words, such as bun|ner; but the cracker’s dictionary is less likely to include every possible variation on case, letter order reversals, and inserted random punctuation. Thus, the final password of b#tUn?NEb is unlikely to be in a cracker’s dictionary.

Of the modifications, the first (adding numbers and punctuation) is arguably the most important because it creates the largest number of variants. In fact, some password-changing tools on some systems require that passwords use at least one or two letters or symbols. (FreeBSD’s standard passwd tool does not impose this requirement, though.)

### Special Comments for the root Account

The root account is extraordinarily important, and thus its password is unusually sensitive. On some systems, more than one user needs the root password—for instance, a multiuser system that has several administrators. You should take special care in generating the root password, and if the system has several administrators, make sure that each one understands the importance of root password security. Never send the root password over a network connection that’s not encrypted. For instance, you should never use su to acquire root privileges from a Telnet login or when using a system remotely via X or VNC (unless the session is tunneled through SSH). You should also be diligent about changing your root password on a regular basis, so that if it is compromised, the intruder will have a limited window of opportunity in which to use the root password.

Of course, some of the same caveats about passwords apply to system administrators as to ordinary users—a typical system administrator will find it difficult to remember a truly random password, for instance. Nonetheless, because the number of system administrators is typically small (often just one), and because it’s the system administrator’s job to secure the system, the root password may reasonably be less memorable than most ordinary user passwords.

### Detecting Intrusion

Precautions such as those described up to this point in this chapter are very important, but a 100 percent secure computer is about as real as a unicom. No matter how much work you do and how skilled you are, there’s always some chance that somebody can break in. Possible methods of entry include unknown (to you, but not to an attacker) bugs in servers or other software, misconfigurations of servers or other programs, stolen passwords, and attacks based on physical access to the computer. Because you can’t absolutely rule out the possibility of intrusion, you should develop a plan to detect intrusion. There are several steps you can take to improve your chances of quickly detecting an intruder. These include general vigilance, monitoring log files, and using intrusion-detection tools such as Tripwire. If you do detect an intrusion, knowing how to handle it can be very important.

### General Warning Signs

Fortunately, most crackers aren't very skilled. Script kiddies commonly invade poorly secured computers, and the root kits they use frequently leave traces behind. These traces may include modified utilities that don't work quite like the originals, modified configuration files that damage normal functionality, and so on. You should be on the lookout for certain warning signs that sometimes indicate an intrusion:

- **Broken programs** If a program suddenly stops working, investigate the matter. For instance, if a common program such as `ls` or `cat` suddenly starts crashing, it could be that the program has been replaced with one written or modified by a cracker.
- **Odd program behavior** Less serious problems than out-and-out crashes may signal an intrusion. In the UNIX world generally, programs such as `ifconfig`, `grep`, and `netstat` work differently on different platforms. Even in FreeBSD alone, these programs also change over time; options in FreeBSD 5.0 may be slightly different than those in FreeBSD 4.6, for instance. A cracker might have replaced one of these tools with a modified version derived from a non-FreeBSD source or from an earlier or later version of FreeBSD than you're using. If so, the program's output or options may suddenly change, from your point of view.
- **Changes in resource use** Sometimes crackers break in to steal your CPU time, network bandwidth, or other resources. Chapter 28 describes how to monitor many of these resources. If you notice a sudden change in these factors, you should investigate the cause to be sure it's not malicious activity.
- **Forgotten passwords** If a user comes to you and claims to have forgotten a password, investigate further. Ask the user when the account was last used, then check `/var/log/auth.log` to see if there were any logins after that date. If there were, it could be the password hasn't been forgotten, but has been changed by a cracker.
- **Suspicious account activity** You may notice that a user is logged in at a peculiar time (say, as listed in the output of `ps` or `who`). For instance, if you know a particular person is on vacation with no network access, but you see that user logged in using a local terminal, it could be that a cracker has broken into the user's account.
- **Gaps in log files** Crackers sometimes delete lines from log files, or even entire log files, to mask their activity. If you notice such gaps, you may want to investigate further. For instance, you can use the `find` command (described in Chapter 8) to locate files that were created or modified within the gap period. Be very suspicious if any critical system binaries or configuration files were modified at that time.
