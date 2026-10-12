
### DISPLAY Shell Variable
- **DISPLAY shell variable** — The DISPLAY shell variable can be set to the system name and number identifying your display. After this is done, the output from any X application run from that shell will appear on the display indicated. For example, to set the DISPLAY variable to the first display on whatever, type one of the following:

```
export DISPLAY=whatever:0
```

or

```
setenv DISPLAY whatever:0
```

The first example is how you would set it on a bash or ksh shell. The second example works for a csh shell.

- **-display option** — Another method for identifying a remote display is to add the -display option to the command line when you run the X application. This overrides the DISPLAY variable. For example, to open an xterm window on a remote system so that it appears on the first display on whatever, type the following:

```
xterm -display whatever:0
```

With this information, you should be able to run an X application from any computer that you can access from your local computer. The following sections describe how you may use this information to start a remote X application.

## Launching a Remote X Application

Suppose you want to run an application from a computer named `remote1` on your local area network (in your same domain). Your local computer is `local1`, and the remote computer is `remote1`. The following steps show how to run an X application from `remote1` from your X display on `local1`.

> **CAUTION:** This procedure assumes that no special security procedures are implemented. It is the default situation and is designed for sharing applications among trusted computers (usually single-user workstations) on a local network. This method is inherently insecure and requires that you trust all users on computers to which you allow access.

1. Open a Terminal window on the local computer.
2. Allow access for the remote computer (`remote1`) to the local X display by typing the following on the Terminal window:

```
$ xhost +remote1
remote1 being added to access control list
```

3. Log in to the remote computer (`remote1`) using the following command:

```
$ ssh -l user remote1
Password:
```

Replace user with the name of the user login that you have on the remote computer. (If you have the same user name on both computers, which is sometimes the case, you can skip the -l user option. The ssh command assumes your current login name.) You will be prompted for a password.

> **NOTE:** By default, the ssh service is not enabled in Red Hat Linux. The server (in this example, remote1) must consider the security consequences of enabling remote login services. Of the available choices, ssh is considered more secure than rlogin, telnet, or other login services.

4. Type the password for the remote user login. (You are now logged in as the remote user in the Terminal window.)
5. Set the DISPLAY variable on the remote computer to your local computer. For example, if your computer were named pine, the command would appear as:

```
$ export DISPLAY=pine:0
```

(If you are using a csh shell on the remote system, you may need to type setenv DISPLAY pine:0.)

6. At this point, any X application you run from the remote system from this shell will appear on the local display. For example, to run a remote Terminal window so that it appears locally, type:

```
$ xterm -title "Terminal from Remote1"
```

The Terminal window appears on the local display with the word Remote1 in the title bar.

> **TIP:** As a rule, I use the -title option when I run remote X applications. In the title, I try to indicate the remote computer name. That way, I am reminded that the application is not running locally.

You need to remember some things about the remote application that is now appearing on your display:

- If you only use the login to run remote applications, you can add the line exporting the DISPLAY variable to a user configuration file on the remote system (such as .bashrc, if you use the bash shell). After that, any application that you run will be directed to your local display.
- Even though the application looks as though it is running locally, all the work is being done on the remote system. For example, if you ran a word processing program remotely, it would use the remote CPU and when you save a file, it is saved to the remote file system.

> **CAUTION:** Don't forget when a remote shell or file editor is open on your desktop. Sometimes people forget that a window is remote and will edit some important configuration file on the remote system by mistake (such as the /etc/fstab file). You could damage the remote system with this type of mistake.

## Securing X Remote Applications

There are several different methods available to prevent just any X application from appearing on your display. Each method offers a different level of security, as well as different amounts of setup. The major security methods that are supported include:

- **Host Access** — This method, described earlier as a default method, lets you decide which host computers can have access to your computer’s X display. Use the xhost command to indicate those computers that are allowed access (xhost +hostname) and those that are not (xhost -hostname). If you allow a host access, any user from that computer is allowed access. This security method works best with small networks and single-user computers owned by people you trust.
- **Magic Cookie** — This method, referred to as the MIT-MAGIC-COOKIE-1 method, lets you grant an individual user remote access to your display. The remote client must present a valid cookie before it can access your display.

The steps go something like this: You generate a magic cookie (using the mcookie command); you refer to the cookie when you start your X server (usually from a copy of the cookie in your $HOME/.Xauthority file); you distribute this cookie to remote computers that want to show X clients on your display; and the remote client refers to this cookie when it starts.

There are other X security methods that are also based on storing one or more randomly generated keys in the .Xauthority file. XDM-AUTHORIZATION-1 uses a two-part key — a DES encryption key (56-bit) and some random data (64-bit) — to enable access. When a system supports secure RPC, the SUN-DES-1 method can be used to enable access by setting up public and private key pairs that can be validated on a per user basis. Finally, the MIT-KERBEROS-5 method enables both the X client and X server to validate each other (using a Kerberos trusted third party).

> **CROSS-REFERENCE:** For more information about Kerberos, visit the Kerberos home page at web.mit.edu/kerberos. For general information about Linux security, refer to *The Linux Security Toolkit* by David A. Bandy (May, 2000, Wiley Publishing).

## Using Emulators to Run Applications from Other Operating Systems

Linux is ready to run applications that were created specifically for Linux, the X Window System, and many UNIX systems. Many other applications that were originally created for other operating systems have also been ported to Linux. There are still, however, thousands of applications created for other operating systems for which there are no Linux versions.

Linux can run some applications that are intended for other operating systems using *emulator* programs. An emulator, as the name implies, tries to act like something it is not. In the case of an operating system, an emulator tries to present an environment that looks to the application like the intended operating system.

> **NOTE:** The most popular of these emulators, called WINE, is not really an emulator at all. WINE is a mechanism that implements Windows application-programming interfaces; rather than emulating Windows it provides the interfaces that a Windows application would expect. In fact, some people claim that WINE stands for “WINE Is Not an Emulator.”

In the next sections, I discuss emulators that enable you to run applications that are intended for the following operating systems:

- DOS
- Windows 3.1
- Windows 95
- Windows 98
- Windows NT
- Macintosh

> **NOTE:** There is currently no product that offers a way to run Windows 2000 applications specifically in Linux. However, any application that is Win32 compatible should, in theory, be able to run using software such as WINE (described later). Whether or not a Windows application will run in an emulator in Linux must really be checked on a case-by-case basis.

Emulation programs for running DOS programs are available for Red Hat Linux. You need to install the dosemu and/or xdosemu packages (which are available from Red Hat Linux FTP sites, though not part of the basic Red Hat Linux distribution). DOS emulation commands from these packages include: dos, xtermdos, dosdebug, xdos, and dosexec. Other operating system emulation programs can be added to your system, including:

- WINE, which lets you run Windows 3.1, Windows 95, Windows 98, and Windows NT binaries. (Windows NT programs are not well supported.)
- ARDI Executor, which enables you to run applications that are intended for the Macintosh operating system.

In general, the older and less complex a program is, the better chance it has to run in an emulator. Character-based applications generally run better than graphics-based applications. Also, programs tend to run slower in emulation, due sometimes to additional debugging code put into the emulators.

## Running DOS Applications

Because Linux was originally developed on PCs, a variety of tools were developed to help developers and users bridge the gap between Linux and DOS systems. A set of Linux utilities
