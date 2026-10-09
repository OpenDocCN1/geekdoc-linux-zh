The output from this command points us in the direction of the file */etc/resolv.conf* – in fact, it is this file that holds all the DNS server information. You can take a look at this file, using a text editor such as gedit:

```
# gedit /etc/resolv.conf
```

You’ll see that it is simply a text file with the following format:

```
nameserver 192.168.1.1   ## primary
nameserver 192.168.1.2   ## secondary, etc.
```

Let’s take a look at some more configuration files.

# # Configuration Files

We mentioned that there are a large number of configuration files contained in the */etc* directory hierarchy. They’re stored in a tree structure; the diagram below gives you an idea of the common ones you might find:

![](bbox=[0.3, 0.43, 0.68, 0.91])