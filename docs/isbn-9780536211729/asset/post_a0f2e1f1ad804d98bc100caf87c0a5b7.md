
Allchin, group vice president for platforms at Microsoft, was the last executive to defend the Redmond, Washington, software developer. As did company Chairman and Chief Software Architect Bill Gates in his own testimony, Allchin highlighted security problems that could result from technical information disclosure sought by the nonsettling customers.

“It is no exaggeration to say that the national security is also implied by the efforts of hackers to break into computing networks,” Allchin testified. “Computers, including many running Windows operating systems, are used throughout the United States Department of Defense and by the armed forces of the United States in Afghanistan and elsewhere.”

Is this the software that you want to trust your organization's mission and your job to?

A study for the U.S. military headquarters by the Mitre Corporation in May 2002 recommended expanded use of open-source computing because it was less vulnerable to cyber attacks and was far cheaper. Linux is in use by military and intelligence agencies in the U.S., Canada, Germany, France, Spain, China, and Singapore. The U.S. National Security Agency (NSA) even offers its own secure Linux version that is C2-compliant: www.nsa.gov/selinux

Finland, China, Peru, the Philippines, South Korea, Mexico, Germany, and the city of Redmond, Washington are other governments that find Linux meets their needs best. Unlike most commercial software, the code in open-source software benefits from continual scrutiny and improvements made by a large community of programmers dedicated to making it the best that it can be rather than "pushing it out the door" as quickly and cheaply as possible.

a. Reported May 13, 2002 on www.eweek.com/print_article/0,3668,a=26875.00. Some information here comes from the AP's May 30, 2002, article titled "Linux Grows on Government-Systems," reported on Yahoo.

## 2.2.6 Stale and Unnecessary Accounts (#6)

As discussed, each account is a possible entry point into the system. Imagine a moment that you realize your system has been compromised and you have to send a message to everyone to change their passwords immediately.

When a user no longer will be using the system, be sure to remove her account from the system.

A stale account's password will not be changed, thereby leaving a hole. If they have data that needs to be reassigned, disable their account by putting a "*" or "!" in the user's password field in the /etc/passwd file. This disables logging in via that account because no password encrypts each of these values and shadow password-code understands these sequences. Gets cleaned up as soon as possible. Make sure that no set-UID or set-GID programs or publicly readable or writable files containing confidential data remain owned by that account.

Issuing

```
chmod 0 /home/someone
find /user someone -ls
```

It is a good start. Note that the user may have a mailbox, entries on mailing lists, files in the print spool directory, accounts in various applications, etc. that will need to be attended.

Note that some of the services you removed (while correcting an earlier sin) accounts in the /etc/passwd file. When you remove that service, make sure that the /etc/passwd account is also removed or disabled. Some of the notables are FTP, NFS, uucp, mail, gopher, and news. If you do not need them, get rid of them.

In many reports of intrusions the SysAdmin says, "I meant to install...TCP Wrappers...a newer version of a...firewall...meant to turn off NFS... Clearly knew, at least vaguely, what had to be done until it was too late. Sure, you have more responsibilities than time, but consider aside an hour twice a week to upgrade security.

This book is organized so that it may be used as a workbook, with the most urgent and fundamental problems discussed first. This allows you to pop a book marker in it and advance the marker every few days.

## 2.3 Passwords—A Key Point for Good Security

![Password Security](img/7d04225c75a86d3cf4bd6077596f35b2_56_0.png)

Good passwords and good password policy are absolutely critical to security on any computer. Some of this will be familiar to experienced SysAdmins, but everyone gets busy at times, so this is a good time to review these issues and make the necessary changes. Even the author's systems were in need of a password "tune-up." It is suggested that you advise your users not to let others know their passwords or see them type passwords in. Explain that they should not tell a significant other, boss, or even what password is being used.

Ask each of them to report to you if anyone tries to obtain a password or if someone might have obtained one. Explain that your interest is only in security and that the user's name in any of his reports of problems will be kept confidential.

### 2.3.1 Avoiding Weak and Default Passwords

> DANGER LEVEL

Some distributions of Linux fail to put passwords on some system accounts, though modern popular distributions do not seem to have this problem. Still, you certainly want to check by inspecting the text files /etc/passwd and /etc/shadow. The second colon-separated field of /etc/passwd should contain either a “!” or “*”, indicating that a shadowed password is being used. Similarly, the second field of /etc/shadow should contain an encrypted password or one of these sequences.

It is unfortunate that often unusable passwords are used (and allowed), that have the effect of eliminating all security. Because the concept of a password is a sequence of characters known only to the person or persons allowed to use an account, a password should be hard for either someone who knows it or a stranger to guess. The ispell dictionary on most Linux systems allows easy breaking of weak passwords. So do sites offering lists of words, such as various crater sites and ftp://ftp.zedz.net/pub/crypto/wordlists/

Most distributions now offer shadow passwords, kept in the /etc/shadow file only readable by root. This prevents a cracker from copying the world-readable /etc/passwd to his system and running a password-cracking program like John the Ripper. Most distributions offer pwconv and grepshadow utilities as standard to convert non-shadowed passwords into shadowed ones.

-   Use of shadowed passwords should be considered mandatory.

a. John the Ripper can crack DES, double DES, MD5, and other common hashes. Because the crackers hit it, you should have it too and see if your passwords can be cracked easily. It is on the CDROM (but it is not on the Web site) and it is available at: www.openwall.com/john/

There are alternatives to a keyed password that have some advantages, and they are even more powerful when used in conjunction with keyed passwords. These include smart-cards and the like and biometrics. Biometrics are devices that measure a physical attribute, such as the length of your fingers or your fingerprint. Retinal scanners are not yet inexpensive enough for wide use. Some people are fans of one-time passwords.

![Security Concepts](img/7d04225c75a86d3cf4bd6077596f35b2_57_0.png)

At one company I was acting in a consulting capacity, the policy was that a standard password was used for all new employee accounts used for booking customer orders and I discovered that half of the 400 accounts on the system still had this default password.

When I, the SysAdmin, sent these people e-mail asking them to change their passwords and sent follow-up e-mail threatening to disable the account of anyone who did not change his password, I almost got fired for "interfering with the users' work." This policy continued even when massive layoffs started. Fortunately, there were no security violations.

Well, at least these new accounts that I created each got a different initial password so these accounts were safe. The password suite offers password aging to take care of this problem and others.

A password should not be a name or other sequence of characters that others would associate with the person. The following is a list of easily guessed passwords that should not be used:

-   The name of the account or computer itself (yes, some people do this)
-   The word "password" or some variation (I have seen this recently)
-   References associated with the account or containing the account name itself, e.g., the root, p0wer, wheel, or similar for the root account
-   Any reference to Star Trek, Star Wars, Dr. Who, or gaming; we all know these
-   Any part of the account's name, initials, family or significant other, pet, vehicle type, plane or boat details, hobby or pastime, or villain, car tag or license plate, phone number, birthday, anniversary, postal address, e-mail address, Social Security (government identification) number
-   References to your employer or associates
-   Anything that appears on your Web site
-   Favorite food, beverage, or other guessable personal information
-   Your alma mater references associated with it
-   Sexual interests (someone probably knows them)
-   Belief
-   A well-known word or name from science, sports, or politics, e.g., Einstein, Braves, or Gore
-   Commonly known names, places, events, ideas, or phrases
-   Any word or pair of words in the dictionary, including those of foreign
-   The same character repeated or obvious sequences, such as abcde, edcba, or qwerty
-   Passwords used in examples, such as secret and xxyzzy
-   Any of the above with the "clever" substitution of zero for the letter "o", the digit "1" for the letter "I", "8" for "ate". Crackers do this as a matter of course; they will ferret out your use of them.
-   Any of the above spelled backward or with various letters capitalized
