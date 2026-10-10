unprivileged ports. And, as stated earlier, passive mode doesn't have the problems with NAT that port mode does on the client side.

# ## ALLOWING INCOMING ACCESS TO YOUR LOCAL FTP SERVER

Whether to offer FTP services to the world is a difficult decision. Although FTP sites abound on the Internet, FTP server configuration requires great care. Numerous FTP security exploits are possible.

If your goal is to offer general read-only access to some set of files on your machine, you might consider making these files available through a web server. If your goal is to allow file uploads to your machine from the outside, FTP server access should be severely limited on the firewall level, on the xinetd configuration level, on the tcp_wrappers level, and on the FTP configuration level.

In any case, if you decide to offer FTP services, and if you decide to allow incoming file transfers, write access should not be allowed via anonymous FTP. Remote write access to your file systems should be allowed only from specific, authenticated FTP user accounts, from specific remote sites, and to carefully controlled and limited FTP areas reserved in your file system. Hosting the FTP area from a chroot environment would be even better.

# ### INCOMING FTP REQUESTS

The next two rules allow incoming control connections to your FTP server:

```
```
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \\
       --sport $UNPRIVPORTS \\
       -d $IPADDR --dport 21 \\
       -m state --state NEW -j ACCEPT
fi
```
```

```
```
$IPT -A INPUT -i $INTERNET -p tcp \\
     --sport $UNPRIVPORTS \\
     -d $IPADDR --dport 21 -j ACCEPT
```
```

```
```
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \\
     -s $IPADDR --sport 21 \\
     --dport $UNPRIVPORTS -j ACCEPT
```
```

# ## PORT-MODE FTP DATA CHANNEL RESPONSES

The next two rules allow the FTP server to call back the remote client and establish the secondary data channel connection:

```
```
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \\
```
```