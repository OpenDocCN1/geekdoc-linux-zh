Option | Description
--- | ---
blackhole | Specifies a list of hosts that should not be allowed to query the name server. The default value is none.
directory | Specifies the working directory of the server. By default, the working directory is set to `/var/named`, the directory from which the server was started. The specified directory should have an absolute path.
forwarders | Specifies a list of valid IP addresses of name servers that named will query if the local cache fails to resolve. Requests are forwarded to these name servers for resolution.
forward | Specifies the behavior of the `forwarders` directives, `first` or `only`. The first option specifies that named initially queries the name servers listed in the `forwarders` directive before resolving the hostname itself. The `only` option specifies that named will resolve only if the name servers specified in the `forwarders` directive fail to resolve queries.
listen-on | Specifies the interfaces and ports that the server will listen and answer queries to. The `listen-on` option accepts an optional port and a collection of IP addresses. An option statement can have multiple `listen-on` statements.
recursion | Specifies whether `recursion` should be disabled or not. If the name server is disabled, it will not send queries on behalf of the name servers or resolvers, and will not cache data as well.
notify | Specifies whether the `named` daemon should notify the slave servers when a zone is updated. The `notify` option can be set to `yes`, `no`, or `explicit`. By default, the `notify` option is set to `yes`, so the slave server will be notified about the changes. If the `notify` option is set to `explicit`, then the slave servers mentioned in the `also-notify` list of the zone statement will be notified.

# Syntax

The syntax of the options statement is:

```
```
  options {
      option;
      option;
  };
```
```