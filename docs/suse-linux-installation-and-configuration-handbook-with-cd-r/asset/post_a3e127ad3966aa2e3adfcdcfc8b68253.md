
In the previous command, xxx is the last three digits of the client IP. Now, you can start X-Windows programs that will run on your Windows 9x. Enter the following command:

```
bash#xmessage "Hello from SuSE Linux Dial-In Server"
```

## Setting Up PAP

*Password Authentication Protocol (PAP)* works almost the same way as the normal login procedure. The client sends a username and password, which might be encrypted in some cases, to the server. The server checks the username and password and authenticates the client accordingly.

PAP authentication is performed through the pppd. In fact, what makes PAP such a widely used protocol is that it does not require a terminal window for a user to log in. Also, in cases in which the password is sent encrypted, the client can ensure that her password is always safe.

To set up PAP, make sure you do the following:

- Include an entry in `/etc/ppp/options` for PAP.
- Set up users in `/etc/ppp/pap-secrets`.

The entry in `/etc/ppp/options` should be the following:

```
require-pap
```

Add the following entry in the `/etc/ppp/options` to enable your SuSE Linux users to connect using their SuSE Linux usernames and passwords for PAP authentication:

```
login
```

You should bear in mind that pap-secrets works for both incoming and outgoing connections. SuSE Linux comes with a pap-secrets file that contains some pre-configuration for most of the ISPs in Germany.

To configure the pap-secrets file for inbound connections, add the entries as follows:

```
# User          Server         Secret         Address
```

The fields in this file are explained in the following list:

- User—The username the connecting client should use.
- Server—The server name, mainly, your hostname.
- Secret—A secret word or sentence in quotes.
- Address—IP address or host address of the caller.

The pap-secrets file is used in SuSE Linux to decide which users to block from using the pppd. So, you can decide which users you want to keep from using the pppd and add them to a list in the following format:

```
username hostname "* *"
```

In the previous code, username is the SuSE Linux username you want to block from using pppd and hostname is your SuSE Linux IP address or hostname.

## Setting Up CHAP

Challenge Handshake Authentication Protocol (CHAP) ensures better security because passwords always are encrypted. CHAP is more powerful than PAP in the sense that it sends requests to the client to solve the challenge sent to it during the connection time. The server sends the hostname along with a random string to the client. The client looks up the hostname and checks for the secret associated with the hostname. After the client has found the secret, it combines it with the string that was sent and encrypts them both. The client then sends them back to the server, which tests whether the results are correct. The server continues checking the client every now and then to see whether the client changed.

Setting up CHAP is as easy as setting up PAP. The secrets file for CHAP is located in /etc/ppp/chap-secrets and has the same rules as the PAP secrets file. Read the previous section "Setting Up PAP" for more information on how to set up this file:

```
require-chap
login
```

You will also have to set up the /etc/ppp/chap-secrets file as described previously.

## Limiting Services

To establish an ISP using SuSE Linux, you must set up either one of the previous configurations. We recommend that you use CHAP instead of PAP for your PPP users. An ISP usually offers more than just PPP service; some users might want to have email accounts as well. This requires different levels of configuration for each type of user.

To limit users connecting to SuSE Linux to using only email or FTP, make sure your /etc/options file does not contain the following options:

```
defaultroute
proxyarp
```

Instead, make sure it includes the following lines:

```
nodefaultroute
noproxyarp
```

Eliminating the defaultroute and proxyarp options ensures that users will be able to access only the SuSE Linux server—meaning they will only be able to grab their emails or FTP to the SuSE Linux server.

For users whom you want to be able to access the Internet through SuSE Linux, add the following lines to the .ppprc that resides in their home directories:

```
defaultroute
proxyarp
```

## Troubleshooting

*I can't dial in to my SuSE Linux. It does not answer. Why is that?*

This might be due to several reasons:

- mgetty isn't running or was run by hand. Make sure that mgetty has an entry in the /etc/inittab file as discussed in this chapter.
- mgetty isn't configured on the correct modem port. Review your configuration and make sure that mgetty is listening to the correct port.
- Make sure the number you are dialing in isn't one of the disallowed numbers if you have a caller ID installed.

*I'm trying to establish a connection through the terminal. The connection dies when I start pppd.*

This is an /etc/options misconfiguration. Some people need to have the -detach option in this file.

*I can't see any machine beyond the server. Why is that?*

The /etc/options file needs to have the following lines to make a route entry for the client:

```
defaultroute
proxyarp
```

## Setting Up SuSE Linux as a Proxy Server

### In this chapter

- What Is a Proxy Server? 392
- Installing the Squid Proxy Server 393
- Running Squid for the First Time 394
- Access Control in Squid 396
- Controlling How Squid Will Use Your System Resources 400
- Creating a Cache Hierarchy 401
- Troubleshooting 403

## What Is a Proxy Server?

The Internet is growing day by day, and is becoming more of a necessity to our lives than ever before. Speed is the buzz word these days—we all want faster Internet connections. Several techniques and technologies are currently available to meet this demand. One of these technologies is the proxy server.

A proxy server is a program that you can use to speed up the retrieval of frequently visited material on the Internet. To understand what a proxy server is, let's look at a common scenario. Let's assume that your system is configured to use a proxy server. When you attempt to visit SuSE's Web page at http://www.suse.com, your browser will send the request to the running proxy server. The proxy server will then make the connection to SuSE's Web site and retrieve the page. The server will send your browser a copy of that page and save another copy on the hard disk. The next time you want to view SuSE's Web site, the proxy server will simply send your browser a copy of the page it already has on the hard disk. The Internet connection will seem much faster to you because the page will almost immediately pop up when you send the request.

This process of keeping a copy of the pages you visit on a hard disk is known as caching. Proxy servers cache requested pages on a hard disk in case they are requested again. Proxy servers handle most of the common protocols used on the Internet, of which the most important are HTTP and FTP.

Proxy servers are used not only to speed up Internet connections, but to perform a lot of other functions, too. You can use a proxy server to allow machines that have no Internet connection to browse the Web by using a proxy server installed on one machine that does have Internet access. For example, say you have two PCs at home, and they are connected together via a network cable. One of them has a modem, but the other one doesn't. You could connect to the Internet and run a proxy server and then configure the other machine to use that server. With this configuration, both machines can browse the Web using one Internet connection.

Well-configured proxy servers can be used as a controlling mechanism for your users. A large company might be interested in setting up a proxy server that blocks access to certain non-work-related Web sites from their employees. This ensures that working hours are not wasted browsing irrelevant Internet sites.

Proxy servers have a wide spectrum of uses that are limited only by your imagination. SuSE Linux comes with one of the best proxy servers available—squid. Squid is an open source proxy server that offers very good performance and includes support for multiple proxy server uses.
