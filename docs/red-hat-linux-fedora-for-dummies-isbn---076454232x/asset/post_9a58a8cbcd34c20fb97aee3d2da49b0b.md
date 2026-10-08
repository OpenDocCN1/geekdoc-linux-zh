
## Hide Your Communications with OpenSSH

  You may find it difficult to trust communication media that you don't completely control — such as university LANs, wireless home networks, and the Internet. Our point: Trust no one!

![](img/8c094d1b36276212c03d10d898508a6e_328_0.png)

  Any public network is potentially dangerous, especially the Internet. One way to protect yourself is to use encryption for all communication. You use encryption when you conduct credit card transactions or read remote e-mail. Secure Socket Layer (SSL) communication is the standard encryption mechanism for secure Internet browsing and e-commerce transactions.

  The Secure Shell (SSH) protocol is used to conduct encrypted CLI (command-line interface) terminal sessions and file transfers. Red Hat bundles the open source version of SSH called OpenSSH with its distributions. When you install Red Hat Linux, you automatically get the OpenSSH client. You can use OpenSSH from a terminal session by entering the command `ssh destination`. The destination is the computer you want to communicate with. You can get information about OpenSSH from www.openssh.org.

![](img/8c094d1b36276212c03d10d898508a6e_328_1.png)

  Using encryption is essential when you use wireless networking. Wi-Fi (also known as 802.11b) wireless networks can use built-in encryption based on the WEP protocol. WEP does have some significant security vulnerabilities, though. The only long-term answer is either to wait until the next standard comes along to fix the problem or to use OpenSSH to provide you with your own encryption. You're much safer if you use OpenSSH and SSL for as much of your communication as possible.

## Aha! No Firewall — Very, Very Good

  Broadband connections give you a quantum leap in speed and convenience when you're connecting to the Internet. The two most popular choices for a broadband connection are DSL and cable modems. After you start using them, you may never go back to slow, Stone Age telephone-based modems.

  But every silver lining implies a dark cloud. Broadband connections give you not only fast Internet connections but also continuous ones. With a telephone-based modem, a hacker can attack only your home computer and private network while you're connected to the Internet. Using a 24/7 broadband connection means that every hacker on the Internet — that means every hacker in the world — can constantly bang on your computer and private network. That's lots of vulnerability.

  Firewalls provide your number-one protection from Internet-based attacks. The modern Netfilter/Iptables packet-filtering firewall system gives you excellent protection when it’s properly configured. The Red Hat installation process installs a good Iptables-based firewall by default, and Chapter 8 describes how to configure an even better one. You should never, ever connect to the Internet without first configuring your personal firewall.

![](img/8c094d1b36276212c03d10d898508a6e_329_0.png)

  We don’t mean to imply that you’re invulnerable to attack if you use a telephone-based modem to connect to the Internet. Traditional modem connections are just as vulnerable as continuous broadband connections *when they’re active*. What we mean is that an unconnected modem is a safe modem.

## Keeping Up with the Software Joneuses

  Nobody’s perfect, and that goes for operating system vendors. Even open source Linux developers and excellent companies like Red Hat make mistakes. Vulnerabilities are found in software systems all the time and have to be fixed.

  Red Hat provides a way to keep up-to-date with current problem and security fixes through its Web site. Go to `ftp.redhat.com/pub/redhat` to find the newest and safest versions of all your system’s RPM packages. You can also find out how to use the Red Hat Linux Network, at `rhn.redhat.com`, so that it updates itself automatically — see Chapter 17 for details.

## “Backups? I Don’t Need No Stinking Backups!”

  If you don’t regularly make backups of your computer’s contents, you face a security vulnerability, plain and simple. You may lose some or all of your valuable information if your computer is compromised. You should back up your data as frequently as possible.

  You can use one of many techniques and software for making backups, but that’s stuff we couldn’t possibly begin to cover in this book. We wouldn’t be able to cover Red Hat Linux if we even began to go into detail.

![](img/8c094d1b36276212c03d10d898508a6e_329_1.png)

  So keep it simple: Archiving your home directory and copying it to another location is a simple and effective backup mechanism.

  For example, the following commands use the ubiquitous Linux tape archive (tar) command to create an archive of your home directory. You can then use the OpenSSH $scp$ command to securely copy the archive to another location, such as your ISP account or another computer you have access to. Follow these steps to create an archive of your home directory:

- 1. Log in to your user account.
- 2. Run this $tar$ command:

```
tar czf mybackup.tgz .
```

  In this case, the $c$ option means to use $tar$ to copy the specified files and directories. The $z$ option tells $tar$ to compress the data. The $f$ option defines the text that follows it—$mybackup.tgz$—as the file to copy the files to. The single dot (.) says to copy to the archive all files in the current working directory.

- 3. Use OpenSSH to copy the $tar$ archive to another location:

```
scp mybackup.tgz myloginaccount@myisp.com
```

  This command securely copies the $tar$ archive to the account $mylogin$ $account$ at the ISP $myisp.com$.

## My Buffer Overflow-eth

  One of the most popular methods that hackers use to break in to computers is via buffer overflows. The buffer overflow technique attempts to feed crazy streams of data to programs in order to make them behave in ways their designers never intended. (A detailed description of what a queue does is beyond the scope of this book. Suffice it to say that Linux uses a queue to store instructions and addresses for later use.) The result of the buffer overflow is that sometimes the program provides the hacker with a shell or other open door when it fails.

  The shell created by a buffer overflow is an open door to your computer. Sometimes, the shell has root (superuser) privileges, and then the hacker owns your system.

  Here are some simple techniques you can use to minimize buffer overflows:

- **The first line of defense is simply to minimize the number of services you run.** You run zero risk of compromise from a buffer overflow vulnerability in Service A if you don’t run that service.

  For example, the Lion worm wreaked havoc in spring 2001. Lion exercised vulnerability in the Linux sendmail and lpd printer services. Computers that didn’t run those services weren’t vulnerable to the Lion worm.

- The second line of defense is to update your Red Hat Linux computer as often as possible. Red Hat posts package updates, as they become available, that fix vulnerabilities. Buffer overflow fixes comprise many of the package updates. Updating your system fixes many buffer overflow vulnerabilities.

## Social Engineering 1010101010

  Hackers don't have to discover supertechnical tricks to break into your computer. Many smart hackers aren't deterred when they encounter a well-protected computer or network. What does a poor hacker in these security-aware times have to do to break into your system?

  Some hacker techniques don't rely on technological means. One such technique is *social engineering*, which is a fancy way of saying “I plan to trick you or your associates into giving me information to use against you.”

  Social engineering can be as simple as a hacker calling you to see whether you're at home or in the office. If you're not physically present, the hacker or burglar can drop by, break in and steal the computer or its disks. After someone gains physical possession of your computer, most security precautions you take can be easily defeated.

  Another social engineering technique hackers employ is to call a corporation's help desk and pretend to be a VIP. The poor minimum-wage employee can often be bullied or cajoled into giving out a password or other important information.

![](img/8c094d1b36276212c03d10d898508a6e_331_0.png)

  The moral of the story is to exercise good security hygiene and be careful of strangers. Don't give out information unless it's essential and you can verify the authenticity of the request.

## Bad Passwords

  Probably the easiest to avoid, and most often abused, vulnerability is poor or non-existent passwords. Passwords are your first line of defense. If your password is easily guessed or — even worse — blank, someone will break in.

  Bad passwords are easy to fix. Start by assigning a password to every account you create — *especially* root. Then make it a habit to use “good” passwords. Passwords can be cracked by brute force because computers have become very fast. Because you connect to the Internet, hackers can steal your `/etc/passwd` file, which contains the encrypted version of your text-based passwords and then use a computer to crack them.
