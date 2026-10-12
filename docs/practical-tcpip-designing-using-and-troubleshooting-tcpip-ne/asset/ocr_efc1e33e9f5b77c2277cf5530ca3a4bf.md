# # 8.15 Lab – configuring your PC to use DNS (3) – the “searchlist”

This option is relatively rarely used (partly because lots of people don’t know what it’s for) but it is useful in a couple of circumstances, where:

+   1.  the domain name of this host contains more than two components, like example.co.uk or ops.example.com (as opposed to a name with just two components, like example.com)
+   2.  your machine communicates regularly with machines whose domain-name setting isn’t the same as yours, and which isn’t a parent of yours. For example, if my domain-name setting is ops.example.com, the normal searching derived from the domain name will let me reach my parent example.com machines, but it won’t let me get automatically to hr.example.com or partnerco.com machines.

We’ll continue with the scenario we used in Module 8.13. Alice is a PC on our LAN and her FQDN is alice.oz.ops.example.com.

Instead of relying on the automatic searchlist derived from Alice’s domain-name setting, she can configure an explicit searchlist herself. This completely over-rides the derived list and is used instead of it – i.e. the domain-name and searchlist settings are mutually exclusive. Now when attempting to resolve a name, the resolver appends each searchlist entry in turn, until it succeeds, or else fails because there are no entries left. The resolver tries the searchlist entries exactly as they are; it doesn’t remove any components as happened with the domain-name setting.

Based on the example.com network, and Alice’s position in it (as far as naming is concerned – her location on a physical subnet is irrelevant), she might configure her searchlist to be:

+   oz.ops.example.com
+   hr.example.com
+   example.com
+   partnerco.com
+   ops.example.com
+   fin.example.com

Note that we have to include example.com and ops.example.com explicitly: no variants are created automatically when you’re using the explicit searchlist.

The order of entries is significant but not crucial – it’s a question of efficiency. Earliest entries are tried first, so if Alice refers to machines at the partner company partnerco.com more often than she deals with her own operations or finance departments, the order shown makes sense. If the order isn’t optimal, all that happens is that more failed lookup requests are made than is strictly necessary.

This type of configuration is obviously useful for sites that use subdomains.

If your domain name has more than two components (e.g. example.co.uk), as discussed in the previous module it’s advisable to set the searchlist. This prevents the resolver appending the final two components (.co.uk in this example) to simple names. For a small site, we might set the searchlist to the single entry:

+   example.co.uk

Because the domain-name and searchlist settings are mutually exclusive, this prevents the resolver appending anything other than example.co.uk in full to simple names.