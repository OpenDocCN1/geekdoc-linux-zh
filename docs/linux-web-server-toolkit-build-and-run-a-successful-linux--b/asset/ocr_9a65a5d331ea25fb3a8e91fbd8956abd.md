# Linux Web Server Toolkit

some ISPs do not use PPP. But PPP has at least two security methods to guarantee that you are the one authorized to connect to the PPP server at the ISP. One is called Password Authentication Protocol (PAP); the other is the Challenge Handshake Authentication Protocol (CHAP). I'll describe the second, as you're more likely to see it in use.

CHAP uses a secret phrase that is stored on both computers. It is encrypted and compared during the PPP connection process (the command in the section). If the phrases don't match, the connection is dropped.

You have to coordinate the secret phrase with your ISP. With the secret key can control access from one or many PPP systems to one or many PPP systems. When your ISP gives you a pass phrase, create a text file called /etc/ppp/chap-secrets. The file can contain the following line:

```
www.mydomain.com myisp.com_pass_phrase
```

# AUTOMATING YOUR CONNECTION

A modem connection is inherently not as stable as a digital connection, but it can remain up for days or weeks at a time without problems. When you want the system to come up as effortlessly as possible.

Assuming that your Web server is operating full-time and that you have a dedicated connection to your ISP, you would want your modem-based PPP connection to the Internet to come up whenever the connection is turned on.

To do this, add the ppp command from the previous section to the end of the file /etc/rc.d/rc. The ppp command will be executed each time the system boots and make your ISP connection immediately, before anyone logs in the system. You can also try using the dial command, which automatically calls your ISP and makes a PPP connection whenever someone makes a request for an Internet connection. Follow the dial man page for more information (enter dial at any command prompt).

# Other Types of Connections

Other connections are not nearly as easy to set up as a modem connection. That may sound discouraging after reading all the details of the previous section. There's so much to know, and so many options, that I can't explain all here. I provide some direction, however, to get you started.

If you're going to use a digital Internet connection (described in the next section), this is about the best piece of advice I can give: develop a good relationship with your ISP technical staff and find a knowledgeable sales person to guide you through the maze that is your local telephone company. It wasn't long ago that you could call your telephone company's business service numbers and talk to ten people before you found anyone who knew what ISDN is. The Internet has become too large a part of their business for that to happen now, but