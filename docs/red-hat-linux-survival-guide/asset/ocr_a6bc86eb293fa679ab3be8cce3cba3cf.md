The standard Apache distribution includes a module called mod_access, which enables access control that is based on the Internet host name of a Web client. The host name can be either a fully qualified domain name (FQDN), such as blackhole.mobidac.com, or an IP address, such as 192.168.1.100. The module provides this access control support using the following Apache directives: Allow, Deny, Order, Allow from env=variable, and Deny from env=variable.

# Allow directive

This directive enables you to define a list of hosts (containing one or more hosts or IP addresses) that are allowed access to a certain directory.

+   - **Syntax:** `Allow from host1 host2 host3 ...`
+   - **Context:** `<Directory>`, `<Location>`, per-directory access control file
+   - **Override:** Limit

When more than one host or IP address is specified, they should be separated with space characters. Table 12-5 shows the possible values for the directive.

Table 12-5 Possible Values for the allow Directive

| Value | Example | Description |
|---|---|---|
| All | Allow from all | This reserved word allows access for all hosts. The example shows how to use this option |
| A fully qualified domain name (FQDN) of a host | Allow from wormhole.mobidac.com | Only the host that has the specified domain name FQDN is allowed access. The allow directive in the example only allows access to wormhole.mobidac.com. Note that this compares whole components; toys.com would not match etoys.com. |