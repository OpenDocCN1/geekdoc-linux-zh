
## USING FINGER

Finger is a nifty little tool that can tell you who owns a particular email address, or sometimes display other interesting data. As the name implies, when you use Finger you are “pointing” at someone. When you finger an address, you send a request to another system asking it to tell you everything it knows (or is willing to tell) about that address. The results of fingering vary widely from system to system, and some systems will not even honor Finger requests at all, for privacy reasons. Still, most Finger requests will return some limited information about the user, such as the user's real name or the last time the user logged in to the system. To use the Finger client from your Linux command line, enter the finger command followed by an email address, like this:

```
finger jsmith@hotdog.edu
```

Home: /user/jsmith    In real life: Janet Smith
Shell: /bin/csh
New mail received Thu May 16 13:33:18 1996;
 unread since Tue May 14 07:50:31 1996
Janet Smith (jsmith) is not presently logged in.

And as you’ll see in this next example, sometimes people connect strange things to the Net and allow you to query them via Finger...

```
finger coke@cs.cmu.edu
```

M & M          Coke Buttons
/------\        C: CCCCCCCCCCCCCCCCCCCCCCC
[?????]        C: ............   D: ............
[?????]        C: ............   D: ............
[?????]        C: ............   D: ............
[?????]                     C: CCCCCCCCCC
\------/                     S: CCCCCCCCCC
|     Key:
|     0 = warm; 9 = 90% cold; C = cold; . = empty
|     Beverages: C = Coke, D = Diet Coke, S = Sprite
|     Leftmost soda/pop will be dispensed next
----... M&M status guessed.

This example shows how to get the status of a Coke machine, which has been connected to a minicomputer and wired into the Internet at Carnegie-Mellon University!

## EMAIL HANDLING

In Chapter 10, “Managing Your Email,” you will learn about the mail and Pine programs, which are text-based email handlers on your Linux system. With a SLIP or PPP connection, you can send email to Internet addresses, but you can’t receive Internet mail directly on your system without a permanent connection and a registered domain name. The fetchmail utility is the next best thing, though, if you don’t have a permanent Internet connection. Once you have established a dial-up connection to your ISP, the fetchmail program will transfer any new mail waiting on your ISP’s mail server to a local mail folder on your Linux system. You can then read and respond to emails using your favorite Linux email client. You may find this more convenient than using telnet to log in to your ISP and checking your email with Pine. Use the man fetchmail command for usage details.

If you want to be able to receive mail directly on your Linux system, you’ll have to work with your ISP to register a domain name and get either a permanent or UUCP connection to the Internet. You can create a permanent connection (up to 56 Kbps) with a modem and a dedicated phone line, or you can install some expensive equipment and special phone connections to forge a high-speed link.

A UUCP connection is one where you occasionally dial up your ISP to send outgoing and receive incoming email messages. Any mail destined for your domain will queue up at your ISP until you dial in to receive it. UUCP is much less expensive than a dedicated phone connection to your ISP and is quite common on BBS systems in rural areas of the United States, and in other countries, where long-distance telephone costs are much higher.

Refer to the UUCP-HOWTO file and the “Help with Linux Networking” section later in this chapter for more details on UUCP

connections. (Visit the Linux Documentation Project home page on the Web at http://metalab.unc.edu/LDP to find all the HOWTO files.)

## USING PING

Ping is a simple utility that can tell you the status of another computer on the Internet and the quality of the connection between your computer and the remote host. Ping works by throwing electronic pebbles at other computers. Every computer on the Internet has a little daemon just waiting for other computers to "ping" it, and when this happens, it tries to catch the pebbles and throw them back. If the network connection is sluggish, some of the pebbles might never hit their target, and if the other computer is slow or busy, the little daemon might miss or drop some pebbles.

To use the Ping client from your Linux command line, enter the ping command followed by a domain name or IP address, like this (press CTRL-C to stop after a few lines of output):

```
ping cqu.edu.au

PING cqu.edu.au: 56 data bytes
64 bytes from cqu.EDU.AU (138.77.1.23): icmp_seq=1 time=8100 ms
64 bytes from cqu.EDU.AU (138.77.1.23): icmp_seq=2 time=7354 ms
64 bytes from cqu.EDU.AU (138.77.1.23): icmp_seq=3 time=6281 ms
^C
----cqu.edu.au PING Statistics----
13 packets transmitted, 3 packets received, 77% packet loss
round-trip (ms) min/avg/max = 6281/7245/8100
```

This output tells you three things:

- The other computer (located at a university in Australia, represented by the "au" in its address) is running and connected to the Internet. We know this because we didn’t get a "no such host" or "host is not responding" message.
- It has an IP address of 138.77.1.23. This is the value in parentheses on the second line of the output.
- The connection is lousy. We can tell this because of the Statistics section at the end of the output. We sent out thirteen pebbles, er, packets, and only three were acknowledged. The "77% packet
