This command will send the maximum sized CDP frame with random data link addresses to all hosts within your multicast domain. Nothing else is needed to potentially cause a large outage on your network segments.

# Defending Against CDP Denial of Service

Mitigating your risk against this attack is quite simple: Disable CDP on all of your Cisco routers and switches, or update to the latest version of Cisco IOS. However, if you are still running a version of IOS prior to 12.0, the command to disable this feature is the following:

```
BRIAN(config)# #no cdp run
```

This will disable CDP on your device and protect against this attack. Remember, that CDP is used in some applications, such as CiscoWorks 2000, so there may be a use for the protocol in your environment. If this is the case, weigh the risks versus the rewards of running this protocol and determine what your ultimate goals are.

More information on this vulnerability can be found at the Phenolit de Web site (www.phenenoit.de/stuff/CiscoCDP.txt) and the Cisco Web site (www.cisco.com/warp/public/707/cdp_issue.html).

![](bbox=[0.109, 0.568, 0.839, 0.653])

# Applying Defense in Depth

As you have learned, many Layer 2 attacks already have easy to use, GUIbased tools freely available on the Internet. To make matters worse, many of these attacks can provide a treasure trove of information for a would-attacker. More importantly, these attacks expose all the areas of your network infrastructure, which makes the "defense in depth"con extremely vital.

As these attacks have shown, the correct exploit might allow an unauthorized user to pass passwords or sniff sensitive traffic, which might lead to further compromises on your network. Securing your network hardware will only help until the Layer 2 exploit becomes available, and a GUI-based tool is written for the novice user to play with. Defense in depth tells us that we must not only secure one