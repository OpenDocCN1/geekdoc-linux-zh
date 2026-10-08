compromised, the hacker may delete my e-mail before their people see it. (I used “hacker” because I doubted that she was familiar with the term “cracker.”) The line went quiet without explanation and there was no one on the other end.

As I was debating whether I had been hung up on, she came back on the line and said that there was no answer when they tried to reach their computer operations department. I reiterated the importance of this matter and asked that he contact someone and that I wanted a call back with status. I never received any further contact. An nmap scan of their DNS server offered only one service: X. My nmap scan of this system (allowed by those in the southeastern U.S. due to a Federal District Court ruling) also showed no firewall rules in place.

# B.13 Persistence with Recalcitrant SysAdmins Pays Off

SysAdmins who have tracked down a system that has repeatedly attacked their network commonly contact the system’s SysAdmin or Webmistress, explain the problem, and ask that it be corrected. More common than not, the response is none or we cannot be bothered. Some techniques on dealing with potential nonresponses are discussed in “Other SysAdmins: Do They Care?” on page 511. Most administrators of systems that have been attacked just throw in an IP Tables rule to block their packets or in the case of spam do the following as root

```
```markdown
cd /etc/mail
echo "spammer@baloney.com tab DISCARD" >> access
make
```
```

and accept the lost bandwidth. However, persistence can pay off. Telephone the organization and get the name and extension of the responsible person or their management. Call them several times a day until the matter is resolved to your satisfaction. If the problem is serious enough and you have the backing of your management, ignore the threats of calling the authorities that will certainly follow. Most will not call. Of the few that do, their complaints likely will be ignored, and if the authorities actually get involved, the first thing they will do, at worst (for you), is to ask you to stop. In your case, though, you have a legitimate reason for calling.

The effectiveness of this was thoroughly demonstrated to me recently when the phone company made an error in my bill. My attempts to resolve it by normal means failed and I started getting harassing calls from MCI at least daily and up to four times a day demanding payment. My demands not to phone me again or I would file a complaint about harassing calls with the authorities were ignored. When I asked each person calling to connect me with a manager to discuss the matter, they either hung up on me or put me on infinite hold. My certified letter to MCI was ignored.

Eventually, I surrendered and mailed the amount they demanded. Even then, they refused to stop calling until the payment was received in a distant city, despite my explaining that I had mailed payment, and they refused to connect me to anyone with the authority