
## 19.12 Troubleshooting NetBIOS name resolution

The hardest thing with NetBIOS name resolution is understanding what it's supposed to be doing, i.e. knowing what is correct behavior and what isn't. That's what the earlier part of this chapter was about.

Next, remember that name resolution and browsing the network (Chapter 21) are different. Browsing uses its own servers (“browse masters”) that accumulate a list of the network resources, and return this (the “browse list”) to clients that request it, e.g. in Windows Explorer or `net view`. Browsing does call on name resolution to locate the browse masters but otherwise is completely separate.

Finally, remember that name resolution is only one phase of a network operation – resolving a name to an IP number. If connecting to a share on another PC fails, it may be that the name is resolving correctly and the problem lies in the connect-to-share operation. (Just like not being able to retrieve a Web page from a dead server: DNS is resolving successfully, for example, **www.example.com**, but the Web server at that address isn't responding.) So it's important to recognize what name resolution is doing, and to separate out its function from the other components of Windows Networking. As usual, to do this we rely heavily on `tcpdump` (or `ethereal` or Netmon), looking for name resolution traffic on the wire.

> **Warning:** a PC's node type determines how this PC *resolves* names; it does *not* affect how this PC *answers* name queries. (This can be confusing if you're solving a network problem under pressure). In particular, if my node type is H and WINS is running, I will always register names on WINS; but if you send a broadcast name query for my name, I'll see it on the network and reply to you, giving my IP number.

> **Tip:** the best sniffer for this type of work is **ethereal**: it shows NetBIOS traffic clearly and it can collect packets in promiscuous mode, so you don't have to install it on the PC you're investigating (Alice, say) which might be possible. More importantly, you can capture promiscuously and see the whole picture from one place whereas Netmon can only see traffic to and from Alice: if Alice is using broadcasts and there's a WINS proxy on the network, Network Monitor won't show you the traffic between the WINS proxy and the WINS server. `tcpdump`'s display of Windows Networking traffic is horrible and verbose; we only use it to confirm traffic flow but never to examine the content of the traffic.

### Troubleshooting tips for name resolution

As with everything so far, our approach is to understand what ought to be happening, and then trace each step of the network conversation with a sniffer. When something happens that isn't what you expect, you have a pointer to where the problem is. To verify that name resolution is working correctly, especially if you're not familiar with Windows Networking, you have to work slowly and methodically. The first step is to find out exactly what's happening on your network. Let's say your PC is Alice and you want to resolve the name **bobnt**.

1. Collect all the relevant configuration details for your PC. We've included a worksheet for this in Appendix 23, which you can photocopy from the table in Appendix 23, write down the order of name resolution steps that this node type uses.
2. Print listings of Lmhosts and hosts files.
3. Run your chosen sniffer on Alice or at some point where it can see all the relevant traffic.
4. On Alice, you now want to force two name resolutions:
    - A name that doesn’t exist anywhere, to exercise each name resolution method. We use the name badxxx.
    - The name that you’re investigating (bobnt in our example).
    - First run the command:
      ```
      nbtstat -a badxxx
      ```
    - When the resolution is finished (successful or failed), note the last packet shown in your sniffer, and then run:
      ```
      nbtstat -a bobnt
      ```
5. When the resolution is finished, clear the NetBIOS cache and run the command again, and when that resolution is finished, stop your sniffer.
    - Clear cache:
      ```
      nbtstat -R
      ```
    - Run command again:
      ```
      nbtstat -a bobnt
      ```

If the name you’re testing is a real one, remember that it may be in the NetBIOS name cache; if it is, it will be resolved, but you’ll see no packets on the wire.

> (If the application causing your name resolution problem is a “real” TCP/IP program and not a NetBIOS program, use ping instead of net view. True-blue TCP/IP programs use DNS-names instead of NetBIOS names, so the resolution order is different – see Appendix 22.)

Here are some specific points that often cause problems:

1. If you’re using an Lmhosts file:
    - Don’t forget to include #PRE or you won’t see the entry in `nbtstat -c`.
    - Don’t forget to run `nbtstat -R` (not -r) to force the file to be reloaded.
    - Always use uppercase for host and domain names, and keywords like #PRE and #DOM.
2. If you have different netmasks on PCs on the same LAN segment, their sub-net broadcast addresses will be different, so they won’t hear each others’ broadcasts and B-node and similar resolution will fail. See also the Warning regarding broadcast addresses in Chapter 4’s Notes.
3. Remember, there is a difference in resolution order between DNS names and NetBIOS names (see Appendix 22).
4. If you are running any other protocol in addition to TCP/IP (e.g. running NetBEUI or Novell) they may interfere with name resolution and make it much more complicated. Don’t run any protocols that aren’t essential.
5. If you’re using Samba, its nmblookup tool (Module 22.4) gives you much more precise control, and more feedback, than NT’s nbtstat over how the test name query that you issue is resolved.

### Summary

- Windows Networking uses names as its primary reference for machines and resources.
- A NetBIOS name contains not just a machine or domain or username, but also a special suffix that specifies what type of resource this name refers to. There are individual names and two types of group names.
- A machine registers a name when it is prepared to offer a particular type of resource. Registration can be done by broadcasting a “name claim” request on the local network, or by registering the name with a WINS server.
- Windows Networking uses six different methods to resolve names that have been registered:
    1. Broadcasts: this machine broadcasts a “name query” request and the owner of the name replies. Because this uses broadcast packets, it can only work on the local network segment.
    2. WINS: this machine sends a name resolution request to a WINS server. The server replies with the resolution details. This uses only unicast UDP packets so it can work over a WAN or the Internet. You can run multiple WINS servers for resilience and performance; you should configure the servers to replicate their databases to one another.
    3. DNS: you can use the DNS to resolve NetBIOS names. This can give you a unified name resolution system for all your machines, not just Windows PCs.
    4. The *hosts* file: don’t use it.
    5. The Lmhosts file: you can enter static entries, with their 16th-byte suffixes, in a machine’s Lmhosts file. This is useful when you are running a network containing routers but are not using WINS, for testing, and for overcoming particular network problems.
    6. The internal NetBIOS name cache. You can view the contents of the cache, or cause it to be cleared and re-load its static (Lmhosts file) entries with the `nbtstat` command.
- A machine’s NetBIOS node type determines which resolution methods are used and in which order.
- The **nbtstat** command lets you view the names a particular machine has registered.

### What’s next?

The next chapter explains how you logon to a Windows-NT machine or to a Windows-NT “domain.” We’ll see that the logon mechanisms have to make use of the name resolution that we’ve just covered, to locate a logon server to authenticate your logon.

### Notes and further reading

Name resolution is also called *name discovery*. We don’t use that term because we find it confusing: the name is already known and it’s the address that has to be discovered.
