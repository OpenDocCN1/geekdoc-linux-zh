The following example shows only the configuration entries needed to implement an internal view. In the **mygolf.com** zone, queries and transfers are allowed only among internal hosts. The global **allow-recursion** option allows recursion among internals.

```
Internal DNS server
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1};

options {
		forward only;
		forwarders {10.0.0.1}; // forward to external servers
		allow-transfer { none; };
		// allow-transfer to no one by default
		allow-query { internals; externals; };// restrict query access
		allow-recursion { internals; };
		// restrict recursion to internals
	};

zone "mygolf.com" {
	type master;
	file "mygolf";
	forwarders { };
	allow-query { internals; };
	allow-transfer { internals; }
	};
```

In the configuration for the external DNS server, the same ACLs are set up for internals and externals. In the **options** statement, recursion is now allowed for both externals and internals. In the **mygolf.com** zone, queries are allowed from anywhere, and recursion is allowed for externals and internals. Transfers are not allowed at all.

```
External DNS server
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1};

options {
		allow-transfer { none; }; // allow-transfer to no one
		allow-query { internals; externals; };// restrict query access
		allow-recursion { internals; externals };
		// restrict recursion
	};

zone "greatgolf.com" {
	type master;
	file "greatgolf";
	allow-query { any; };
	allow-transfer { internals; externals; };
};
```