```
[root] $ nano /etc/apt/sources.list
deb http://ftp.fr.debian.org/debian/ jessie main contrib non-free
deb http://security.debian.org/ jessie/updates main contrib non-free
```

Update your system:

```
[root] $ apt-get update && apt-get dist-upgrade
```

Install the Guest Additions requirements

```
[root] $ apt-get install build-essential module-assistant
[root] $ m-a prepare
```

Insert the Guest Additions CD image (Host + D), go to the root of the mounted drive and execute the program:

```
[root] $ sh ./VBoxLinuxAdditions.run
```

# Customizing your System

... to get something that looks a little more modern.

![](bbox=[0.062, 0.49, 0.596, 0.71])

# Terminal

The terminal is one of the most useful tools on a Linux system. Spend some time making it pleasant to look at: enable your prompt color ink .bashrc, add your aliases, and enable colors and auto completion in root bash.

```
$ nano ~/.bashrc
```

uncomment the “force_colored_prompt=yes” line

```
[root] $ nano .bashrc
```