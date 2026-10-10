
## Chapter 3: An Overview of the System

Enter your password at this prompt, and then press ENTER again. As a security measure, you won't see your password echoed to the screen. (The security benefit is that nobody lurking nearby sees it, either.) If you enter the correct password, FreeBSD displays a screenful of information about where to find security advisories, FreeBSD documentation, and so on. At the bottom of the screen you'll see a command prompt, which is probably a single dollar sign ($). The root account's prompt is a pound sign (#), though, to help you identify when you are logged in as root. Depending upon your account's configuration, you may see additional information just prior to the prompt, such as your username or the name of this shell.

A text-mode login such as this allows you to run text-based programs and use text-mode commands, as described in the upcoming section, "A Summary of Text-Mode Commands." Sometimes you may want to run multiple text-mode programs. Two common ways to do this:

- **Virtual consoles** FreeBSD supports a feature known as virtual consoles, which enables you to log in several times. After you've logged in once, press F2, or any other function key up to F8. You'll see another login: prompt, and you can log in a second time. Press F1 to return to the first virtual console. You can then run different programs in the different screens. You can even log in as different users in the different virtual consoles. (Once you start running X, as described later in this chapter in the section "Starting X," you must press ALT together with the function key to switch to another virtual console. X itself runs in the 9th virtual console, accessed via F9.)
- **Background processing** You can run one program in the background, meaning that it no longer receives your keyboard input. To do this, append an ampersand (&) to its command name when you run the program, as in `numbercrunch &`. Alternatively, you can suspend a program's operation by pressing CTRL-Z when it's running; this stops the program without killing it and returns you to a command prompt. This step is particularly useful if you want to temporarily exit from a program and then return to it; typing `fg` gets you back into the program, and typing `bg` sets it running in the background, as if it had been started with an ampersand to begin with.

If you log in using text mode, you won't be able to run GUI programs without first starting the X Window System (or X for short), as described in the upcoming section, "Starting X." You can configure a FreeBSD system to automatically start X when the system boots. Such a system uses the X Display Manager (XDM) program, or a similar tool, to provide a GUI login screen, as shown in Figure 3-1. When you type your username and password in this screen, FreeBSD automatically starts your X environment. You may prefer such a configuration if you do most of your work in X. Properly configuring such a setup requires starting the XDM program in one of the startup scripts, and you may need to adjust users' individualized X configurations, as well. Chapter 21 describes how to configure XDM or similar programs, and Chapter 6 covers users' login control files, including those for use with XDM.

![](img/f34d37e3abe9f4517128e54f80ab2616_113_0.png)

### User vs. root Accounts

As described in Chapter 2, you're likely to use at least two FreeBSD accounts: an ordinary user account and the root account. You employ a user account for day-to-day user tasks, such as reading e-mail, browsing the Web, using a spreadsheet, and manipulating graphics files. The root account is the account used by the system administrator, aka the *superuser*. This account provides more-or-less unlimited control of the computer; root can read, write, move, or delete any file on the system. For most tasks, you should use an ordinary user account; reserve root logins for the times when you need to administer the system.

> In this book, commands you type are shown after a prompt. In most cases, this prompt is either a dollar sign ($) or a pound sign (#), signifying the command's use from a user account or as root, respectively. This mirrors the default prompts displayed on the screen when you're logged in as an ordinary user or as root.

It's not uncommon to find that you've logged in as an ordinary user, but need superuser privileges for some short action. This problem can be overcome in several ways. One is to use FreeBSD's virtual consoles to log in as root, perform whatever action you need to do, and log out again. A procedure can be awkward if you're running in X and want to run a program that requires root privileges alongside other programs, though. Even when running in text mode, there's a method that's often simpler: `su`.

The `su` program name stands for substitute user. It's a method of changing the identity of a user who's already logged in. It can take several options and parameters:

```
su [-] [-f|-fm] [-c class] [username [args]]
```

> FreeBSD documentation often lists command syntax as in this example. Square brackets indicate a parameter that's optional. Single-character options within brackets can be added or deleted individually (as in -f|-fm in this example; you can use just -f, just -l, just -m, or any combination you like). Italic indicates variables. Ellipses (not shown here) indicate that an option may be repeated. A vertical bar (|, also not shown here) separates two alternatives that aren't used together.

The simplest use of `su` is to type it alone, as in `su`. If the user who types it is in the wheel group, `su` prompts for the `root` password. If the user types this password correctly, the user acquires superuser privileges. If you enter a username on the `su` command line, you acquire that user's identity. In either case, typing `exit` ends the identity change. You can further modify `su`'s behavior by adding various optional parameters:

- **`-l` or a single dash (`-`)** Ordinarily, `su` creates an environment that's not quite identical to a normal login environment. The `-l` option (or a simple dash by itself) discards most of the user's current environment and creates a new one that should match the target user's normal environment.
- **`-f`** If the target user uses `csh` as a shell, this option causes `su` to not read the `csh` configuration file, `.cshrc`. You can use this to make the target environment less like the target user's normal environment.
- **`-m`** This option changes your identity without changing your environment at all. For instance, you'll continue to use your normal command shell, even if the target user normally uses a different one.
- **`-c class`** FreeBSD supports login classes, which are similar to groups. You can specify a class whose settings you want to use.
- **`args`** If you want to pass arguments (control parameters) to the target user's command prompt shell, you can do so by placing them at the end of the `su` command.

You'll find that `su` is an extremely useful tool for administering FreeBSD. Using `su`, you can log in as an ordinary user and run privileged programs when necessary by first typing `su`. This procedure works both from text-mode logins and from GUI logins once you've started a window in which you can enter commands.

You can log in directly as `root` at the console, but as a security measure, FreeBSD doesn't accept remote logins via Telnet as `root`. This restriction means that a remote attacker who knows the `root` password must also know another user's password to invade the system—a would-be attacker must log in as an ordinary user and then use `su` to acquire root privileges. Of course, the same is true of authorized administrators, which may be an inconvenience. Nonetheless, the increased security is worth this inconvenience. Indeed, even at the console, it's best not to log in directly as `root`. When you use `su`, FreeBSD logs the fact, including the user who issued the `su` command. This logging can help you track who's doing administrative tasks, which may be important if you find that somebody's abusing superuser power.

### A Summary of Text-Mode Commands

Because FreeBSD defaults to starting up in text mode, this chapter's first real description of FreeBSD tools focuses on text-mode operations. This topic begins with a description
