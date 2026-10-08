# Chapter 8: Input Validation Attacks

Printing session values:

```
IP - 192.168.0.1
Port - 80
Min - 400
Max - 5000
Timeout - 250
Loop Pause - 0
AddRet - 2
ReOpen - true
NoReceive - true
Verbose - true
TrialRun - false
```

Beginning loop command series...
Beginning loop test with 400 byte buffer...
Connected to 192.168.0.1 .php on 80
Trial Buffer - 'GET /login.php?user=NNN...NNN HTTP/1.0
...testing continues for buffer lengths between 400 and 500...
Testing completed

As the program goes through the loop of buffer overflow tests, the target application returns errors. These errors might be "password incorrect," but some of them might indicate conditions for the "user" argument. The rule of thumb buffer overflow testing is to follow basic differential analysis. Send a normal request to an application and record the output. Send the first buffer to the application, record its output. Send the second buffer, record its output. And so on. When the output changes, examine the differences. This helps you track the specific attack (such as 7,809 slashes on the URL are are not).

In some cases, the buffer overflow attack can enable the attacker to execute arbitrary commands on the server. This is a more difficult task to produce once, but simple to replicate. In other cases, security auditing in the first case, unsophisticated script runner in the second.

> Most of these buffer overflow attacks are performed "blind." Without access to attach a debugger or view log system information, it is very difficult to craft a buffer overflow that results in system command execution. The FrontPages Extension overflow on IIS, for example, could not have been crafted without full access to a system for testing.

# Canicalization (dot-dot-slash)

These attacks target template files or otherwise reference alternate files on the Web server. The basic form of this attack is to move outside of the Document root in order to access system files, that is "../../../../../../boot.ini". The actual server (IIS and Apache, for example) is (hopefully) smart enough to stop this. Older versions of Compaq Insight Manager, however, happily allowed users to escape the Web document root.