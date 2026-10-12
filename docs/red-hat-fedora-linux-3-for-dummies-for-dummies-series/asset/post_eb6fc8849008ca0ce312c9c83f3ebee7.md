
The *Targeted* policy compromise makes sense. If you use your Fedora Core computer as a workstation protected by a firewall and the methods and systems described in this chapter, then you have relatively little security exposure. However, if you start running network services such as Apache, then your risk accelerates. Protecting network-based services with SELinux provides a big step up in security.

Describing more about the inner workings of SELinux is beyond the scope of this book. Using the *Targeted* policy should be adequate for most people's needs. However, you can read more about SELinux from the following mailing list and Web sites:

- `http://fedora.redhat.com/mailman/listinfo/fedora-selinux-list`
- `www.lurking-grue.org/gettingstarted_newselinuxHOWTO.html`
- `www.crypt.gen.nz/selinux/faq.html#WWW.1`
- `www.samag.com/documents/s-7835/sam0303a/0303a.htm`
- `www.crypt.gen.nz/selinux/faq.html`

## Understanding the Security Process

The best way to look at security is as a process. The more you think about it and the more you study it, the safer you are. You should use the security systems described in this chapter as the foundation for your security process. However, you should continue to build your security process to meet the needs of your own computer system and network.

This section outlines some additional building blocks you may consider adding to your process:

- **Making backups:** Backups are part of the security process? Yes! Backups are an essential security tool in the sense that you can never eliminate the possibility of getting hacked. When your security is breached, you may lose all sorts of information and configurations. For example, all the information on your computer may be completely erased or, worse, you may not know which files are good or bad. You must ensure your ability to recover from these types of catastrophes.

One good backup method is to use the GnomeTool user application, as we describe in Chapter 11. You can store your user account and configuration files on a CD-R/RW or DVD+/-RW. This method is reliable, and the discs should last forever. The only limitation is the CD's ability to store only 700MB to 800MB of data (although you can store more data with compression).

- **Security education:** Keeping up with security trends and topics helps you avoid getting bitten by new hacks. Knowing your adversaries and their techniques is essential.

These URLs provide good security-based information; see Chapter 21 for some current top security holes:

- www.linuxsecurity.com
- www.sans.org
- www.nmap.org
- www.securitytracker.com
- www.counterhack.net
- www.infosysec.com
- www.cert.org

- **Physical security:** We focus on discussing network-based security in this book. We assume that your Fedora Core computer is running on your home network, in which case you have to worry mostly about Internet bad guys. In an office environment, however, you have to worry about physical security.

Physical security involves preventing people from walking up and gaining unauthorized access to your computer. You should set a BIOS password to prevent anyone else from booting your computer into single-user mode (which would totally avoid your Linux passwords). You should lock your computer in your office, if possible, to prevent anyone from stealing your hard drive. Don't, under any circumstances, write your passwords in any accessible place (such as on your desk or computer).

You should also set the GNOME (or KDE) screen lock unless you want to log out every time you leave your desk. Choose GNOME Menu → Preferences → Screensaver and then select the Lock Screen After option. Select the amount of time to wait before locking your screen and then click the Close button.

- **Boring consistency:** Good long-term security depends on consistency. Making backups, reading security logs, and performing other, similar tasks all depend on your maintaining interest. It's like staying in shape: You cannot be good for a while and then forget about your routine.

# Chapter 18

# Bringing In the Fedora Core Repairman

## In This Chapter

- Understanding the art of troubleshooting
- Gardening with the fault tree
- Diagnosing network problems

This book is perfect, and there’s no way that anything we have written can ever go wrong — never, ever. You may be as lonely as the Maytag repairman if you expect trouble. As the Pop Will Eat Itself tune goes: The trouble is, trouble never happens. Errata (corrections) are as outdated as a brick-and-mortar bookstore. This book makes setting up computers and networks so easy that you may wonder why other people have so many problems! Blah, blah, blah.

Yeah, right. The problem is that this guy named Murphy (as in Murphy’s Law) hangs out in both virtual and real bookstores, and visits all things mechanical and electronic. He’s always jumping in just when things are starting to go well. The guy just cannot keep his nose out of other people’s business. This chapter is meant to smooth things out between you and Murphy in case he catches up with you.

One common problem involves getting your Fedora Core computer to work on a network. Sometimes, the best-laid plans go a little awry and Murphy comes to visit. This chapter is designed to help when networking problems pop up.

## The Fix Is In: Troubleshooting Your Network

Your Fedora Core machine is the foundation of your network and must be set up correctly for anything to run. If it isn't working or if you have an unusual setup (or if Murphy is in a bad mood), you can check for several different causes.

We use a Fedora Core computer connected to a private network as the troubleshooting example in this chapter. The Fedora Core network is one of the more difficult things to set up correctly because it depends on not only your Linux computer but also other computers. Suppose that your Fedora Core computer isn't working within your private network. If that's the case, use this chapter to help troubleshoot your network.

![](img/41feae212f5c6612ff709354891f7b39_281_0.png)

See Part V for insights into other problems. Chapter 20 describes how to find information about common problems with your Fedora Core computer. Chapter 21 describes several security fixes.

## Introducing Fault Trees

As with a surprising number of technical pursuits, troubleshooting is more of an art than a science. Sometimes, you can easily see what the problem is and how to fix it. At other times, that's not so easy. The degree of difficulty you have in fixing a problem depends on how complex the problem is and how well you know your stuff. Obviously, the better acquainted you are with computers and Linux, the better you are at troubleshooting.

Every problem has a solution. Computers are cause-and-effect-based machines. When something breaks or doesn't work, there's always a reason. The reason or reasons may not be easy to find, but they exist.

How do you find the cause? That's a million-dollar question. Getting a million bucks isn't easy unless you're willing to grind your teeth, plot against your fellow contestants for weeks on a remote island, purchase 10 million PowerBall tickets, or — believe it or not — work hard and work smart. Some people are willing to eat rats for the chance at a million bucks or are lucky enough to win the lottery; most just have to work hard. Oh, well.

Working hard is conceptually easy, but how do you work smart? This concept is where the idea of the fault tree comes into play. (You mean faults grow on trees? Not exactly . . . ) The *fault tree* is a conceptual aid that helps you to eliminate all but the real cause of your problem. The fault tree looks like an upside-down tree, where the trunk of the tree represents the fault, or problem. The ends, or leaves, of the branches represent all the possible causes. After that's done, solving the problem is virtually guaranteed.

For example, Figure 18-1 shows part of a fault tree that points out which major subsystems you should examine. To find the solution to a problem, you have to systematically identify what's working. You work your way to what's not working and then when you find it, you usually solve your problem. The fault tree simply helps to formalize the process of problem solving.

Here are some possible faults:

- **The first branch on the left involves problems with the physical connection.** Do you have a malfunctioning network adapter or switch/hub? Is the cable not connected properly to the adapter? In that case, jiggle the cable or fuss with the connector. Do you have a break in the cable or a loose connector?
- **The second branch deals with the network interface configuration.** Have you correctly configured the IP address for your Ethernet adapter (NIC)?
- **The third branch helps you to decide whether the problem exists with the network routing.** Can your network packets be directed toward the correct network?

The fault tree helps you to break down any big problem into several simpler ones. By eliminating each simple problem one by one, you should eventually locate the root cause.

![](img/41feae212f5c6612ff709354891f7b39_282_0.png)

### The blind leading the blind

A colleague of ours, Ken Hatfield, once said, "One of the side benefits from lots of troubleshooting comes from what I call 'the value of blind alleys.' Most often in troubleshooting, you go down blind alleys, as in your tree example, the wrong branches of the solution tree. But in doing so, you learn something. In the future, when you encounter a different problem, that previous blind alley may be the road to the solution."

Here's an example: We recently had a server that was having lots of problems. The `/var` file system had filled up, which caused some programs to fail. When space on `/var` was freed up, most of the programs started to do their jobs again. But one program didn't work. Paul spent a long time trying to figure out why it didn't work even after the problem was fixed. As it turned out, this particular program's real problem was that its license had expired. He had not only walked down a blind alley but also bumped into a wall and kept trying to go forward. (D'oh!)
