
you well, particularly as you interact with more experienced Linux users on the Internet.

- An explanation of how Linux works -- While it’s not necessary to delve into the most arcane aspects of the Linux kernel, it’s a good idea to know something about how Linux is put together. This is particularly important if you’ve been working with other operating systems; some of the assumptions you hold about how computers work may not transfer from that operating system to Linux. A few paragraphs that discuss how Linux works (and particularly how it differs from the operating system you’re used to) can be invaluable in getting off to a good start with your Red Hat Linux system.

- An introductory command overview (with examples) -- This is probably the most important thing to look for in Linux documentation. The design philosophy behind Linux is that it’s better to use many small commands connected together in different ways than it is to have a few large (and complex) commands that do the whole job themselves. Without some examples that illustrate the Linux approach to doing things, you will find yourself intimidated by the sheer number of commands available on your Red Hat Linux system.

Here is some additional direction that may help to match all of your requirements:

- Books -- Linux for Dummies, by John “maddog” Hall, published by IDG; Using Linux, by William H. Ball, published by Que; Running Linux, by Matt Welsh and Lar Kaufman, published by O’Reilly & Associates; Red Hat Linux Secrets, by Naba Barkakati, published by IDG.

- Red Hat’s website -- At our very own website (http://www.redhat.com), you’ll find links to the Linux Documentation Project (LDP), the Official Red Hat Linux Installation Guide, the Official Red Hat Linux Getting Started Guide FAQs (Frequently Asked Questions), a database which can help you search for a Linux Users Group near you, a knowledgebase of information, and more. In short, you’ll find a wealth of information to help you get started.

- Newsgroups -- Linux users are second to none when it comes to helping new users understand Linux. You can find dozens of Linux-related newsgroups on the Usenet, but a quick search through Deja.com (http://www.deja.com) shows:
  - `linux.help`
  - `linux.redhat`
  - `linux.redhat.digest`
  - `linux.redhat.misc`
  - `linux.redhat.rpm`

Also, from the Deja.com website, you can frequently search for specific information from Linux newsgroups.

Continue reading the next section to find out more about the kinds of documentation that will help you at that point.

## For the More Experienced

If you’ve used other Linux distributions, you probably already have a basic grasp of the most frequently used commands. You may have installed your own Linux system, and maybe you’ve even downloaded and built software you found on the Internet. What sorts of information will you need?

- Task-oriented items -- Many times, you will find that you would like to configure your Red Hat Linux system in a certain way, but you’re not sure where to begin. In this case, it’s often a big help to see what others in similar circumstances have done. This is where the Linux Documentation Project (also known as the LDP) can come in handy. Each of their HOWTOs document a particular aspect of Linux, from low-level kernel esoterica, to using Linux for amateur radio station work.

If you selected one of the various HOWTO packages when you installed Red Hat Linux, you’ll find the HOWTOs on your system in /usr/doc/HOWTO.

## Documentation for Linux Gurus

If you’re a long-time Red Hat Linux user, you probably already know that the following pretty much says it all when it comes to documentation:

> *Use the Force -- Read the source!*

There are times when you'll just have to sit there and look at the sources to understand things. Fortunately, because of the freely available nature of Linux, it's easy to get the sources. Now if it were only that easy to understand them...

## More to Come

The *Official Red Hat Linux Reference Guide* is part of the Red Hat's growing commitment to provide useful and timely support to Red Hat Linux users. Future editions will feature expanded information on system administration, console tools and other resources to help you extend the power of your Red Hat Linux system -- and yourself. That's also where you come in.

## Send in Your Feedback

If you'd like to make suggestions about the *Official Red Hat Linux Reference Guide*, please mention this guide's identifier:

RefGuide(EN)-6.2-Print-RHI (02/00)

You can send mail to:

docs@redhat.com

## Sign Up for Support

If you have an official edition of Red Hat Linux 6.2, please remember to sign up for the benefits you're entitled to as a Red Hat customer.

You'll be entitled to any or all of the following benefits, depending upon the Official Red Hat Linux product you purchased:

- Official Red Hat support -- Get help with your installation questions from Red Hat, Inc.'s support team.

- Priority FTP access -- No more late-night visits to congested mirror sites. Owners of Red Hat Linux 6.2 receive free access to priority.redhat.com, Red Hat's preferred customer FTP service, offering high bandwidth connections day and night.

- Red Hat Update Agent -- Receive e-mail directly from Red Hat as soon as updated RPMs are available. Use Update Agent filters to receive notification and quickly download updated packages about those subjects that interest you. Also receive -- automatically -- kernel updates, security updates and other packages.

- Under the Brim: The Official Red Hat E-Newsletter -- Every month, get the latest news and product information directly from Red Hat.

To sign up, go to http://www.redhat.com/now. You’ll find your Personal Product ID on a red and white card in your Official Red Hat Linux box.

To read more about technical support for Official Red Hat Linux, refer to the Appendix in the Official Red Hat Linux Installation Guide.

Good luck, and thank you for choosing Red Hat Linux!

*The Red Hat Documentation Team*

# Part I System-Related Reference

## 1 Red Hat Linux 6.2 New Features

This chapter describes features that are new to Red Hat Linux 6.2.

### 1.1 Installation-related Enhancements

The Red Hat Linux 6.2 installation program includes a number of new features. For more information, please refer to the *Official Red Hat Linux Installation Guide*.

### 1.2 System-Related New Features

There are many new features to Red Hat Linux 6.2 that are not part of the installation process. Some new features are tools or applications that you can use, others are new versions of the kernel or desktop environments. This list will provide a little more information about what to expect from Red Hat Linux 6.2 once you are actually using the OS itself.

**Network services split into client, server packages:**

The following network services have been split into client and server packages:

- telnet
- finger
- talk
- rsh
- rusers
- rwall
- tftp

For example, on the Intel-compatible platform `telnet` is now packaged in two RPMs --

- `telnet-0.16-5.i386.rpm`
- `telnet-server-0.16-5.i386.rpm`

**sysctl now controls system settings:**

In Red Hat Linux 6.2, kernel options such as IPv4 forwarding and enabling and disabling of the “magic sysrq” keys is done via the `sysctl` program, as opposed to being controlled by the contents of files in `/etc/sysconfig`. The `sysctl` settings are stored in `/etc/sysctl.conf`, and are loaded at each boot by the command:

```bash
sysctl -p /etc/sysctl.conf
```

Here is a sample `/etc/sysctl.conf`:

```bash
# Disables IPv4 packet forwarding
net.ipv4.ip_forward = 0
# Enables source route verification
# This drops packets that come in over interfaces they shouldn't;
# (for example, a machine on an external net claiming to be one on your
# local network)
net.ipv4.conf.all.rp_filter = 1
# Disables automatic defragmentation
# Automatic defragmentation is needed for masquerading and Linux
# Virtual Server use; it is not needed otherwise.
net.ipv4.ip_always_defrag = 0
# Disables the magic-sysrq key
kernel.sysrq = 0
# Disables stop-a on the Sparc
kernel.stop-a = 0
```

Many other kernel tunable parameters can be set; to see the full list, run `sysctl -a`, or look in the file `/usr/doc/kernel-doc-<version>/sysctl`.
