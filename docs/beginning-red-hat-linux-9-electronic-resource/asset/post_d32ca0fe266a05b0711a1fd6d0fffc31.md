
## Transferring Data

Transferring information over a network also opens up the possibility of eavesdropping – someone other than the intended recipient may intercept the information on route.

## Physical Threats

Theft of computer equipment can be a big problem – especially for laptop users, and certain areas may suffer from environmental problems, such as flooding, that can damage computer equipment.

So, in summary our list of possible threats could look something like this:

- Operator error
- Hardware failure (particularly disk drives)
- Theft of equipment
- Unauthorized local access
- Unauthorized remote access
- Denial of service (DoS) attack
- Eavesdropping of network communications
- Environmental conditions damage

## Countering the Threats

The list of possible threats may look a bit daunting, but each can be countered by relatively simple measures, as we’ll explain below.

### Hardware

### Physical Security of the Hardware

Physical security is really just a matter of common sense. Keep computer equipment – especially portable equipment, such as laptops – secure. If the computer BIOS has the facility to configure a power-on password, use it. This at least will make it harder for someone to access your machine if it is stolen.

If you are unlucky enough to have your computer stolen, then you have to rely on your backups to get back the information that you lost. You do have backups, don’t you? You have tested them, haven’t you? Better read Chapter 10!

While we're on the subject of backups, the idea behind backing up your system is to allow you to **rebuild it** in case of some catastrophic event. This means that someone else can also build a copy of your system if they can get hold of your backups, so take care over the physical security of your backup media too.

### Hardware Failure

Pay attention to the environmental conditions that your computer is working in. Computers don't like to get hot, and excessive temperature can cause premature failure of heat sensitive components, especially hard disk drives. There are ways of preventing the failure of a disk drive from causing loss of data, and these techniques rely on keeping the information on more than one physical disk.

The term **Redundant Array of Independent Disks** (or **RAID**) is widely used to describe these solutions, and the **RAID level** – a combination of digits and sometimes letters – indicates how the information is stored on multiple disks.

RAID may be implemented in hardware (typically in the hard disk adapter) or in software. If you're interested in RAID, have a look at the Linux-ATA-RAID HOWTO and the Software-RAID HOWTO on your system's documentation resources, or on-line.

Common RAID levels are:

| RAID level | Data positioning |
| :--- | :--- |
| 0 | Data is broken up into equal size chunks (64Kbyte and 128Kbyte are common) and chunks are written to every disk in the array in turn (with four disks in the array, the 1st, 5th, 9th, ...., chunks of data are written to the first disk, the 2nd, 6th and 10th to the second disk, etc.). This pattern of data placement is called "striping", and the size of each chunk of data is called the stripe width. This gives the best performance, but worst availability, since failure of any disk will result in the loss of some data. |
| 1 | Data is copied on to pairs of disks (mirrored). Good performance and availability, but it uses twice as much disk space. |
| 5 | Data is striped across multiple disks, and protected by parity information that is also striped across the disks. Good performance for reading, but writing can be slowed by the need to update parity information. Requires extra disk capacity to store the parity information. |
| 7 | Not really RAID at all! RAID 7 is also known as JBOD (Just a **B**unch **O**f **D**isks). Here the information is not configured according to RAID, and your multiple disks are simply configured as one larger logical drive. It offers no fault tolerance advantages over simply using several disks individually. |
| 10 (or 0+1) | Data is striped across multiple pairs of disks. Combines performance of RAID 0 with availability of RAID 1. |

Whether RAID is suitable for you depends on how valuable you consider your information to be – a decision that only you can make. Even if you do go for a hardware or software RAID solution for your Red Hat Linux system, please don't make the mistake of thinking that you don't need to take regular backups. Even if you set up the most extreme combination of hardware and software RAID (using software RAID to mirror data between two hardware RAID arrays, giving you effectively four copies of the data on four separate physical hard disks), the rm command can still irreversibly delete all four copies in a fraction of a second!

### Local Security

So, we've sorted out the physical security of our Red Hat system. We've enabled the BIOS password so that only those who know it can start the machine up in the first place, and we've taken care with the physical location so it won't get stolen (we hope!) and the disk drives will stay nice and cool. Should we be unlucky enough to suffer a disk drive failure, we're taking – and testing – regular backups (we discussed how to do this in the previous chapter), so we're confident we can recover any lost information. What's next?

### (Mis)using the root Account

You'll recall from the section on 'Threats that operator error was high on the list of potential threats. Computers have a nasty habit of doing exactly what we tell them to do, and not what we want them to do. So that this doesn't cause us too many problems, the trick is always to work with the lowest level of authority that we need to perform a particular task. Usually, this is not the root account.

Here's a little hypothetical example to demonstrate the potential pitfalls of using the root account for everyday tasks. **Don't try this at home, as it could result in serious damage to your system!**

Suppose we need to maintain the contents of a directory called /home/foo/logs by deleting files that are more than 14 days old. We could write a simple script to do this:

```
Remember, don't try this at home, folks!
```

```
#!/bin/bash
LOGDIR="/home/foo/logs"
cd $LOGDIR
find . -mtime +14 -exec rm \{\} \\;
```

Unfortunately, we’ve made a typo in the script (the 4th line should say `cd $LOGDIR`); this means that when the `cd` command is run, its argument is blank (because the misspelled variable `$LOGDIR` is not defined). This means that the `cd` command makes the current working directory our `$HOME` directory, not `/home/foo/logs` as we want. The `find` command then finds all the files below our `$HOME` directory (the current working directory) older than 14 days and deletes them. That’s a pain if we’re logged on as an ordinary user, but if we’re logged on as root, this could well delete a lot of critical configuration information. (At least root’s home directory on Red Hat Linux defaults to `/root`, which is a small mercy – on some other flavors of Unix, the default home directory for root is `/`, so running the above flawed script on one of those could well wipe out the entire operating system!)

### Passwords

The password that we use to authenticate ourselves to the operating system when we log in is the only way we have of proving our identity, and thus keeping an intruder out. Your password is never stored on the Linux system (the operating system won’t do it). Instead, a non-reversible mathematical function called a **hash** is used to combine your password with a random value (called the *salt*), and the hashed password is stored by the system. When you try to log in, the password you type is once again hashed with the same salt and the result compared to the one stored when the password was originally set. If the values are the same, then it’s fairly safe to assume that the password you typed is the same as the original one, and you are allowed in.

Now, you’re probably thinking that someone could look at the stored hashed passwords and deduce the original passwords by reversing the hash function. However, the hash functions are chosen to make this reversal practically impossible. However, that doesn’t stop someone who has access to the hashed passwords from using a program that guesses passwords to try and guess one.

Early versions of Unix stored the hashed passwords with other user information in `/etc/passwd`. Since the user information needs to be accessible to everyone (so, for example, user names could be shown in the output of `ls -l`), this also made the hashed passwords available to everyone too. Modern versions of Unix, including Red Hat Linux 9 avoid this problem by keeping hashed passwords in a separate file, called the **shadow password file**. On Red Hat, this is `/etc/shadow`. Since the hashed passwords need to be accessible only to authentication programs that run with root authority, the shadow password file should be accessible only to the root user.

### Choosing a Strong Password

Choosing a strong password is really better phrased as avoiding weak passwords. Weak passwords are ones that can be guessed, either by humans or by password cracking programs (that will quite happily try different permutations of words from password dictionaries for days on end without getting bored).
