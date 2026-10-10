
## 2 Your UNIX Account

In one respect, UNIX is like your local bank. Just as you need a bank account to withdraw money (legally) from a bank, you also need an account to use a UNIX computer. In this chapter, you will learn what you need to know to obtain and begin using a UNIX account.

### 2.1 Your System Administrator

Every bank has a manager who sets bank policy, opens and closes customer accounts, balances the books, and generally sees that the bank operates smoothly. Of course, the manager does not necessarily do all of these things personally, but the manager is responsible to see that someone does.

Similarly, most UNIX installations have a *system administrator*, who sees that the system runs smoothly (most of the time, anyway). The system administrator’s duties include:

- Setting up the hardware.
- Installing software, including the UNIX operating system.
- Starting up the system (and shutting it down when necessary).
- Monitoring system usage.
- Backing up users’ files.
- Creating new user accounts.
- Troubleshooting.

The system administrator does not necessarily do all of these things personally—large computer installations typically divide these duties among several persons. Thus, when you read “system administrator,” think “the system administrator or one of his or her assistants.”

### 2.2 Your Account Name

A large UNIX installation may serve hundreds or thousands of users, each having his or her own account. To identify these accounts, each is given a unique name, which is typically based in some way on the user’s real name or nickname. For example, the following would all be likely account names for a user named John P. Jones:

- j_pjones
- jonesjp
- jones
- johnp
- jpj
- sparky

The policies for assigning account names vary. In some organizations, the system administrator chooses the name for you; in others, you may choose your own, subject to certain rules. The following rules are fairly typical:

- Select a name that is at least three characters long, but no more than eight characters long.
- Be sure that no other account has the same name.
- Choose an account name that is related in some way to your real name or a nickname.
- Use only numbers and lowercase letters; do not include uppercase letters or punctuation.

When you start a work session on the computer, you will be asked to *log in* by giving your account name:

```
login:
```

Because you use your account name when logging in, your account name is often referred to as *your login name or login*.

### 2.3 Your Password

Your login name is public knowledge. To prevent unauthorized use of your account, the computer also asks you for a *secret password*:

```
password:
```

By entering your password, you verify to the computer that you really are the person to whom the account belongs.

The system administrator will probably choose your first password for you. After that, you can (and should) choose your own password. A good password is one that is easy for you to remember, but difficult for someone else to guess. Here are some good general guidelines for selecting a password:

- Choose a password that is at least six characters long. (Passwords can be as long as you like, but some systems only examine the first eight characters.)
- Combine numbers, upper- and lowercase letters, and punctuation.
- Make the password memorable, but avoid common names and words.
- Do not use your social security number, your telephone number, your login, or any variation (forward or backward) of your login.
- Make sure a new password differs significantly from the old one.

A number of strategies exist for choosing a password. One is to misspell an easily remembered word or name. For example, neither Ch*cago nor ch*cago would be acceptable as passwords. But the following deliberate misspellings would be:

ch*KagoH
Ch*.CAG_O
Sheekago
She?kago

Another strategy is to form a password from the first letter of each word in an easily remembered phrase. Including punctuation is a good idea. For example:

N*My*d! (*Not in My yard you don't!*)
Ihnybt*f (*I have not yet begun to fight*)
H*otr (*Home, home on the range*)
wt*dat*p (*where the deer and the antelope play*)

Your password is the main line of protection for your account. Anyone who discovers your password can do nearly anything to your account—including deleting all of your files. Therefore, it is extremely important that you keep your password secure.

![](img/52d592fcd97ba67dcb2b4a36fde4eb4c_24_0.png)

If you suspect that someone else has learned your password, you should change it immediately. In fact, it may be a good idea to change your password occasionally in any case, just to be safe.

### 2.4 Other Account Information

When your account is created, the system administrator sets up the following information in addition to the login name and password:

- **Home Directory.** Your home directory is the place where all of your other files and directories reside. The home directory has a name, which is the same as your login name.
- **Group ID.** You may be assigned to a group of users. In some organizations, groups are set up so that users in the same department or working on the same projects can easily share files.
- **Login Shell.** Three UNIX shells are commonly used: the Bourne Shell, the C Shell, and the Korn Shell. The system administrator will select one of these to start up automatically whenever you log in.

When you receive your UNIX account, be sure to ask what groups (if any) you have been assigned to and what your login shell is.

### 2.5 More Questions to Ask

There are a number of additional questions you should ask your system administrator:

- Which version of UNIX will I be using?
- What kind of terminal will I be using? What is its term info code?
- What are the erase, interrupt, stop, and continue keys?
- Which printer(s) may I use?
- How can I gain access to the system?

The rest of this chapter will explain what each of these questions means.

### 2.6 Versions of UNIX

When we say UNIX, we are really talking about a family of operating systems. Most can trace their ancestry to AT&T System V or Berkeley Software Distribution (BSD) UNIX:

| Name | Supplier | Based on |
| :--- | :--- | :--- |
| AIX | International Business Machines | AT&T System V |
| A/UX | Apple Computer | AT&T System V |
| Dynix | Sequent | BSD |
| HP-UX | Hewlett-Packard | BSD |
| Irix | Silicon Graphics | AT&T System V |
| Linux | Free Software Foundation | |
| NextStep | Next | BSD |
| OSF/1 | Digital Equipment Corporation | BSD |
| SCO UNIX | Santa Cruz Operation | AT&T System V |
| Solaris | Sun Microsystems | AT&T System V |
| SunOS | Sun Microsystems | BSD UNIX |
| Ultrix | Digital Equipment Corporation | BSD UNIX |
| Unicos | Cray | AT&T System V |
| UnixWare | Novell | AT&T System V |
| XENIX | Microsoft | AT&T System III |

Keep in mind that these UNIX versions are very similar; if you learn to use one, you should have little trouble with any of the others.

> Ask your system administrator whether your system is based on AT&T or BSD UNIX.

### Why So Many Versions of UNIX?

When UNIX was under development at AT&T’s Bell Laboratories in the 1970s, AT&T was still prevented by federal law from competing in the computer industry. Since the company could not make a profit on UNIX, they gave it away, essentially free of charge.

UNIX became very popular at colleges and universities, where it was used for both teaching and research. (The low price tag undoubtedly had something to do with this popularity.) The early versions of UNIX were still quite crude, so academic computer scientists introduced their own improvements. Especially prominent in this effort was the Computer Systems Research Group at the University of California at Berkeley, which began producing its own versions of UNIX. By 1982, Berkeley Software Distribution (BSD) UNIX rivaled the AT&T versions in popularity.

Meanwhile, many computer companies produced their own versions of UNIX, often borrowing features from both AT&T and Berkeley UNIX. Of course, each version had its own name, usually ending in x (AIX, A/UX, HP-UX, Irix, Ultrix, and XENIX, to mention a few.) At one time there were as many as 200 variants of UNIX on the market.

Although similar in most respects, the many versions of UNIX had enough differences to cause headaches for programmers, vendors, and users. To make life easier for everyone, an industry group was formed to define a UNIX standard. The first Portable Operating System Interface (POSIX) standard was formally adopted in 1988. Since then, most of the major vendors of UNIX operating systems have been modifying their systems in accordance with the POSIX standards.

AT&T was also conscious of the need for standardization. In 1989, AT&T System V (“System 5”) Release 4 appeared. System V Release 4 (abbreviated “SVR4”) combined the best features of the four most popular UNIX derivatives, which were SVR3, 4.3BSD, SunOS, and Microsoft Xenix.

In 1993, the Computer Systems Research Group at Berkeley announced it would cease operations with the release of 4.4BSD. However, the Open Software Foundation (OSF)—a consortium of major computer manufacturers that includes IBM, Digital Equipment Corporation, and Hewlett-Packard—continues work on operating systems based on BSD UNIX.
