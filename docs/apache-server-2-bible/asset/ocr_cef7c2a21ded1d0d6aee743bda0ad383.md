| Attribute | Meaning |
| --- | --- |
| MAILPROGRAM = /path/to/mail/program | Default: MAILPROGRAM = /usr/sbin/sendmail -oi -t |

 This attribute specifies the mail daemon path and any arguments that you need to supply to run it. This attribute only makes sense if you are using MAILMETHOD = SENDMAIL. |
| EMAILREPORTLEVEL = 0 - 4 | Default: EMAILREPORTLEVEL = 3 |

 This attribute specifies the level of information reported via email. Leave the default as is. |
| MAILNOVIOLATIONS = true | false | Default: MAILNOVIOLATIONS = true |

 If you wish to not receive e-mail when no violation is found, set this to false. |

To test your e-mail settings, you can run Tripwire by using the `/usr/sbin/tripwire -m t -email your@emailaddr` command. Don’t forget to change `your@emailaddr` to your own e-mail address.

# ## Securing Apache using the Linux Intrusion Detection System (LIDS)

*Root is the source of all evil.* The previous statement probably only makes sense to the Unix/Linux system administrators of the world. Once an unauthorized root access is confirmed, damage control seems hopeless or at the mercy of the intruder.

In a plain-vanilla Linux system, several subsystems are typically unprotected. The file system is often left as open as the wild, West. There are many important files, such as `/bin/login`, in the system, that hackers exploit frequently because they are not protected. If a hacker breaks in, the hacker can upload a modified version of the login program as `/bin/login` to allow him or her free access to the system in the future. But the fact of the matter is that files (that is, programs) such as `/bin/login` files do not need to change frequently (if at all); therefore, they must not be left unprotected. Like the file system, the running processes are also unprotected. Many processes run with the root privilege, which means that when they are exploited using tricks such as buffer overflow, the intruder gains full root access to the system.

Reducing the power of the root user enhances system security. LIDS does that. It actually does quite a few other things. It implements a very low-level security model in the kernel to provide security protection, incident detection, and incident response capabilities. For example, LIDS can: