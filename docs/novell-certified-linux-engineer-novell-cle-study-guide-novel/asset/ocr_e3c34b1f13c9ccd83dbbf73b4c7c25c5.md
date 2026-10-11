When you do this, the install script reads the data it needs from the file instead of displaying prompts on the screen for you to respond to. The user input portion of the express installation response file is shown in Figure 5.14.

Notice in Figure 5.14 that you simply enter the information you would have been prompted for onscreen in the appropriate fields. Using a response file isn't of much benefit if you're only installing one or two NNLS servers. If you're installing many servers, however, it can be a real timesaver.

```
```
# >>> Required General Directives and Parameters <<<
# Do not modify the following.
CONFIG_INSTALL_LICENSE_AGREEMENT=yes
CONFIG_INSTALL_EXPRESS=yes

# >>> eDirectory <<<

CONFIG_EDir_NFK_FILE=<>
CONFIG_EDir_TREE_NAME=<>
CONFIG_EDir_ADMIN_CONTEXT=<>
CONFIG_EDir_ADMIN_PASSWORD=<>

# >>> NetMail <<<

CONFIG_NETMAIL_DOMAIN=<>
```
```

![](bbox=[0.78, 0.26, 0.92, 0.36])

The express installation response file can be downloaded from http://www.novell.com/documentation/lg/nnls/answers/express.txt.

> **WARNING** I strongly recommend that you use Kwrite, vi, or another Linux text editor to edit this file. Some Windows text editors mess up the CRLF characters in Linux text files. If this happens, the file won't work with the NNLS install script.

Once you've edited the file, create a directory named `/etc/opt/novell` on your server and save the response file there as `nterprise_linux_services_install.conf`. Then, run the install script with the `-s` option (for example, `./install.sh -s`).

If you need more flexibility in your installation than the express option has to offer, you should use the custom installation option.

# Custom NNLS Installation

The custom installation option takes a lot longer to complete and increases the risk of administrator error, but it also provides you with a high degree of flexibility. With a custom installation, you can do the following: