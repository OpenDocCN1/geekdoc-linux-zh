Once the module is installed, we can use it with **modules load**, and run **info** to display information about the module and its options:

```
[recon-ng][default] > modules load recon/hosts-hosts/resolve

[recon-ng][default][resolve] > info

		Name: Hostname Resolver
		Author: Tim Tames (@lanmaster53)
		Version: 1.0

Description:
	Resolves the IP address for a host. Updates the 'hosts' table with the results.

Options:
	Name		Current Value	Required	Description
	----		-------------	--------	---------
	SOURCE	default		yes		source of input (see 'show info' for details)

Source Options:
	default		SELECT DISTINCT host FROM hosts WHERE host IS NOT NULL AND ip_address IS NULL
	<string>		string representing a single input
	<path>		path to a file containing a list of inputs
	query <sql>	database query returning one column of inputs

Comments:
	* Note: Nameserver must be in IP form.
```

As is clear from the above output, this module will resolve the IP address for a host.

We need to provide the IP address we want to resolve as our source. We have four options we can set for the source: default, string, path, and query. Each option has a description alongside it as shown in Listing 206. For example, in the “google_site_web” recon-ng module, we used a string value.

However, we want to leverage the database this time. If we use the “default” value, recon-ng will look up the host information in its database for any records that have a host name but no IP address.

As shown in Listing 203, we have four hosts without IP addresses. If we select the “default” source, the module will run against all four hosts in our database automatically.

Let’s try this out by leaving our source set to “default” and then **run** the module:

```
[recon-ng][default][resolve] > run
[+] www.megacorpone.com => 38.100.193.76
[+] vpn.megacorpone.com => 38.100.193.77
[+] www2.megacorpone.com => 38.100.193.79
[+] s1em.megacorpone.com => 38.100.193.89
```

Nice. We now have IP addresses for the four domains.