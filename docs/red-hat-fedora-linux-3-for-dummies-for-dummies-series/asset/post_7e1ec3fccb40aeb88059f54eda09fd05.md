
You can choose from many techniques and software programs for making backups, but that’s a topic we couldn’t possibly begin to cover in this book. We wouldn’t be able to cover Fedora Core if we even began to go into detail. One great book that covers Fedora Core in great detail is *Red Hat Linux Bible: Fedora and Enterprise Edition*, by Christopher Negus (Wiley).

For example, the following commands use the ubiquitous Linux *tar* package archive (*tar*) command to create an archive of your home directory. You can then use the OpenSSH *scp* command to securely copy the archive to another location, such as your ISP account or another computer you have access to.

Follow these steps to create an archive of your home directory:

- **Log in to your user account.**
- **Run this *tar* command:**

```
tar czf mybackup.tgz
```

In this case, the *c* option means to use *tar* to create a new archive. The *z* option tells *tar* to compress the data. The *f* option defines the text that follows, *mybackup.tgz*, as the file to copy the files to. The single dot (.) says to copy to the archive all files in the current working directory.

- **Use OpenSSH to copy the *tar* archive to another location:**

```
scp mybackup.tgz myloginaccount@myisp.com
```

This command securely copies the *tar* archive to the account *myloginaccount* at the ISP *myisp.com*.

## My Buffer Overflow

Beneath the surface, computer programs — applications — are made up of many subprograms known as subroutines. *Subroutines* allow programmers to divide into many smaller tasks the task a program is to perform. Designing big or small programs without subroutines would be impossible.

Whenever a program calls a subroutine, or a subroutine calls a subroutine, information can be passed between the two via the stack. *A stack* is like a can of tennis balls: The first ball pushed into the can is the last one taken out. This type of stack is called *first-in-last-out*. (Other variations are possible, such as *first-in-first-out*.) Stacks turn out to be quite efficient for transferring information: Memory is consumed when transferring information to a subroutine and then automatically released when the subroutine finishes. Stacks are also referred to as *buffers* and *queues*.

Although stacks make programming with subroutines efficient, they're vulnerable to a hacking technique called *buffer overflows (or stack-smashing)*. Overflowing a buffer is one of the most popular methods hackers use to break into computers. The idea is to feed seemingly crazy streams of code, in binary form, to a program in order to make them behave in ways their designers never intended.

Here’s how buffer overflows work:

- The character stream overflows the intended boundaries of the subroutine’s buffer.
- When the subroutine finishes, it reads the return address of the calling program or subroutine off the stack.
- But the false return address executes the malicious hacker code — and you have been hacked!

A little more has to happen for the hacker to be successful, but you get the idea. When a hacker finds and exploits a vulnerable program, he gains access to your computer. Sometimes that access comes in the form of superuser (*root*) access! Yikes!

Here are some simple techniques you can use to minimize buffer overflows:

- **Your first line of defense is simply to minimize the number of services you run.** You run zero risk of compromise from a buffer-overflow vulnerability in any particular service *if you don’t run that service*.
    - For example, the Lion worm wreaked havoc in Spring 2001. Lion took advantage of a vulnerability in the Linux *sendmail* and *Lpd* printer services. Computers that didn’t run those services weren’t vulnerable to the Lion worm.
- **Your second defense is to update your Fedora Core computer as often as possible.** Fedora Core posts package updates (as they become available) that fix vulnerabilities. Buffer overflow fixes comprise many of the package updates. Updating your system fixes many buffer overflow vulnerabilities.
    - Click the red exclamation button on the GNOME Panel to start the update service. You can also run the command **yum update** to accomplish the same function.
- **Your last defense is the new stack-protection system named ExecShield.** ExecShield places a canary in the stack. *A canary is a number that, if overwritten by a buffer overflow, creates an invalid state for the calling software.* The software that called the compromised subroutine sees the invalid state, and can decide to exit before any damage is done.

## Chapter 21: Ten Security Vulnerabilities and Their Fixes

ExecShield is included in the Fedora Core kernel. When ExecShield is enabled, it prevents sections of a program, including its stack, from executing code or other programs. Some sections of a program (such as data) shouldn't be executable — and that includes the stack, of course.

ExecShield provides three modes of operation:

- **Disabled:** ExecShield is disabled and doesn't affect your computer's operation.
    - You manually configure Linux to disable ExecShield by logging in as root, starting the GNOME Terminal, and running this command:

```
echo 0 > /proc/sys/kernel/exec-shield
```

    - Alternatively, you can add the following option to the /etc/sysctl.conf configuration file to turn ExecShield off at boot time:

```
kernel.exec-shield = 0
```

- **Enabled for marked binaries only:** This mode, the default, enables only enabled programs — binaries to work with ExecShield. You may want to use this mode with, for example, a Web server. You would protect your most vulnerable services with ExecShield and not worry about, for example, your Mozilla browser.
    - This mode of operation is the default for ExecShield. However, if you have changed to another mode, you can reset this mode by logging in as root, starting the GNOME Terminal, and running this command:

```
echo 1 > /proc/sys/kernel/exec-shield
```

- **Enabled for all binaries:** In this mode, all programs on your computer use ExecShield. Because ExecShield is relatively new, we recommend this mode only for experimenting.
    - You can manually configure Linux to use this higher level of security by logging in as root, starting the GNOME Terminal, and running the command `echo 2 > /proc/sys/kernel/exec-shield`. Alternatively, you can add the option `kernel.exec-shield = 2` to the /etc/sysctl.conf configuration file to set ExecShield to its maximum level at boot time.

You can find out whether a program is compatible with ExecShield. Use the program execstack to query and set programs to use ExecShield. For example, enter the command `execstack -q /sbin/*` and you see that a few files, such as GRUB, are compatible; the capital X in the first column indicates that the file has been compiled with the ExecShield hooks. You can set GRUB to use ExecShield by typing `execstack -s /sbin/grub`. You should eventually see more programs become ExecShield-compatible.

ExecShield can also randomize the location where programs are loaded into your computer's virtual memory. A hacker can exploit the knowledge of where a program is loaded into your computer's memory. Linux loads programs at fairly predictable locations, but ExecShield mostly fixes the problem.

ExecShield randomizes Linux memory by default. Woo-hoo! You can manually configure the ExecShield random function: Log in as root, start the GNOME Terminal, and run the command `echo 1 > /proc/sys/kernel/exec-shield-randomize`. Alternatively, you can add the line `kernel.exec-shield-randomize = 1` (or `0`) to `/etc/sysctl.conf` to automate the process at boot time.

## Social Engineering

Hackers don't have to discover supertechnical tricks to break into your computer. Many smart hackers aren't deterred when they encounter a well-protected computer or network. What does a poor hacker in these security-aware times have to do to break into your system? Not all that much.

Some hacker techniques don't rely on technological means. One such technique is social engineering, which is a fancy way of saying "I plan to trick you or your associates into giving me information that I will use against you."

Social engineering can be as simple as a hacker calling you to see whether you're at home or in the office. If you're not physically present, the hacker can drop by, or break in, and simply steal your computer or its disks. A hacker who's not that bold may be able to gain access to a computer by tricking a help desk technician into resetting a password. The idea is to gain access or control of your computer or network in unexpected ways.

![](img/41feae212f5c6612ff709354891f7b39_327_0.png)

Another social-engineering technique hackers employ is to call a corporation's help desk and pretend to be a VIP. The poor minimum-wage employee can often be bullied or cajoled into giving out a password or other important information.

The moral of the story is to exercise good security hygiene and be careful of strangers. Don't give out information unless it's essential and you can verify the authenticity of the request.

## Bad Passwords

The vulnerability that's probably the easiest to avoid, and most often abused, is poor or non-existent passwords. Passwords are your first line of defense. If your password is easily guessed or — even worse — blank, someone will break in.

Bad passwords are easy to fix. Start by assigning a password to every account you create — especially root. Then make it a habit to use "good" passwords. Passwords can be cracked by brute force because computers
