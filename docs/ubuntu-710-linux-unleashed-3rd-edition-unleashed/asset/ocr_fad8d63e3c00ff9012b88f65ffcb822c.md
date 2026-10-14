# Text-Based Console Login

If you sit down at your PC and log in to a Linux system that has not been booted to a graphical login, you see a prompt similar to this one:

```
Ubuntu 7.10 (gutsy) ubuntu tty1
login:
```

Your prompt might vary, depending on the version of Ubuntu you are using. In any event, at this prompt, type in your username and press Enter. When you are prompted for your password, type it in and press Enter.

> NOTE
> Note that your password is not echoed back to you, which is a good idea. Why is it a good idea? Well, people are prevented from looking over your shoulder and seeing your screen input. It is not difficult to guess that a five-letter password might correspond to the user's spouse's first name!

# Logging Out

Use the exit or logout commands to exit your session. Type the command and press Enter. You are then returned to the login prompt. If you use virtual consoles, remember to exit each console before leaving your PC. (Otherwise, someone could easily sit down and use your account.)

# Logging In and Out from a Remote Computer

Although you can happily log in on your computer, an act known as a local login, you can also log in to your computer via a network connection from a remote computer. Linux-based operating systems provide a number of remote access commands you can use to log in to other computers on your local area network (LAN), wide area network (WAN) or the Internet. Note that not only must you have an account on the remote computer, but the remote computer must be configured to support remote logins—otherwise, you won't be able to log in.

> NOTE
> See Chapter 14 to see how to set up network interfaces with Linux to support remote network logins and Chapter 11 to see how to start remote access services (such as sshd).

The best and most secure way (barring future exploits) to log in to a remote Linux computer is to use the ssh or Secure Shell client. Your login and session are encrypted while you work on the remote computer. The ssh client features many different