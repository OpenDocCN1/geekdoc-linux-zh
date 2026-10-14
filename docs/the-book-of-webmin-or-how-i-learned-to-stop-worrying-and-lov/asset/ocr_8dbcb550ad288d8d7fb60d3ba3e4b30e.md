# NTLM authentication options

Like Digest authentication, NTLM authentication provides an encrypted connection to a network server. Beware that it is not an HTTP authentication scheme, however. It is a connection authentication scheme that cannot be proxied (though a proxy can use it to authenticate its own clients). NTLM is also less secure than Digest authentication and has a history of vulnerabilities. That said, it is quite popular, because Windows supports a sort of network "single sign-on", in which users only need to log on once to the local network, and they can be automatically authenticated to the proxy server using the same credentials.

# NTLM authentication program

As in Basic and Digest authentication above, this will contain a path to the authentication program and any command-line arguments. Often the arguments will specify the domain or workgroup and the server to authenticate against. This option correlates to the auth_param ntlm program directive and is disabled by default.

# Number of times an NTLM challenge can be re-used

This option configures the number of times that a particular NTLM challenge can be reused. Increasing this number may reduce latency and load on the server slightly, but can also increase the risk of replay attacks (where a challenge response is recorded and played back to imitate the connection of a legitimate user). This option correlates to the auth_param ntlm max_challenge_reuses directive and defaults to 0.

# Lifetime of NTLM challenges

This option corresponds to the auth_param ntlm max_challenge_lifetime directive and defaults to 2 minutes. It is used to specify the length of time that a challenge can be reused. If a challenge is newer than this value and the challenge has been reused fewer than the previous value, a challenge will be reused.

# Access Control

The access control functionality of Squid is perhaps its most complex set of features, but also among its most powerful. In fact, many use Squid primarily for these features. Because of its complexity, you will learn about it in steps, examining the process of creating and implementing an access control list. Access control lists in Squid has two meanings within the configuration file and within the Webmin interface. First, it signifies the whole concept of access control lists and all of the logic that can be applied to those lists. Second, it applies to the lists themselves, which are simply lists of some type of data to be matched against when some type of access rule is in place. For example, forcing a particular site or set of sites to not be cached requires a list of sites to not cache and then a separate rule to define what to do with that list (in this case, don't cache them). There is also a third type of option for configuring ICP access control. These three types of definition are separated in the Webmin panel into three sections. The first is labeled Access control lists, which lists existing ACLs and provides a