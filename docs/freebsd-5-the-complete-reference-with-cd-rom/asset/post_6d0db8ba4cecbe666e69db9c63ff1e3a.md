
![](img/f34d37e3abe9f4517128e54f80ab2616_527_0.png)

> **Figure 20-1**. HTML editors work much like ordinary editors, but include additional features to aid in the development of web pages.

display policies, and so on. Indeed, some browsers lack certain features entirely; for instance, Lynx is a text-based browser, and such cannot display graphics.

Fortunately, HTML was designed as a cross-platform tool. Unfortunately, HTML editors—especially flashy WYSIWYG editors and word processors—often produce HTML that’s not very portable. Such documents may include errors (misordered tags, say) that cause some browsers to misbehave. Other problems occur because of a design that makes too many assumptions about the browser’s configuration. A page may set the background color but neglect to set the text color, for instance; if a user has set the browser’s text color to something too similar to the web designer’s chosen background color, the text becomes illegible. For these reasons, it’s important that you perform several checks on your web pages, such as

-   **Syntax checking programs** Some programs can check a web page for compliance with the HTML standards. In FreeBSD, the text-based `weblint` does this job; `type weblint filename.html` to obtain a report on the compliance of `filename.html` to basic standards. Some HTML editors include similar utilities or can call `weblint` themselves. (The `weblint` program is available as a FreeBSD package or port.)

-   **Accessibility checks** Some programs and services exist to check a web page for common errors that can reduce a page’s accessibility. The most popular of these tools is Bobby ([http://www.cast.org/bobby/](http://www.cast.org/bobby/)), which can check any page on the Web. Bobby flags potential problems such as links that can blur together into one, lack of `ALT` options in `<IMG>` tags, and so on.

-   **Manual checks in multiple browsers** There’s nothing like checking a web page in a few actual browsers to see how it works. You should definitely include at least one recent version of Internet Explorer in your tests because it’s the most popular browser. I also recommend testing with Lynx, which is popular on some systems that lack GUI displays. A Lynx test is also useful in helping to produce a site that will be accessible to the visually impaired, who frequently use speech synthesizers to browse the Web. Testing on two or three other GUI browsers, such as Mozilla and Konqueror, will help as well. You should also test your page on browsers running at various screen resolutions and color depths.

With these tests finished, you can be reasonably certain that your web page won’t cause problems for your users. Of course, there’s no perfect guarantee—a browser might have a bug that causes it to crash when it receives some particular HTML sequence, even if the code is perfectly legal and acceptable to other browsers. Still, a few checks can greatly reduce the chance of your page displaying incorrectly on some browsers, and thus annoying your readers.

## Summary

FreeBSD systems make excellent web servers because the OS is stable and supports a wide variety of web server programs, including the robust and popular Apache. A basic Apache configuration is fairly straightforward because the default Apache configuration file works for a simple web server. More advanced configurations may require changes to assorted Apache options relating to directory locations, modules, and more advanced features.

Once you have a web server running, you need to give it documents to deliver to clients. This task requires creating files, which are typically formatted in HTML. You can create HTML in either an ordinary text editor or an HTML editor designed expressly to create web pages.

# The Complete Reference

![](img/f34d37e3abe9f4517128e54f80ab2616_530_0.png)

# Chapter 21

# Login Servers

Many server programs run on computers that provide their users with very limited access. For instance, people who browse documents on a web server usually don't even have accounts on the web server computer. Pull mail servers' users may have accounts on the host system, but these accounts may be restricted so that they're usable only for pull mail retrieval. This chapter covers a class of server that gives much greater access to the computer: *login servers*. These servers enable users to log into the computer and run arbitrary programs on the computer. Such servers may be run on large multiuser systems as an alternative to using many workstations; many users can then simultaneously access just one computer using low-powered terminals. Another common use of login servers is to provide users remote access to their workstations.

This chapter begins with a brief overview of the types of login servers, then moves on to a discussion of two examples each of two types of login servers. Specifically, Telnet and SSH are covered as examples of text-mode login servers, and the X Window System and VNC are described as examples of GUI login servers.

## Types of Login Servers

In the 1970s, when UNIX was young, most computing was performed using text-mode tools. This tradition remains strong in the UNIX world, including FreeBSD. Thus, remote access protocols that work primarily or exclusively with plain text can be very useful for accessing FreeBSD from a distance. If you can sit at one computer, type a command, and see the output of that command as run on another computer, you can make effective remote use of a FreeBSD system. This is the idea behind a text-mode login server; it enables FreeBSD to treat a remote computer as if it were a local text-mode console, thus extending use of FreeBSD programs to remote users.

Many text-mode login protocols are available, but this chapter focuses on just two: Telnet and Secure Shell (SSH). Telnet is the older and simpler protocol. It's included with all FreeBSD systems and focuses exclusively upon providing text-mode access. Telnet clients come with most OSs, including all UNIX-like OSs, Windows, OS/2, and Mac OS X (earlier versions of Mac OS require add-on software to be used as Telnet clients). Despite its ubiquity, Telnet isn't the best login protocol, because it transfers all data in an unencrypted form, so if the data stream is compromised, information such as passwords or any confidential data accessed during the session is also compromised. There are encrypted variants of Telnet, such as one that ships with the Kerberos security suite (`http://web.mit.edu/kerberos/www/`), but these variants have never gained the popularity of the original Telnet.

SSH is an encrypted text-mode login protocol that can actually do much more. In addition to handling text-mode logins, SSH can *tunnel* other protocols, meaning that the SSH client and server cooperate to send the other protocols' data through the SSH connection. SSH also includes built-in file transfer support. These features make SSH an extremely powerful tool and a superior choice to Telnet when security is an issue. On the down side, SSH's encryption requires some CPU time, and so can degrade performance, particularly when SSH is used to tunnel a high-bandwidth protocol.

As GUIs became popular, text-mode remote access protocols became inadequate for some purposes. For instance, X cannot run a graphics editor such as the GIMP over a text-mode protocol. Thus, new protocols emerged to handle this sort. One of these is FreeBSD's native GUI environment, the X Window System (X for short). Unlike GUIs for most other OSs, X was designed with network operation in mind, so using it for remote access is straightforward— in theory. In practice, security issues and a plethora of options for how to establish a connection can make using X remotely more complex than using Telnet or SSH for remote text-mode access.

A more recent remote GUI access tool is *Virtual Network Computing* (VNC; http://www.research.att.com/~vnc/). Unlike X, VNC is designed to support remote access to many different GUIs, including X, Windows, and Mac OS. When using VNC for remote access to FreeBSD, the system on which your programs run uses X in an entirely local manner, and VNC transfers display data to a remote system. VNC can be simpler to configure than X's native remote access tools in some situations, but this apparent simplicity hides an extra layer of complexity. VNC is also slower than X on many networks, although this problem isn't universal.

FreeBSD comes with support for all of these remote access tools, so you can pick the one that's best for you. In most cases, I recommend SSH when text-mode access is sufficient. For GUI access, both X's native tools and VNC have their advantages and disadvantages. As a general rule, when the system at which the user sits is a UNIX-like OS, X is best used directly; but VNC clients may be easier or less costly to configure on Windows or Mac OS systems, so VNC deserves consideration.

## Configuring a Telnet Server

Telnet is among the simplest and most popular text-mode remote-access protocols. For this reason, it's often desirable to run a Telnet server. On the other hand, Telnet is a notoriously insecure protocol; it encrypts no data, so anybody who can “sniff” packets on the source, destination, or any intervening system can easily obtain users’ passwords if they use Telnet. For this reason, it’s usually better to *not* run Telnet, but run the more secure SSH protocol instead.

In some cases, Telnet may be unavoidable, though; for instance, you might not be able to assume that users have SSH clients. Telnet’s risks may also be acceptable on some small private networks, such as those commonly used in residences. (Wireless residential networks are often very insecure, though, so using Telnet on such networks is inadvisable.) In case you must use Telnet, this section describes how, beginning with information on how Telnet works, moving on to how to run a Telnet server in FreeBSD, and concluding with a description of restricting access to the Telnet server to minimize its security risks.
