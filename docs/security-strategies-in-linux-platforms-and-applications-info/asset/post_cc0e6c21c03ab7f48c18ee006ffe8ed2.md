
# PART 3 Building a Layered Linux Security Strategy

A simple method to monitor a system for source code is to look for tarballs, which are normally provided in one or two compressed file archives, normally with .tar.gz or .tar.bz2 extensions. They can be found in user home directories with the find command. Specifically, the following command starts with the /home/ directory and searches all subdirectories for files with the .tar.gz extension:

```
# find /home/ -name *.tar.gz
```

As desired, commands can run on a regular basis as a cron job. For example, to set up a cron job with such searches, use a command like that to show a file in the /etc/cron daily directory. Make sure the output of these commands is redirected to an appropriate file, perhaps in the /var/log directory, suitable for later analysis.

Of course, Linux software comes in other formats. Software suitable for Red Hat distributions are downloaded as package files with .rpm extensions. In contrast, software packages for Debian-based distributions such as Ubuntu are available as package files with deb extensions.

## Executable Files

Naturally, users may set up their own executable files in their home directories with allowed the chmod command. While a few executable files are necessary for certain applications, however, such files should be kept to a minimum. The find command can also be helpful in this area. For example, the following command searches for all files (-type f) with user, group, and other executable permissions, starting with the /home/ directory:

```
# find /home/ -type f -perm /u=x,g=x,o=x
```

Unfortunately, the abilities of this command are limited, especially with respect to applications such as the Evolution Personal Information Manager. Many Evolution data files have to executable permissions.

Perhaps as dangerous as executable files they are with Set User ID (SUID), Set Group ID (SGID), and sticky-bit permissions. Once created by a user, a black hacker may manage to arrange to have them run by a user associated with a service, potentially infecting that with malware of some sort. The find command can be used to search for files with the following command:

```
# find /home/ -type f -perm /u=s,g=s,o=t
```

While changes in executable-permissions are tracked by tools as Tripwire and AIDE in a system, they might not be tracked in user home directories. There are legitimate uses for executable scripts. For example, engineers might have big database jobs that want to run at night through the cron daemon. The tracking of executable files in directories is often left to customized searches with the find command.

# CHAPTER 14 | Detecting and Responding to Security Breaches

# Create an Incident Response Plan

Not all security issues relate directly to computers. Don't forget the human element. The files on a computer are only as secure as the people responsible for them. Nevertheless, when a security issue appears, it is important to be vigilant. It is possible to increase the level of security in a number of areas. Users can temporarily accept increased security if they understand the issues at hand.

Sometimes a security issue is obvious. Someone might identify a file or some information that could be confidential but in an insecure location. Sometimes, you might realize that a specific computer has not been updated with some security patch. If you're able to isolate a security issue to a specific computer, there are several things you can do.

With an appropriate incident response plan, what will you do to collect information. Correct procedures can help you determine what went wrong and what should be done next. In addition, such procedures can help you preserve information as evidence in case the organization decides to secure legal remedies.

> NOTE This chapter does not directly address actual legal requirements with respect to a security breach. In general, it is best to document everything that you may do.

# Increased Vigilance

Every organization with valuable data should have computer security policies in place. As suggested earlier, such policies can be classified in several areas. If there is a reason to suspect black-hacker activity from a local user, you may not be able to share the information with other users.

If you want to pay more attention to user activity, start with the log files. Look at the history of commands normally stored in your user's home directory. If a user has stuck with the bash shell, that history is .bash_history file. Of course, a careful black-hacker may substitute a file with benign commands, but not all black-hackers are so. Any access to administrative accounts should be documented in files discussed earlier and secure auth in the /var/log/ directory.

Any changes to systems access to suspected users can be checked with intrusion detection systems (IDSes) using Tripwire and AIDE.

If you're able to share concerns with users, it's more likely they'll accept reasonable increased security measures in the areas discussed earlier. To recap, when appropriate, security can be increased in the following areas:

- Physical access—Limits on users who are allowed to operate certain workstations
- Internet access—Additional limits on access outside any corporate interns
- E-mail access—Restrictions on communications outside the company
- Remote access—Reduced access to organizational networks
- Passwords—Immediate changes to all passwords

These are just examples of what can be done to increase security, based on less-rigorous policies. Actual policies in standard and higher-alert situations will vary.

# Keep the System On (At Least for Now)

If you identify a system that has been compromised, be careful. The actions you take determine how much can be learned from the situation, whether other systems may be at risk, and how data from a compromised system may be used with respect to potential legal action.

If you're new to computer forensics, read this section as a guide. Any actions with respect to compromised systems should follow a prearranged plan, endorsed by appropriate personnel. This book is not intended to substitute for a real forensics plan.

If it is safe, disconnect the system from a public network, but connect the system to an isolated network. That allows you to use a protocol analyzer to read the traffic going to and from the compromised system. On an Ethernet network, it's possible to use commands like tcpdump and tools like Wireshark. You might get lucky if the black-hat hacker did not change the IP address of packets sent to the targeted system. In that case, you could.

At some point, you may want to disconnect the compromised system from the network. Ideally, if it provides a mission-critical service, you'll have a backup in place with appropriate updates. If that is not, your users may live without the service for a period of time.

If you power down a compromised system too soon, you may lose critical information. Linux stores dynamic information in RAM. That information is accessible through the /proc/kcore file. If you power down a system, that data may be lost.

To get a picture of data in RAM, you'll need a forensics kit. One popular option that has been commercially is known as Helix Kppix. Alternatively, the References section in the back of this book lists several items on the Symantic Web site by Marius Burdach on how to create your own forensics kit. Briefly, the kit can be mounted on a compromised system, with direct access to important commands.

For example, if a forensic system is mounted on the /media/cdrom/, you should be able to run commands from that directory. As suggested by Symantic, you should take the following steps while a system is still running:

1. Take a digital picture of the active monitor of the compromised system.
2. Mount the forensic CD or DVD on the troubled system with the following command (the -n switch avoids writing the mount to the /etc/mtab file):
(troubled system) # mount -n /dev/cdrom /media/cdrom
Be warned: There is fairly risk associated with using the mount command from a troubled system, especially if that command has been compromised by a black-hat hacker.
3. Use netcat, nc, to open communications from a remote system listening (-l 11111) on a specific port such as 11111:
(diagnostic system) # nc -l 11111 date_on_troubled_host
