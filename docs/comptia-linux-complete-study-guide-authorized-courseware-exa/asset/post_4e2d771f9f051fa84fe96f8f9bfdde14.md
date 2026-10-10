
The other major configuration-file class you should examine is the super server configuration. Thus, you should check your `inetd` or `xinetd` configuration files for unwanted servers. Also, unlike SysV startup scripts, super servers only launch network servers. Therefore, you should take a more aggressive approach to disabling entries you don’t recognize from your super server configuration than you do with SysV startup scripts.

On some older systems, `/etc/inittab` deserves examination. This file, described in Chapter 5, controls some of the earliest stages of the startup process. Of greatest interest from a security point of view is the fact that older `/etc/inittab` installations started the processes used to accept text-mode logins, as well as similar processes used to accept logins via dial-up modems and RS-232 serial ports. These processes are called **getty** or some variant of this, such as **mingetty**. Ordinarily, a Linux machine must have at least one such process running, and it’s controlled via an `/etc/inittab` entry such as the following:

`1:2345:respawn:/sbin/mingetty --noacnr tty1`

The first character of this line (1) specifies the virtual terminal (VT) it controls. Most Linux distributions include similar lines for the first six VTs, and there’s usually no need to adjust these lines. Lines that begin with `\#`, where \# is a number, control login via RS-232 serial ports and modems:

`S0:2345:respawn:/usr/sbin/mgetty -F -s 57600 /dev/ttyS0`

If you want to use a modem with the computer but don’t want to enable remote logins via the modem, you should ensure that `/etc/inittab` does **not** have such lines.

Modern systems that lack `/etc/inittab` or have only very basic `/etc/inittab` files typically move these functions into other files, such as SysV startup scripts or files in `/etc/event.d`. You won’t ordinarily need to modify such configurations, but you may want to check to be sure your system isn’t listening for dial-up modem connections unnecessarily. Files called `/etc/event.d/tty#` control local login access, whereas `/etc/event.d/tty#` files control RS-232 serial or modem access.

## Uninstalling or Reconfiguring Servers

Once you’ve identified an unnecessary server, your task becomes one of shutting it down. Broadly speaking, two options exist:

- You can **disable** the server by changing its SysV configuration or disabling it in your system’s super server. Consult Chapter 5 and the preceding sections on `inetd` and `xinetd` for details on how to perform these tasks. Disabling the server in this way has the advantage that you can easily reactivate the server in the future if you decide to do so. It has the disadvantage that the server’s files will continue to consume disk space, and the server might be *accidentally* reactivated in the future.

- You can **completely uninstall** the server using your distribution’s package management tools or by otherwise deleting its files. Chapter 2, “Managing Software,” describes this task. Completely uninstalling software has the advantage of reducing the risk of accidental reactivation, but it has the drawback that you won’t be able to easily reactivate the server intentionally should you decide to do so.

Overall, completely removing the server is generally preferable unless you merely want to temporarily disable a server. If you decide to reactivate the server in the future, you can always re-install it.

# Administering Local Security

Security isn’t limited to networking—local security issues can be as much of a threat as remote intruders. Thus, you should attend to some local security matters: securing passwords, limiting root access to the computer, setting user limits, and tracking down SUID/SGID files.

## Securing Passwords

A default Linux configuration relies heavily on passwords. Users’ passwords are their keys into the system, and if users are careless with their passwords, security breaches can result. Understanding these risks is critical to maintaining system security, but this is one task for which you *must* enlist the help of your users; after all, they’re the ones who are in possession of their passwords! You should also be aware of some of the tools Linux provides to help keep passwords secure. (Most of the details concerning password-related commands are described in Chapter 7, “Administering the System.”)

### Password Risks

Passwords can end up in crackers’ hands in various ways, and you must take steps to minimize these risks. Steps you can take to improve your system’s security include the following:

- Use **strong passwords.** Users should employ good passwords, as described shortly in “Choosing a Good Password.” This practice won’t eliminate all risk, though.
- Change passwords frequently. You can minimize the chance of damage due to a compromised password by changing passwords frequently. Some Linux tools can help to enforce such changes, as described briefly in “Tools for Managing Passwords” and in more detail in Chapter 7.
- Use *shadow* passwords. If a cracker who’s broken into your system through an ordinary user account can read the password file, or if one of your regular users is a cracker who has access to the password file, that individual can run any of several password-cracking programs on the file. For this reason, you should use shadow passwords stored in */etc/shadow* whenever possible. Most Linux distributions use shadow passwords by default. If yours doesn’t, consult the upcoming section “Tools for Managing Passwords” for information about enabling this feature.
- **Keep passwords secret.** You should remind your users not to reveal their passwords to others. Such trust is sometimes misplaced, and sometimes even a well-intentioned password recipient may slip up and let the password fall into the wrong hands. This can happen by writing the password down, storing it in electronic form, or sending it by e-mail or other electronic means. Users shouldn’t e-mail their own passwords even to themselves, because e-mail can be intercepted.
- Use secure remote login protocols. Certain remote login protocols are inherently insecure; all data traverse the network in an unencrypted form. Intervening computers can be configured to snatch passwords from such sessions. Because of this, it’s best to disable Telnet, FTP, and other protocols that use cleartext passwords in favor of protocols that encrypt passwords, such as SSH.
- Be alert to shoulder surfing. If your users log in using public terminals, as is common on college campuses, in Internet cafés, and the like, it’s possible that others will be able to watch them type their passwords (a practice sometimes called *shoulder surfing*). Users should be alert to this possibility and minimize such logins if possible.
- Use each password on just one system. If one computer’s password database is compromised, and if users of that system reuse their passwords on other systems, those other systems can be compromised. For this reason, it’s best to use each password just once. Unfortunately, the proliferation of Web sites that require passwords for access makes this rule almost impossible to enforce, at least without violating the rule of not writing the password down. (Modern Web browsers can remember passwords for you, but this is done by storing them in a file—essentially, writing them down.) A reasonable compromise might be to use one password for the least-sensitive Web sites (such as online newspapers) and unique passwords for sensitive Web sites (such as banking sites) and login accounts.
- Be alert to social engineering. Crackers often use *social engineering* to obtain passwords. This practice involves tricking individuals into giving up their passwords by pretending to be a system administrator or by otherwise misleading victims. Amazingly, a large percentage of people fall for this ploy. A related practice is *phishing*, in which an attacker puts up a fake Web site or sends an e-mail pretending to be from somebody else. The victim is then lured into revealing sensitive data (such as credit card numbers).

Some of these steps are things you can do, such as replacing insecure remote login protocols with encrypted ones. Others are things your users must do. This illustrates the importance of user education, particularly on systems with many users.

### Choosing a Good Password

As a general rule, people tend to be lazy when it comes to security. In computer terms, this means users tend to pick passwords that are easy to guess, and they change those passwords infrequently. Both these conditions make a cracker’s life easier, particularly if the cracker knows the victim. Fortunately, Linux includes tools to help make your users select good passwords and change them regularly.

Common (and therefore poor) passwords include those based on the names of family members, friends, and pets; favorite books, movies, television shows, or the characters in any of these; telephone numbers, street addresses, or Social Security numbers; or other meaningful personal information. Any single word that’s found in a dictionary (in *any*)
