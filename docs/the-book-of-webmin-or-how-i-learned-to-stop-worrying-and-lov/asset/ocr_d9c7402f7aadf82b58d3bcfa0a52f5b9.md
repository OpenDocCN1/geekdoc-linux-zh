case. There is an additional field required, called Priority, which is simply a number that dictates the preference of this mail server relative to others that may be configured, where lower numbers have higher priority with zero being the lowest. Traditionally, a priority of 10 is used for the primary mail server, and other servers will be given priorities higher in steps of ten. So a backup mail server could have a priority of 20. There is no enforcement of this de facto standard, so you could use priorities of 0 and 43 to represent your primary and backup mail servers, but following traditions is probably more polite to any administrator who might have to follow in your footsteps. Click Create to add the mail server record.

# Applying Changes and Testing the Results

Now we have the bare minimum configuration required to make good use of our name server in the real world, so let's reload our BIND configuration and make sure it is working. First, return to the BIND module front page by clicking the Module Index link in the upper right corner of the page. Then click the Apply Changes button at the bottom of the page to signal BIND to reload its configuration files.

To test our work, we can use the host program. First, we'll test to be sure our domain is resolvable from our name server:

```
[joe@delilah joe]$ host swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com has address 192.168.1.1
```

The host command is discussed further in the troubleshooting section of this chapter, but I will point out arguments I've used. Obviously, the first argument to the command is swelltech.com, which is the domain I'd like to look up. While the second argument is 192.168.1.1, which is the name server I'd like to query for the information. This allows us to easily set up a name server in isolation, without relying on it for real-world name service, so that it can be thoroughly tested and confirmed working. Because the above result is exactly what we expected to see, we can move on to testing the MX and NS records, to be sure they also match our expectations:

```
[joe@delilah joe]$ host -t mx swelltech.com 192.168.1.1
Using domain server:
Name: 192.168.1.1
Address: 192.168.1.1#53
Aliases:

swelltech.com mail is handled by 10 mail.swelltech.com.
```