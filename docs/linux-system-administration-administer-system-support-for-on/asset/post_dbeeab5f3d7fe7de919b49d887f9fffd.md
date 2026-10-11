
## Securing Your System

Now that you've got your system set up, you need to do what you can to make it secure and keep it that way. Before you select specific technology for this purpose, however, consider some basic questions such as these:

- How many people have physical access to the computer?
- Is the information on the computer sensitive?
- Do you have a reliable means of backing up your system?
- How many people need accounts on this computer?

## Keeping Physical Security

One of your first concerns as a system administrator is physical security. Start with the basics: Keep the computer locked up – simply out of harm's way – and then decide how to limit access appropriately. For starters, consider these measures:

- If you have sensitive data on a desktop computer, put a password lock on the BIOS and lock the keyboard physically.
- For laptops, leashes are available for about $20. These keep laptops from being opened and used by anyone who doesn't have the key to unlock the leash.
- It's quitting time – do you know where your laptops are? You may want to consider docking stations and locking mechanisms for your hard drives. Many laptops have hard drives that are easily switched out; consider whether such features are appropriate for your system.

## Securing Data Integrity

When you've got your computer physically secure, the next consideration is to keep sensitive data out of the wrong hands. Make sure you know who's got accounts, which accounts are active (and how frequently), and be sure you are verifying the integrity of your files with a program such as Tripwire – which checks files to make sure they have not been modified using checksums, and also looks for Trojan horses (programs designed to run disguised as other programs). A Trojan horse could masquerade as a common UNIX program such as `ls`, `su`, or `csh`.

![](img/8ad518fddafc7f5e73715a2604b61d50_57_0.png)

Tripwire is available at http://www.visualcomputing.com.

### Patching

Patch management is extremely important. When you see a new patch has come out for a vital application, patch the software or kernel right away. Any little software application can become a security hole through which someone can get to the root on your machine.

One of the most recent attacks on the United States government's Sun computer systems involved the statd exploit. Sun released the patch for the statd exploit a year and a half before the attack happened. Such news makes most of the major news Web sites including http://www.cnn.com and http://www.news.com. Nonetheless, some sites such as http://freshmeat.com and http://www.antionline.com report a lot of security and hacker news.

As you might imagine, patching your Linux OS— or any other operating system — is even more important when you're connected to a network, whether through a phone, Ethernet, or any other possible entrance for external mischief.

### Keeping the Correct Number of Accounts

One often-overlooked security issue is account management. Again, start with the basics:

- Keep only the necessary accounts on the machine designated for your use as system administrator.
- Your machine should keep two accounts: its root account and a user account.
- Regulate the use of the root account. If it's always in use, mistakes are likelier — and even a small mistake can easily destroy your system accidentally.
- Use the root account as carefully as you would any powerful and dangerous tool. Using the root account, I once removed all the SUID bits from a system accidentally. They were as necessary to run some programs as was root itself. That caused a bit of a stir.
- If you've got an old account, get rid of it. It could easily become a back door to your system, especially if the previous user had a poor password.

## Backing Up

To defend your system against catastrophic attack, back up religiously. I mean schedule weekly, monthly–if necessary, daily –backups. An incremental backup offers some short-term protection; you back up only the information that wasn't backed up the last time. A full backup is more drastic: You back up everything. A typical schedule uses both types–incremental backups daily and full backups weekly.

## Cleaning Up After an Attack

If you do find yourself attacked, use the latest backups you can that date from just before the attack was detected. Depending on the severity and nature of the attack, you may want to go farther back. If you've installed Tripwire, it should give you plenty of clues about when someone got into your system and started to modify files and logs.

## Dealing with Denial of Service

Although much of this book, focuses on protection against intrusion, another serious type of attack uses *denial of service, or DOS*. A DOS attacker floods your network ports with packets up until the machine says *Okay, I give up. I've had enough*. It's the equivalent of having 200 people in a room trying to talk to one person at the same time. That one person realizes that communication is impossible, and walks out of the room – and your computer responds to a DOS attack in much the same way.

One way someone might bring down your Web server is to type the following:

```
# ping -f www.victim.com 80
```

This command floods port 80 (the Web server port) with ICMP packets and causes the Web server to crash. Fortunately, this method is easily traceable; others may not be.

![](img/8ad518fddafc7f5e73715a2604b61d50_58_0.png)

For online discussion of how to deal with DOS attacks, try the following Web sites: `http://www.rootshell.com` and `http://www.nmrc.org`.

## Summary

When you install Slackware Linux, make sure you have the system requirements, including a CD-ROM and a mouse. First, create the boot and root disks, which enable you to boot your computer into Linux and install the operating system to your hard drive. Then partition your hard drive correctly, allowing enough space to accommodate your Slackware Linux installation and swap space. After this step, you’re ready to install Slackware Linux.

After you’ve installed Linux, set up some basic configurations such as date and time, mouse, modem, and X. When you’ve installed Linux, it’s wise to keep up with how to upgrade the kernel and other programs (including sendmail, and XFree86).

Additionally, make sure your computer can handle the work you give it. Use performance-monitoring tools such as `xload`, `top`, and `free` to check on the allocation of CPU time and memory space.

This chapter introduced some basic security concepts that become important the moment your computer boots up: Make sure your computer is in a secure location, keep data integrity, keep good account management, and maintain the operating system and programs.

## Chapter 2

### A System Administrator’s Responsibilities

IN THIS CHAPTER

- Defining your goals
- Establishing security
- Maintaining accessibility
- Handling growth
- Understanding networking

Now THAT you have Slackware set up and working, I’ll go over some file and disk management techniques that can help you keep your system running smoothly – provided they become habits. Also, I’ll cover disaster recovery, which includes what to do in case of a break-in or major system failure.

### Defining Your Goals

If you’ve administered a system, you know that a basic part of your job is to keep it running with minimal downtime. Then you can define other goals such as these:

- Keeping files from being corrupted or accessed by unauthorized users
- Keeping hardware as failure-free as possible
- Keeping up performance
- Keeping data safe
- Keeping your users happy

The last goal on this list grows quickly in importance if you are maintaining a system for multiple users. Other goals to add may be related to databases, specific in-house applications, or networking. If you’re using your Slackware machine as a router or firewall, for example, network connectivity is crucial.
