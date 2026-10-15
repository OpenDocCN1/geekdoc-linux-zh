
and see whether I have a certain file there:

Click here to view code image

```
$ ssh intuitive.com
The authenticity of host `intuitive.com (104.131.46.171)` can't be established.
RSA key fingerprint is
34:ba:0e:84:e8:ef:82:59:7c:91:2e:8f:0b:
2e:50:08. Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added `intuitive.com,104.131.46.171` (RSA) to the
known hosts.
daylor@intuitive.com's password: _
```

If you’ve never connected to a particular remote host via SSH, you can see that it uses public key encryption and so needs to establish a shared encryption key. To do this, you need to indicate your trust that the remote system is the machine you think it is, which is what the prompt shows. You can also see that I have answered yes, which is needed only once per remote system.

By default, ssh assumes that your account on the remote system has the same name as your account on your home system. If you need to use a different account name, specify it with the -l account option:

Click here to view code image

```
$ ssh -l dave intuitive.com
dave@intuitive.com's password: _
```

After I enter my password, I’m logged in to the remote system:

Click here to view code image

```
Last failed login: Tue May 26 18:14:27 EDT 2015 from ip-64-134-29-252.public.wayport.net on ssh:notty
There was 1 failed login attempt since the last successful login.
Last login: Thu Apr 30 18:12:27 2015 from c-98-245-91-148.hsd1.co.comcast.net
[taylor@ado105 ~]$
```

Using ls tells me what I want to know:

Click here to view code image

```
[taylor@ado105 @]$ ls
Global.Software   News/             history.usenet.Z
Interactive.Unix  Src/              login
Mail/             bin/              testme
[taylor@ado105 @]$
```

2. The ssh command offers a shorthand notation for logging out of the remote system; instead of using logout, you can simply enter ~. to do the job. To stop the ssh session, use ~^z.

I choose to log out the normal way:

Click here to view code image

```
[taylor@ado105 @]$ exit
Connection to intuitive.com closed.
$
```

Now I’m back on the original computer system.

3. Turns out there are a number of the tilde commands available, which you can learn about by typing ~ ? at any point during the SSH connection:

Click here to view code image

```
~?
Supported escape sequences:
~ .  - terminate connection
~ B  - send break (SSH protocol 2 only)
~ C  - open a command line
~ R  - Request rekey (SSH protocol 2 only)
~ ^Z - suspend ssh
~ #  - list forwarded connections
~ &  - background ssh (when waiting for connections to terminate)
~ ?  - this message
~ ~  - send the escape character by typing it twice
(Note that escapes are only recognized immediately after newline.)
[taylor@ado105 @]$
```

The ssh command is fast and easy, offering a simple way to jump onto a remote system and use the command line, including screen-oriented programs like emacs or the vi editor. It’s the functional equivalent of using VLC or RDP to get a remote GUI session to a Windows machine or Mac; but because Unix is command-line driven, a textual terminal gives you all the functionality of being on the machine locally with none of the need for heavyweight telepresence servers to be installed on the remote machine. I use it quite frequently.

Sure, you could still use telnet or its partner program rlogin, but both of those have security problems that make them poor choices in this modern era of widescale computer hacking and system break-ins. It’s best to ensure that they’re disabled on the server itself and just learn ssh!

## Task 21.2: Third-Party SSH Connections

I’ve already pointed out the security problems with telnet and its ilk. There are important considerations, not the least of which is that the information between the client and the server is “in the clear.” That is, if you could somehow interpose a network packet sniffer that could filter out just the telnet traffic, you could read the account/password pair and everything that’s displayed on the remote user’s display.

Although a number of possible solutions exist for this problem, Tatu Ylönen at Helsinki University of Technology in Finland came up with the best one: SSH. SSH is essentially a point-to-point encrypted telnet protocol. If your server supports SSH, and odds are excellent that it does, you should unquestionably use it. There are no downsides that I’ve found, and the additional security is a definite boon.

On the PC side, the SSH client of choice is unquestionably PuTTY, which includes SSH support and can be found at http://www.putty.org. Better yet, it’s free. You can’t go wrong with that price.

For Macintosh users, an SSH client is included with Mac OS X, so you need merely open up the Terminal (it’s in Applications -> Utilities) and type ssh to get started.

If you’re on a Unix or Linux system, you already have an SSH client. Just type ssh and
