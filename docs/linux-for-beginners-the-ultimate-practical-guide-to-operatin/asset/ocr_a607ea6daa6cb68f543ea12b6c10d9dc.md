B as Server

```
$nc -l 6870 > example.txt
```

Client $nc 292.232.2.1 6870 < example.avi

4) Stream a Video in the server There are many other ways to do this but if using command line this can be an easy way.

Server

```
$cat tutorial.avi | nc -l 2343
```

Looking at the following examples you might have understood how useful Netcat is. There are several tens of experiments that you can do with Netcat in such a way that can help you increase your hacking skills. In this chapter, we have dealt in detail about the hacking tools like Nmap, Nessus and Netcat along with explaining potential examples that can give you good clarity over things that happen in the background.