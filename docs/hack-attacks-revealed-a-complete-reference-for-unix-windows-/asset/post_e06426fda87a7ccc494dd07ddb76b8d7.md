
## Mail Bombing, Spamming, and Spoofing

Mail bombs are email messages used to crash a recipient's electronic mailbox, or to spam by sending unauthorized mail using a target's SMTP gateway. Mail bombs can exist in the form of one email message with huge files attached or thousands of e-messages with the intent to flood a mailbox and/or server. For example, there are software programs that will generate thousands of email messages, dispatching them to a user's mailbox, thereby crashing the mail server or restraining the particular target as it reaches its default limit.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_391_0.png)

**Figure 8.5** Forging mail headers to spoof e-messages.

Mail spamming is another form of pestering; it is an attempt to deliver an e-message to someone who would not otherwise choose to receive it. The most common example is commercial advertising. Mail spamming engines are offered for sale on the Internet, with hundreds of thousands of email addresses currently complementing the explosive growth of junk mail. It is common knowledge among hackers that unless the spam pertains to the sale of illegal items, there is almost no legal remedy for it.

Other widespread cases include email fraud, which involves an attacker who spoofs mail by forging another person's email address in the From field of an email message (shown in Figure 8.5), then sending out a mass emailing instructing recipients to “Reply” to that victim's mailbox for more information, and so on. Currently, ISPs are on the lookout for mail fraud bombers, as they have been known to disrupt the services of entire networks.

Most email bombers claim their mechanisms protect the send with anonymity. You will come to realize that it can be difficult to spoof these messages. You will also realize that most of those email bombers come with a list of SMTP servers that currently do not log IP addresses. In a nutshell, this is how most Windows-based email bombers send spoofed emails.

Accordingly, hackers who wish to spoof emails use programs such as Avalanche (or Mailflash in DOS mode), by using a server that does not log IP. Up Yours (shown in Figure 8.6) and Avalanche are programs used to bomb someone’s email address. They were made with dual objectives in mind: anonymity and speed. On average, Avalanche can, for example, send about 20 emails in five to seven seconds, using five clones running on only a 28.8 K connection. What’s more, these programs can generate fake mail headers that help cover up the attack.

The Bombsquad utility was developed to protect against mail bombs and spamming, though it was designed primarily to address mail bombing. The software enables you to delete the email bombs, while retrieving and saving important messages. It can be used on any mailbox that supports the standard POP3 protocol. That said, be aware that phony compilations of Bombsquad have been floating around that implement remote-access control Trojans to cause far worse a fate than mail bombing. Reported, these daemons have come with the following filenames:

- squad1.zip
- squad.zip
- bomsg.zip
- bmsquad.rar

![](img/ba85bb40c695c02adae8cbd6666f2e0c_392_0.png)

**Figure 8.6** Up Yours mail bomber control panel.

> **Hacker’s Note** For more information on mail bomb countermeasures, check out *Hack Attacks Denied* and visit the Computer Incident Advisory Capability (CIAC) Information Bulletin at http://ciac.lln.gov/ciac/bulletins/c-005c.shtml.

## Password Cracking

Forget your password? Have your passwords been destroyed? Need access to password-protected files or systems? Did certain of your former employees leave without protecting their files? Or do you simply want to learn how hackers gain access to your network, system, and secured files?

In a typical computer system, each user has one fixed password until he or she decides to change it. When the password is typed in, the computer's authentication kernel encrypts it, translates it into a string of characters, then checks it against the long list of encrypted passwords. Basically, this list is a password file stored in the computer. If the authentication modules find an identical string of characters, paired with the login, it allows access to the system. For obvious reasons, then, hackers, who want to break into a system and gain specific access clearance typically target this password file. Depending on the configuration, if hackers have achieved a particular access level, they can take a copy of the file with them and run a password-cracking program to translate those characters back into the original password.

Fundamentally, a password-cracking program encrypts a big list of character strings, such as all words in a dictionary, and checks it against the encrypted file of passwords. If it finds even one match, the intruder has gained access to the system. This sort of attack does not require a high degree of skill; hence, many types of password cracking programs are available on the Internet. Some systems can defend against cracking programs by keeping the password file under tight security. The bigger problem, however, is sniffers (described later in this chapter).

### Decrypting versus Cracking

Contrary to popular belief, UNIX passwords are difficult to decrypt when encrypted with a one-way algorithm. The login program encrypts the text entered at the password prompt and compares that encrypted string against the encrypted form of the password. Password-cracking software uses wordlists; each word in the wordlist is encrypted, and the results are compared to the encrypted form of the target password. One of the most common veteran cracking programs for UNIX passwords is `xcrack.pl` by hacker guru manix, shown next.

```perl
# start xcrack.pl

#system("cls");    # This will clear the terminal/DOS screen
                    # Then stick this info on the screen
print ("\n \t\t-----------------------------\n");
print ("\n \t\t Xcrack V1.00");
print ("\n \t\thttp://www.infowar.co.uk/manix");
print ("\n \t\t-----------------------------\n");

if ($#ARGV < 1) {

    usage(); # Print simple statement how to use program if no arguments
    exit;
}

$passlist = $ARGV[0];      # Our password File
$wordlist = $ARGV[1];      # Our word list
# ---------------- Main Start ---------------------
```
