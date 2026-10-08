
# Networking and Security

## IP Addressing 101

IP addressing (in its simplest definition) is a string of four numbers separated by periods (such as 10.1.1.1) used to represent a host (computer system) on the Internet. When a PC accesses the Internet through an ISP, it sometimes receives a temporary IP address and with that a name server assignment—something we will cover in more depth at the end of this lesson.

A hostname can only be used if you have the entry in your hosts file (remember that file from Lesson 8, “Text Editing,” working with the vi editor) or are working with a name server that will allow you to specify the IP address back to you.

## Using ssh

If you understand the concepts around telnet and how to use it, then you will have absolutely no problem understanding secure shell, commonly referred to as ssh and invoked with the ssh command. Secure shell is primarily used to log into another computer over a network, to execute commands in a remote machine, and to move files from one machine to another as you would with telnet. The difference is, ssh does it securely.

There are serious flaws in the telnet program as it is based on the telnet protocol, which is part of the TCP/IP protocol suite. Without getting involved with what the suite is, remember that you had an IP address before that you needed to connect to a remote system. Well, IP is a protocol and it has weaknesses because the version of it in use (version 4) has been around just as long as Unix has. That being said, IP wasn't made for your script kiddie/cracker/exploiter, and does not satisfy the need for greater security.

A newer version was created to replace the older version 4, but the newer version is harder to implement. Also, because of the disruption it may cause, and issues it may bring up, version 6 of the IP protocol hasn’t gained the steam it should have.

# Lesson 18

So, what is the solution? This is where ssh comes in. ssh in its simplest definition is encrypted telnet. It provides strong authentication and secure communications over insecure channels, namely the Internet, or your current network, which, believe it or not, could have a sniffer on it which could capture your packets and see your unencrypted data. Although this is highly unlikely, it is completely possible. It is a replacement for telnet and login and some other unsecured protocols conform to the same cleartext model. We will cover login next. Before we do, let's look at how to use ssh:

- > ssh 10.1.1.1
- > ssh pr1

Remember that ssh protects you only if you use it. The ssh command comes standard on most systems, but if you do not have it, ask your system administrator to set it up for you, especially if you use Unix remotely.

> ssh Usage Using the ssh command can be tricky if you have never used it. Telnet is straightforward; you enter the command and specify the host. With ssh, it may be easy if it is set up already. If not, you may get errors back. You may also need to set up encryption information on your Unix system before you use it. Just be aware of this and ask your Unix systems administrator for help if you are in a jam.

## Using login

The login command is similar to the telnet command in that it is used for remote access and that it is not secure. However, there is one major difference: login will carry some user information along with the attempt to connect.

If your account is good on several machines, they might be set up to enable you to connect between them without having to log in to each one. Try the login command as follows: login <remote machine>.

# Networking and Security 205

## Variety Is the Spice of Life

Unix students ask me, "If login is not good and we should only be using ssh, why is it still supported?" My answer is always to tell them that with everything good, there is bad, and vice versa. That's why you have variety. login can also perform well. Here is an example. I have mentioned using ssh as a way to encrypt your remote access session, but that would only protect data in transit from being intercepted and read. If password sniffing, a common attack, took place, your data would be intercepted and your credentials exposed. One way to protect yourself from this exploit is to not type your password. The program login can be configured to not require your password. If you know ahead of time that you'll be using your account from a given computer, you can create a file named .rhosts. You can make files and edit them, and put a line with the name of the computer you'll be using in that file. If you try to login using the listing in the .rhosts file, the computer will trust the computer for your account you won't be asked for your password. In effect, the computer will trust the other computer for your account if you list it in your .rhosts. This is in itself a form of security, but it won't protect you from getting your credentials snatched from someone sniffing the network.

There are also security risks associated with the use of .rhosts file. If the remote computer gets cracked into, the attacker might see this file and realize that she can now use that account to get into other systems. This could expose the remote systems. However, if you have a good Unix administrator who knows all of these dangers and how to do a risk assessment on which ones are more important to outweigh, then your system will be safe.

![](img/9552a570ce35faac09a770fd5ff1ede3_223_0.png)

# 206 Lesson 18

An example of how to use:
- > ssh 10.1.1.1
- > ssh pr1

## Using login

An alternative to login is to use slogan. The login command is similar to the telnet command in that it is used for remote access and that it is not secure. However, there is one major difference: login will carry some user information along with the attempt to connect.

## Using ssh

An alternative to login is to use slogan. The login command is similar to the telnet command in that it is used for remote access and that it is not secure. However, there is one major difference: login will carry some user information along with the attempt to connect.
