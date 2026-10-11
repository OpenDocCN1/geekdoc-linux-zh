+   1. **Type** `ssh username@IPaddress` or `ssh username@machinefullname` **to open the connection.**
+      
+      For example, type `ssh rich@192.168.1.76` or `ssh rich@computer.example.com`. After you do this step, the following text appears:
+   
+      The authenticity of host '192.168.1.76 (192.168.1.76)' can't be established.
+      
+      RSA key fingerprint is ed:68:0f:e3:78:56:c9:b3:d6:6e:25:86:77:52:a7:66.
+      
+      Are you sure you want to continue connecting (yes/no)?
+      
+   2. **Type yes and press Enter.**
+      
+      You now see these lines:
+      
+      `Warning: Permanently added '192.168.1.76' (RSA) to the list of known hosts.`
+      
+      `rich@192.168.1.76's password:`
+      
+   3. **Enter your login password and press Enter. Now you're in!**
+      
+      Close the connection by logging out of the account (type `logout`)

# ## Connecting to your Linux box from a Macintosh running OS X with SSH

The process from a Macintosh is similar to that under Linux. Go to Applications→Utilities→Terminal.app, which opens a command line window for you. Then type

```
ssh IPaddress
```

to access the same user account on the remote machine (again, you can use a computer’s full name rather than the IP address), or type

```
ssh login@IPaddress
```

if you want to access the account `login` instead of the same account you're using on the Mac.

# ## Software holes

When someone is already in your system — whether or not they're allowed to be there — you have additional security concerns to keep in mind. One of these involves what software you have on the machine. Believe it or not, each piece of software is a potential security hole. If someone can get a program to crash in just