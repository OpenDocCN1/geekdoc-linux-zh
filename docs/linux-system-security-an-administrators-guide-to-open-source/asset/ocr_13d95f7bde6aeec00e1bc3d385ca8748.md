(see *Sample ICMP Rules* on page 454). The rules in `icmperr` will be invoked by both the input and output chains.

# **Example 16-15** Adding Rules to a Custom Chain

```
# $ icchains -A icmperr -p icmp --icmp-type destination-unreachable -j ACCEPT
# $ icchains -A icmperr -p icmp --icmp-type parameter-problem -j ACCEPT
# $ icchains -A icmperr -p icmp --icmp-type source-quench -j ACCEPT
# $ icchains -A icmperr -p icmp --icmp-type time-exceeded -j ACCEPT
```

Now that we have created the custom chain, we need to invoke the chain through one or more of the permanent chains. Here we will add rules to the input and output chains that will invoke our custom chain. These two commands are shown in Example 16-16. Notice that we invoke the `icmperr` chain only if the protocol is ICMP. While this may be obvious, if we had left off -p icmp in the two commands shown in Example 16-16, the rules would still be valid and would inspect every packet against all the rules in `icmperr`. Such a mistake could cause significant performance problems.

# **Example 16-16** Adding Rules to Invoke the Custom Chain

```
[root@topcat]# $ icchains -A input -p icmp -j icmperr
[root@topcat]# $ icchains -A output -p icmp -j icmperr
```

Example 16-17 shows us what our rule base looks like now.

# **Example 16-17** Listing of Rule Base with Custom Chain

```
[root@topcat]# $ icchains -L
Chain input (policy REJECT):
target	prot opt	source	destination	ports
ACCEPT	icmp	-	anywhere	topcat	echo-reply
REJECT	icmp	-	anywhere	any	any

Chain icmperr (policy REJECT):
target	prot opt	source	destination	ports
ACCEPT	icmp	-	anywhere	anywhere	echo-request
ACCEPT	icmp	-	anywhere	anywhere	parameter-problem
ACCEPT	icmp	-	anywhere	anywhere	source-quench
ACCEPT	icmp	-	anywhere	anywhere	time-exceeded

Chain forward (policy REJECT):
target	prot opt	source	destination	ports
ACCEPT	icmp	-	anywhere	anywhere	echo-request
ACCEPT	icmp	-	anywhere	anywhere	echo-reply
ACCEPT	icmp	-	anywhere	anywhere	any

Chain icmperr (2 references):
target	prot opt	source	destination	ports
ACCEPT	icmp	-	anywhere	anywhere	destination-unreachable
ACCEPT	icmp	-	anywhere	anywhere	parameter-problem
ACCEPT	icmp	-	anywhere	anywhere	source-quench
ACCEPT	icmp	-	anywhere	anywhere	time-exceeded

[root@topcat]#
```

If you wish to delete a custom chain, you may do so with the -x flag. The chain must be empty in order to delete it, so you will have to flush it with -F first. Example 16-18 shows how we could delete the custom chain `icmperr`.

# **Example 16-18** Removing a Custom Chain

```
# $ icchains -F icmperr
# $ icchains -X icmperr
```