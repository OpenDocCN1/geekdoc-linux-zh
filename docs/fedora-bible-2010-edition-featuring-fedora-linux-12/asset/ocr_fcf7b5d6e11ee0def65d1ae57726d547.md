improper in some way. In other words, if you don't want to drop a packet for some reason, you can just log its activity and decide later if something needs to be corrected.

The LOG target directs log information to the standard tools used to do logging in Fedora: **dmess** and **rsyslogd**. Here's an example of a rule using a LOG target:

```
-A FORWARD -p tcp -j LOG --log-level info
```

Instead of *info*, you could use any of the following log levels available with *rsyslog*: *emerg*, *alert*, *crit*, *err*, *warning*, *notice*, *info*, or *debug*. Using the *--log-prefix* option as follows, you could also add information to the front of all messages produced from this logging action:

```
-A FORWARD -p tcp -j LOG --log-level info --log-prefix "Forward INFO "
```

# Enhancing your iptables firewall

You can modify or expand on the iptables examples given in this chapter in many ways. iptables is tremendously flexible.

When you actually create your own iptables firewall, you should refer to the iptables man page (type **man iptables**) for detailed descriptions of options, ways of matching, ways of entering addresses, and other details. I also recommend an excellent iptables Tutorial by Oskar Andresson (http://www.frozentux.net/documents/iptables-tutorial/).

Here are a few tips for using iptables features:

+   - **Reduce rules** — Try to improve performance by reducing the number of rules. Using subchains can keep a packet from seeing rules that don't apply to it.
+   - **Deal with fragments** — Use the `-f` option to refer to the second and subsequent packets of a packet that was split into fragments. In general, it is safe to not drop second and third fragments for which you don't have a first packet fragment because they won't be reassembled. If you use NAT, the fragments are assembled before filtering, so you shouldn't have problems with unfiltered fragments being sent through.
+   - **Opposite** — To make a rule its opposite, use an exclamation mark (!).
+   - **All interfaces** — To match all interfaces of a type, use a plus sign (+), as in *eth+*.
+   - **Blocking connections** — Use the *--syn* option to block SYN packets (that is, those packets requesting connections). This option applies only to TCP packets.
+   - **Limiting** — Use the *--limit* option to restrict the rate of matches that result in log messages. This option allows matches to produce messages only a limited number of times per second (the default is three per hour with bursts of five). See http://www.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/5.4/html/Deployment_Guide/s3-iptables-options-match-modules.html for more on limiting.