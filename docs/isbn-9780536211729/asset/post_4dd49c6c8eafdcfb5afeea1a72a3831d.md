
## USING SWATCH TO MONITOR SSH LOGIN FAILURES

In 2004 and 2005, a number of brute-force login attempts were noted against servers running SSH. These usually didn’t result in much of anything except annoyance. However, it’s generally useful to monitor log files for these and other attempts to brute-force attack a server. Swatch can be configured to send an email (or do any number of other actions) when such an attempt is logged. This section shows how to send an email alert when an authentication failure is logged.

The system logs a line similar to the following when a login is attempted and fails:

```text
Jun  7 17:09:10 ord sshd[3434]: error:
  PAM: Authentication failure for root from 192.168.1.10
```

There are a number of unique items on this line, but I’ll choose to look for the words “Authentication failure” because that is the type of thing I want to be alerted on. The Swatch syntax is painfully easy yet can be incredibly powerful. This is because Swatch uses regular expression syntax for matching. The match in this case is rather trivial. Simply telling Swatch what to watch for with the aptly titled watchfor configuration directive and then giving it one or more actions to perform when a match is noted is all that’s required for Swatch configuration. For example, to look for the words “Authentication failure” and have an email sent, the Swatch configuration consists of the following:

```text
watchfor /Authentication failure/
  mail
```

These two lines are saved in ~/.swatchrc. In this case, I’m doing so as root because Swatch will need read access to the log file in question.

Next, start Swatch and tell it what file to monitor. Again, the default is /var/log/messages. However, I’m creating this example on a Debian system and therefore the authentication failures are logged to /var/log/auth.log by default. Therefore, I point Swatch at the correct configuration file and start it:

```bash
swatch -tail-file=/var/log/auth.log
```

Swatch will now monitor the log file for the words “Authentication failure” and will send an email to root if and when the words are found.

As previously stated, there are several options for alerts, including executing other programs. These programs could be shell scripts or really anything, so the possibilities are virtually limitless.

## 10.5 How to Not Become Compromised

Virtually nothing can be done to stop an attacker with unlimited resources and unlimited time. From DoS attacks to rootkits to physical attacks, if someone wants at your data badly enough, chances are that he can get to it, given no other constraints. That said, there are many things you can do to limit your exposure to most risks.

Neither this chapter nor this book deals with *physical* attacks on any level. If an attacker is onsite and can simply walk off with the computer or hard drive containing the data, there's no amount of firewalling that will help. If the attacker has physical access to the computer or device holding the data, the attacker can steal the data itself or possibly plant his own malicious trojan software.

This section gives some general suggestions that are *field-tested* to keep systems secure. The suggestions given here are by no means all-encompassing; rather they are merely things I suggest to help ensure system integrity.

### 10.5.1 Secure Often

Securing the computing environment is a continual process rather than an endpoint. As you work to secure systems and networks, new vulnerabilities are being discovered and new software is being developed. There is simply no magic bullet that enables you to be done and complete when it comes to securing a computer environment. This book has been devoted to securing a network and its systems through the use of a firewall built on Linux. This chapter has introduced some of the other aspects of a security-in-depth process.

Using the tools available to you, such as those already introduced in this chapter, you can secure a computer and the network on which it resides. There are, of course, additional steps you can take to further enhance the security of the environment.

#### KERNEL ENHANCEMENTS

There are certain things you can do with the Linux kernel to enhance its security. Naturally, anything you do at this, the lowest, level of the operating system will only serve to help the security of those things above it.

#### BASTILLE LINUX

Bastille Linux is a program that helps automate the process of system security as well as report on the security of the system. Bastille Linux implements many of the security best practices that you could find by reading volumes of material and countless websites. All of those best practices are implemented through a wizard-like interface (command-line or GUI) that contains a lot of information on not only what you're being asked but why it's important.

Bastille Linux goes so far as to give recommendations for certain features. Unlike many tools that try to give recommendations, Bastille gets it right by explaining the reasoning behind the proposed change, as well as the implications that it might have if you choose to use the step.

Finally, Bastille also includes an undo process so that you can quickly undo any changes that might be causing problems. Bastille is welcomed by experienced Linux administrators and those new to Linux alike. Some Linux distributions include Bastille as a package. More information on Bastille Linux can be found at http://www.bastille-linux.org/.

### 10.5.2 Update Often

Although by far the most effortless of any task in this book, keeping a computer system up-to-date is an often-overlooked aspect of system security. The best way to ensure that a computer will be broken into is to leave it running without updating it.

One of the greatest strengths of Linux and open-source software is security. Some attempt to argue that this security is achieved because open-source software is less popular. Of course, this completely ignores market-share statistics such as Netcraft’s web server survey showing that Apache holds nearly 70% of the web server market.

Part of this security strength comes from the open-source community’s ability to provide fixes within hours of the security disclosure. It’s quite common for fixes to be available the same day as the disclosure, even for security issues that weren’t previously disclosed. In events in which a fix might take a little time, the community has historically been excellent at providing workarounds to mitigate and sometimes eliminate the vulnerabilities entirely.

Both of these characteristics, quick fixes and quick workarounds, work to your advantage in maintaining system security. However, for either one to be of use, you need to keep track of their availability by monitoring mailing lists and security websites. Most major Linux vendors offer announce-only security mailing lists in which subscribers receive an email whenever a vulnerability is disclosed. In addition, there are other industry mailing lists that can keep you up-to-date on security issues.

Keeping software up-to-date is an important aspect of system security. I recommend updating as often as possible while obviously paying attention to the software that’s being updated to ensure that none of the updates breaks live systems.

### 10.5.3 Test Often

It’s not enough to secure often and update often, though those two items certainly go a long way toward ensuring a secure environment. Another basic point of security in-depth is to test often. Testing ensures that the security policies are being enforced and the implementation of those security policies is successful.

Penetration testing is another important aspect of system security. Penetration testing, or pen-testing, is a process by which the security of a system is tested by trying a number of attack vectors to get the system to behave in an unexpected way. The definition of penetration testing is purposely vague so that it is not limited to attacks of only a certain class or type.

Penetration testing can be both informal and formal. The informal pen-tests are typically run by security administrators or even developers using anything from manual attempts to break into an application to automated attacks using a number of tools. A formal pen-test would be done by a third party who would likely use a combination of both manual and automated attacks to test the system. The type and frequency of pen-testing is a matter for your security policy.

Of course, when you do test, it’s important to test both types as if you were a normal attacker and as if you were an insider. Testing as a normal attacker means testing the application from the outside, just as a hacker would.
