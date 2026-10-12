This is again probably most useful in conjunction with a Host directive. Default is the standard **SSH** port of 22.

User michael

Here's your chance to specify a username other than the one you're logged in to the current machine as. This is essentially the same as using the -l option on the command line.

The value of those last few options as entries in a **config** file might make more sense if you see them in context with a Host example.

```
# my personal ssh_config file
# first some global options
ForwardX11 yes
ForwardAgent yes

# ok, now some servers that I use a lot
# my setup for the host I call "brain"
Host brain
HostName shellserver.some.long.domain.com
User mt

# now for "pinkyn"
Host pinky*
HostName pinky.example.org
# what admin put this one on the wrong port?
Port 23
User Michael
```

# Progress Check

+   1. What is the default port used by SSH?
+   2. How do you specify in the **ssh_config** file which protocol version to use?
+   3. What should you specify in **ssh_config** to allow X clients to forward back across the connection?

+   1. Port 22 is used by default.
+   2. Protocol *number* will specify the protocol version attempted on a connection. Multiple protocols can be separated by commas and will be tried in the order listed.
+   3. ForwardX11 yes.