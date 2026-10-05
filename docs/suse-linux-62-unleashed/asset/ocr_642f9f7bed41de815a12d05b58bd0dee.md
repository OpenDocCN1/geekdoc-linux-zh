# Networking and Internet Services
PART II

ps aux ; grep named

The first line lets you see any errors in DNS as the process is relaunching and will display any fatal errors or warnings. Press Control+C to viewing a file with the tail -f command. The second makes sure that name has indeed restarted.

At this point, a trivial caching DNS should be running.

# Testing Your Caching DNS

First, verify that telnet logs in properly. Run the following command on another machine on your local network:

```
# telnet 192.168.42.1
```

If it takes about a second for the name prompt to appear, far so good. If it takes 20 seconds or more, there's a reverse DNS problem.

> The telnet program is the "miner's canary" of reverse DNS. If there's a reverse DNS problem, telnet will hang or be extremely slow. Other programs can hang, with much worse consequences, because of bad reverse DNS. sendmail is one such program.
In the case of sendmail, it's possible the hang will prevent successful boot, requiring a repair expedition with boot and rescue disks. Other programs that are sometimes run can also hang on bad reverse DNS. This is why it's vital to have telnet working before you do or reboot the system.
If for some reason you can't repair reverse before rebooting, temporarily rename /etc/resolv.conf before booting, and then rename it back after.

If everything seems okay, bring in nslookup:

```
$ nslookup 192.168.42.1 192.168.42.1
```

The first argument is the address to correlate with a name, while the second is the address of DNS server to query. In this example, they're the same. (Obviously, you should substitute IP addresses for the DNS server you're testing.) The preceding command should very quickly yield the following output:

```
Server: numark.domain.cxm
Address: 192.168.42.1
```