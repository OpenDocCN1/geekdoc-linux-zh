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