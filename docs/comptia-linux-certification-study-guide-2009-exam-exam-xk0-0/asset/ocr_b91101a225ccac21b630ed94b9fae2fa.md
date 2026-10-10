Variables are typically used within scripts, as in this simple backup script from the Linux Documentation Project:⁵

```
#!/bin/bash
SRC=~/home/  
TGT=/var/backup/  
OF=home-$(date +%Y%m%d).tgz  
tar -cZF $TGT$OF $SRC
```

The “=” is used to compare the equivalence of two variables. An example is comparing two values in bc — a command line calculator that, among other things, will return a 1 for a true comparison or a 0 for a false one:

```
bc  
10==10

1

10==1

0
```

# Learn by Example: Optimizing Frequent Tasks

Like any operating system, Linux offers many ways to automate common tasks. I frequently ping my default gateway of 10.10.10.1 but get tired of typing it out all the time, so I’ve added the router’s name and address to the end of my /etc/hosts file, and now Linux will resolve it by name.

One way to do this is to use vi to edit the file. A G takes me straight to the end of the file, and an o adds a line to the bottom; type the address and name, and a quick <Esc>:wq and I’m done. Even quicker, though, is to use echo “10.10.10.1 router” >> /etc/hosts, which automatically appends the information I need at the end of the file. Just have to make sure I use two greater-than signs — just one will overwrite the file completely.

I also use my laptop on a lot of different networks, and don’t know the default gateway ahead of time. I can build that right into the command, though, using an alias and some command-line redirection:

```
alias pdg='ping -c 3 `ip route show 0.0.0.0/0 | cut -d " " -f 3`'
```

The ip route show gives information about the default route; but I only want the actual IP address, so I use cut to grab just the third piece of information in the list (the address). All that is inside the tick marks (` `), so it gets worked out and then fed to ping. I could just type that whole thing out every time, but that’s even worse than