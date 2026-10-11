Although this isn't a very exciting example, it demonstrates several important features in Netcat. Try to answer these important questions before proceeding:

+   *   Which machine acted as the Netcat server?
+   *   Which machine acted as the Netcat client?
+   *   On which machine was port 4444 actually opened?
+   *   What is the command-line syntax difference between the client and server?

# 4.1.3 Transferring Files with Netcat

Netcat can also be used to transfer files, both text and binary, from one computer to another. In fact, forensics investigators often use Netcat in conjunction with **dd** (a disk copying utility) to create forensically sound disk images over a network.

To send a file from our Kali virtual machine to the Windows system, we initiate a setup that is similar to the previous chat example, with some slight differences. On the Windows machine, we will set up a Netcat listener on port 4444 and redirect any output into a file called **incoming.exe**.

```
```text
C:\Users\offsec> nc -nlvp 4444 > incoming.exe
listening on [any] 4444 ...
```
```

*Listing 82 - Using nc to receive a file*

On the Kali system, we will push the **wget.exe** file to the Windows machine through TCP port 4444:

```
```bash
kali@kali:~$ locate wget.exe
/usr/share/windows-resources/binaries/wget.exe
```

```bash
kali@kali:~$ nc -nv 10.11.0.22 4444 < /usr/share/windows-resources/binaries/wget.exe
(UNKNOWN) [10.11.0.22] 4444 (?) open
```
```

*Listing 83 - Using nc to transfer a file*

The connection is received by Netcat on the Windows machine as shown below:

```
```text
C:\Users\offsec> nc -nlvp 4444 > incoming.exe
listening on [any] 4444 ...
connect to [10.11.0.22] from <UNKNOWN> [10.11.0.4] 43459
^C
C:\Users\offsec>
```
```

*Listing 84 - Connection received on Windows*

Notice that we have not received any feedback from Netcat about our file upload progress. In this case, since the file we are uploading is small, we can just wait a few seconds, then check whether the file has been fully uploaded to the Windows machine by attempting to run it:

```
```text
C:\Users\offsec> incoming.exe -h
GNU Wget 1.9.1, a non-interactive network retriever.
Usage: incoming [OPTION]... [URL]...
```
```

*Listing 85 - Executing file sent through nc. The -h option displays the help menu*

We can see that this is, in fact, the **wget.exe** executable and that the file transfer was successful.