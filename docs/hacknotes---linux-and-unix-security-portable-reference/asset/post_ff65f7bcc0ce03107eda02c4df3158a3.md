
# HackNotes Linux and Unix Security Portable Reference

+   Smbmount ..................................................................................... 183
Tcpdump ....................................................................................... 183
Wget ................................................................................................ 184
ZEthereal ...................................................................................... 184
zNessus ...................................................................................... 184
MTR ......................................................................................... 185
Dig ............................................................................................ 185
Perl .......................................................................................... 186
Online Resources for the Zaurus ................................ 186
Summary ....................................................................................... 186

+   Index ...................................................................................... 187

# ACKNOWLEDGMENTS

His book would not have been possible without the help of many people. First, I would like to thank Mike Horton, the series editor of HackNotes, giving me the opportunity to write this book. Thanks also go to the tireless effort of the McGraw-Hill/Osborne team, including Jane Brownlow, Athena Honore, Betsy Manini, and Robert Campbell.

A big-thank you to Robert Clugston of Foundstone, who was responsible for reviewing this book’s technical contents.

Thanks also to my wife, Deepti, for being so helpful during the time I spent writing this book.

This page intentionally left blank

# HACKNOTES: THE SERIES

McG-Hill/Osborne has created a brand new series of portable reference books for security professionals. These are quick-study books kept to an acceptable number of pages and meant to be a truly portable reference.

The goals of the HackNotes series are:

- To provide quality, condensed security information that is easy to access and use.
- To educate you how to protect your network or system by showing how hackers and criminals leverage known methods to break into systems and best practices in order to defend against hack attacks.
- To get someone new to the security topics covered in each book to speed quickly, and to provide a concise source of knowledge. To do this, you may find yourself needing and referring to time and again.

The books in the HackNotes series are designed so they can be easily carried with you or towed in your computer bag without added weight and without attracting unwanted attention while you are using them. They make of charts, tables and bulleted lists as much as possible and only use screen shots if they are integral to getting across the point of the topic. Most importantly, so that these handy portable references don't burden you with unnecessary verbiage to wade through during your busy day, we have kept the writing clear, concise, and to the point.

# XVI HackNotes Linux and Unix Security Portable Reference

Whether you are brand new to the information security field and need useful starting points and essential facts without having to search through 400+ pages, whether you are a seasoned professional who knows the value of using a handbook as a peripheral brain that contains a wealth of useful lists, tables, and specific details for a fast confirmation, or as a handy reference to a somewhat unfamiliar security topic, as HackNotes series will help you get where you want to go.

# Key Series Elements and Icons

Every attempt was made to organize and present this book as logically as possible. A compact form used and page tags were put into mark primary heading topics. Since the Reference Center contains information and tables you'll want to access quickly and easily, it has been strategically placed on blue pages directly in the center of the book, for your convenience.

# Visual Cues

The icons used throughout this book make it very easy to navigate. Every hacking technique or attack is highlighted with a special sword icon.

> This Icon Represents a Hacking Technique or Attack
> Get detailed information on the various techniques and tactics used by hackers to break into vulnerable systems.

Every hacking technique or attack is also countered with a defensive measure when possible, which also has its own special shield icon.

- This Icon Represents Defense Steps to Counter Hacking Techniques and Attacks
> Get concise details on how to defend against the presented hacking technique or attack.

There are other special elements used in the HackNotes design containing little nuggets of information that are set off from general text so they catch your attention.

This "i" icon represents reminders of information, knowledge that should be remembered while reading the contents of a particular section.

This flame icon represents a hot item or an important issue that should not be overlooked in order to avoid various pitfalls.

# Commands and Code Listings

Throughout the book, user input for commands has been highlighted as bold, for example:

```bash
[bash]# whoami
root
```

In addition, common Linux and Unix commands and parameters that appear in regular text are distinguished by using a monospaced font, for example: whoami.

# Let Us Hear from You

We sincerely thank you for your interest in our books. We hope you find them both useful and enjoyable, and we welcome any feedback on how we may improve them in the future. The HackNotes books were designed specifically with your needs in mind. Look to http://www.hacknotes.com for further information on the series and feel free to send your comments and ideas to feedback@hacknotes.com.

This page intentionally left blank

# INTRODUCTION

This book will teach you exactly how hackers think so that you can protect your Unix and Linux systems from them. There is simply no other way to learn how to prevent your systems from being compromised. In order to stop the attacks of the most sophisticated hackers, you need to understand their thought processes, techniques, and tactics. The powerful nature of the Unix and Linux operating systems is a two-edged sword. In most cases, the operating system kernel source code is available for free, and an administrator can go so far as to change the system internals to suit his or her needs. But this powerful and flexible nature of Unix and Linux includes an enormous amount of complexity, which increases the likelihood of possible misconfigurations that can easily place a system at risk. Consider also the many different flavors of Unix and Linux distributions available today. Every distribution comes bundled with its own set of security policies and configurations. For example, some distributions leave a set of remote services turned off, while others turn on all possible services that have been configured with the weakest possible policies. Hackers are aware of the administrative complexities of managing Unix and Linux hosts, and they know exactly how to abuse them. This book will amaze you with details of the craftiest hacker tactics, and it will teach you how to defend against them.

# HackNotes Linux and Unix Security Portable Reference

Don't worry about hackers getting hold of the material presented in this book. They already know it. The intention of this book is to expose the tactics used by hackers today, so that you can learn to protect against them. Once you understand how hackers think and the many different methods they use to break into systems, the odds will be in your favor.

# How This Book Is Organized

This book has been divided into four major sections:

## Part I: Hacking Techniques & Defenses

Part I of the book follows the common hacking methodology that is being used by hackers today. Defenses against all the hacking techniques described in these chapters are also presented.

- **Chapter 1** We begin by understanding the first logical step in hacking methodology: footprinting. This chapter will teach you how hackers obtain publicly available information from search engines, registrar records, DNS records, and more. Once hackers have obtained all possible information from publicly available sources, they move on to actual network and host identification and scanning.
- **Chapter 2** This chapter teaches you how to determine which hosts on a network are alive and what ports open. Various types of port scanning methods are discussed, along with system identification techniques and tools.
- **Chapter 3** Learn how hackers identify applications and services running on remote hosts. This chapter will show you the many different tools and methods used by potential intruders to enumerate usernames and remote services.
- **Chapter 4** This chapter exposes the fact and tactics used by hackers to gain access to vulnerable hosts. Learn the craftiest techniques being used by hackers, such as brute-forcing, sniffing, man-in-the-middle attacks, password cracking, port redirection, exploits against misconfigurations, buffer overflows, and many other software vulnerabilities.
- **Chapter 5** Often, the exploitation of a specific vulnerability yields a hacker access to unprivileged user or system accounts. In such cases, the next logical step for a hacker is to obtain superuser (root) privileges. This chapter shows you the many different ways hackers attempt to obtain higher privileges.
