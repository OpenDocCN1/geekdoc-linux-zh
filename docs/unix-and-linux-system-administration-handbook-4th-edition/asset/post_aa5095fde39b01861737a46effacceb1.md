
Examples of restricted operations are

- Changing the root directory of a process with chroot
- Creating device files
- Setting the system clock
- Raising resource usage limits and process priorities
- Setting the system’s hostname
- Configuring network interfaces
- Opening privileged network ports (those numbered below 1,024)
- Shutting down the system

An example of superuser powers is the ability of a process owned by root to change its UID and GID. The login program and its window system equivalents are a case in point; the process that prompts you for your password when you log in to the system initially runs as root. If the password and username that you enter are legitimate, the login program changes its UID and GID to your UID and GID and starts up your user environment. Once a root process has changed its ownerships to become a normal user process, it can’t recover its former privileged state.

## Setuid and setgid execution

Traditional UNIX access control is complemented by an identity substitution system that’s implemented by the kernel and the filesystem in collaboration. The system is described in more detail on page 153; the short version is that it allows specially prepared executable files to run with elevated permissions, usually those of root. This mechanism lets developers and administrators set up structured ways for unprivileged users to perform privileged operations.

When the kernel runs an executable file that has its “setuid” or “setgid” permission bits set, it changes the effective UID or GID of the resulting process to the UID or GID of the file containing the program image rather than the UID and GID of the user that ran the command. The user’s privileges are thus promoted for the execution of that specific command only.

For example, users must be able to change their passwords. But since passwords are stored in the protected /etc/shadow file, users need a setuid passwd command to mediate their access. The passwd command checks to see who’s running it and customizes its behavior accordingly: users can only change their own passwords, but root can change any password. (This, incidentally, is yet another example of UNIX’s ad hoc access control—the rules are written into the code of the passwd command.)

## 4.2 MODERN ACCESS CONTROL

The preceding discussion leaves out a few details, but no major concepts in the traditional UNIX model have been omitted. Even though the traditional access control system can be summarized in a couple of pages, it has stood the test of time because it’s simple, predictable, and capable of handling the majority of access control requirements at the average site. All UNIX and Linux variants continue to support this model, and it remains the default approach and the one that’s most widely used today. And except when we discuss some specific alternatives, we assume throughout this book that it’s the approach you’re using.

Nevertheless, it has some obvious shortcomings:

- From a security perspective, the root account represents a potential single point of failure. If it’s compromised, the integrity of the whole system is violated. There is no limit to the damage an attacker can inflict.
- The only way to subdivide the special privileges of the root account is by writing setuid programs. Unfortunately, as the Internet’s steady stream of security updates demonstrates, it’s difficult to write truly secure software. Besides, you shouldn’t have to write custom software to express something as basic as “I’d like these three people to be able to perform backups on the file server.”
- The security model isn’t strong enough for use on a network. No computer to which an unprivileged user has physical access can be trusted to accurately represent the ownerships of the processes it’s running. Who’s to say that someone hasn’t reformatted the disk and installed their own hacked copy of Windows or Linux, with UIDs of their choosing?
- Many high-security environments enforce conventions that simply can’t be implemented with traditional UNIX security. For example, United States government standards require computer systems to forbid privileged users (e.g., those with Top Secret security clearance) from republishing high-security documents at a lower security level. Traditional UNIX security depends on the good will and skill of individual users in this regard.
- Because many access-control-related rules are embedded in the code of individual commands and daemons, you cannot redefine the system’s behavior without modifying the source code and recompiling. But that’s not practical in the real world.
- There is minimal support for auditing. You can easily see which groups a user belongs to, but you can’t necessarily determine what those group memberships permit a user to do.

Because of these shortcomings, UNIX and Linux systems have undergone a variety of interventions over the years to enhance various aspects of the access control system and to help make UNIX systems more acceptable to sites with high security requirements. Some of the adjustments, such as PAM (see page 109), now have nearly universal support. Others are relatively idiosyncratic. The following sections outline the most common extensions.
