# First Boot and Updates

At startup the Grub menu is displayed, stick with the default entry and wait for your system to initialize. At XFCE first start, you will be asked to choose between two panel setups, select the default config.

![](bbox=[0.06, 0.16, 0.94, 0.46])

Check your time configuration. If incorrect, launch as root a dpkg-reconfigure tzdata and select your country.

**Proxy, part #2 (if needed):** during install, you entered your proxy address for **apt** connection (repositories connection). It is has been written inside the file /etc/apt/apt.conf, and can be modified any time. I use nano as command line text editor, change at will.

```
[root] $ nano /etc/apt/apt.conf
Acquire::http::Proxy "http://user:password@proxy.address:port/";
```

Now add the proxy setting for the entire system:

```
[root] $ nano /etc/environment
http_proxy=http://user:password@proxy.address:port/
https_proxy=http://user:password@proxy.address:port/
ftp_proxy=http://user:password@proxy.address:port/
```

Congratulations, you are now a confirmed Linux user! Now we can update and install some useful tools, then we will modify the default UI. To use the full capacity of your VM you need to install a complementary VirtualBox extension called **Guest Additions**. To do so, some dependencies are required.

Check your sources, remove the CD entries, add the **contrib** and **non-free** repos: