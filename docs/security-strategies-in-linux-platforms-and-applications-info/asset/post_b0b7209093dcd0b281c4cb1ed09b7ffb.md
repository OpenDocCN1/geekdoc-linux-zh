
# Preface

Security Agency has even lent its expertise to the Linux community in its efforts to create a more secure computing infrastructure. They have freely released their contributions under open source licenses.

When you are done with this book, you will understand the importance of custom firewalls, restrictions on key services, golden baseline systems, and custom local repositories. You will even understand how to customize and recompile the Linux kernel. You will be able to use open source and commercial tools to test the integrity of various systems on the network. The data you get from such tools will identify weaknesses and help you create more secure systems.

# Learning Features

The writing style of this book is practical and conversational. Each chapter begins with a statement of learning objectives. Step-by-step examples of information concepts and procedures are presented throughout the text. Illustrations are used to clarify the material and to vary the presentation. The text is sprinkled with Notes, Tips, FYIs, Warnings, and sidebars to alert the reader to additional helpful information related to the subject under discussion. Chapter Assessments appear at the end of each chapter, with solutions provided in the back of the book.

Throughout this book are references to commands and directives. They may be included in the body of a paragraph, in a monospaced font like this: apt-get update. Other commands or directives may be indented between paragraphs, like the directive shown here:

```
deb http://us.archive.ubuntu.ubuntu/ lucid restricted
```

When a command is indented between paragraphs, it means to include a Linux command line prompt. You will note two different prompts in the book. The first prompt is represented with a $. As shown here, it represents the command line prompt from a regular user account:

```
$ ls -ltr > list_of_files
```

The second prompt is represented by a #. As shown here, it represents the command line prompt from a root administrative account:

```
# /usr/sbin/apachectl restart
```

Sometimes, the command or directive is so long, it has to be broken into two different lines due to the formatting requirements of this book. Line wraps are indicated by a curved arrow, as is shown at the start of what looks like the second line of the iptables command. It is a continuation arrow, which would be typed as a continuous command on the command line or an appropriate configuration file.

```
iptables -A RH-Firewall-1-INPUT -i eth0 -s 10.0.0.0/8
-j LOG --log-prefix "Dropped private class A addresses"
```

Chapter summaries are included in the text to provide a rapid review or preview of the material and to help students understand the relative importance of the concepts presented.

# Audience

The material is suitable for undergraduate or graduate computer science majors or information science majors, students at a two-year technical college or community college who have a basic technical background, or readers who have a basic understanding of IT security and want to expand their knowledge. It assumes basic knowledge of Linux administration at the command line interface.

# Acknowledgments

I would like to thank Jones & Bartlett Learning and David Kim of Security Evolutions for the opportunity to write this book and be a part of the Information Systems Security & Assurance Series project. This book required a more substantial team effort than ordinary book projects. I would also like to thank the amazing project manager, Kim Lindros; the top-notch technical reviewer, Mike Chapple; the sharp copieditor, Kate Shoup; the marvelous composer, Mia Saunders; the eagle-eyed proofreader, Ruth Walker; and Larry Goodrich along with Angela Silvia of High Stakes Writing for facilitating the entire process.

In addition, I acknowledge the gracious help of Billy Austin of the SAINT corporation, along with Mike Johnson of AccessData with respect to their products. The author also acknowledges the fortitude of Linux security professionals everywhere, white-hat hackers at heart who have to deal with cultural biases from the mainstream security community along with the legitimate fears of the open source community.

Most importantly, I could not do what I do without the help and support of my wife, Donna. She makes everything possible for me.

# About the Author

MICHAEL JANG is currently a full-time writer, specializing in Linux and related certifications. His experience with computers dates back to the days of badly shuffled punch cards. He has written books such as RHCE Red Hat Certified Engineer Study Guide, LPIC-1 In Depth, Ubuntu Server Administration, and Linux Annoyances for Geeks. He is also the author of numerous video courses, and teaches preparation courses on Red Hat certification.

# Is Linux Really Secure?

- CHAPTER 1 Security Threats to Linux 2
- CHAPTER 2 Basic Components of Linux Security 28

# Security Threats to Linux

PEOPLE WHO BELIEVE IN LINUX want to believe that their operating system is inherently more secure. Linux has advantages because fewer viruses, worms, and other malware are written for Linux. There are some juicy targets installed on many Linux systems. For example, Linux is a common platform for relatively insecure file-sharing servers such as the Network File System (NFS) and Samba. In addition, many Linux users still prefer connecting to remote systems with clear-text protocols such as Telnet.

The fact is, risks abound with Linux:

- It is easy to boot fully functional Linux operating systems from a CD drive or a universal serial bus (USB) key, bypassing the access control settings of the operating system installed on the system.
- The standard installation routine of some popular Linux distributions activates potentially vulnerable services.
- Because Linux volumes are not encrypted by default, it's easy to read data from media taken from a physical Linux system.
- Users on Linux systems may make the same security mistakes as users on other systems. Unless prompted, they may never change their passwords. And they're subjected to the same “social engineering” issues as people who use other systems.

A skilled Linux user with malicious intent may pose a more serious threat to your networks than you imagine.

Most Linux software is released under open source licenses. In other words, the source code is publicly available to all. While some say this provides an advantage to users who want to break into a system, open source advocates believe in the power of collaborative development. Even the U.S. National Security Agency (NSA) has contributed a significant amount of code to Linux. To paraphrase the original developer of the Linux kernel, “Many eyes make all security issues shallow.”

The mechanics of information security (IS) on Linux are somewhat different from the mechanics of IS with other operating systems. The principles, however, are the same. In this chapter, you'll examine several models for measuring security, review some attacks on open source software, and learn about different factors that affect security.

Chapter 1 Topics

This chapter covers the following topics and concepts:

- The fundamentals of Linux information security
- How security works as a process in the open source world
- What basic policy and regulatory requirements apply in information security
- What the basic concepts used to measure information security
- The open source security testing methodology manual
- How Linux fits in the seven domains of IT infrastructure
- What kinds of attacks happen on open source software
- How security differs in an open source world
- The costs and benefits of security measures on Linux

Chapter 1 Goals

When you complete this chapter, you will be able to:

- Understand standard and open source criteria for measuring information security
- Describe the basics of security in an open source world
- Explain various roles of Linux systems in the IT architecture
