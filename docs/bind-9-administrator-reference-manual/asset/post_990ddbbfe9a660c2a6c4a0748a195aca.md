
# Chapter 4. Advanced Concepts

Internal DNS server config:

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
acl externals { bastion-ips-go-here; };
options {
  ...
  forward only;
  forwarders { // forward to exter-
    servers {
    bastion-ips-go-here;
    };
    allow-transfer { none; }; // sample allow-
    transfer (no one)
    allow-query { internals; externals; }; // restrict query access
    allow-recursion { internals; }; // restrict recursion
  ...
};
zone "site.example.com" { // sample master zone
  type master;
  file "m/sitel.example.com";
  forwarders { }; // do normal iterative
  tion (do not forward)
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
// resolu-
zone "site2.example.com" {
  type slave;
  file "s/site2.example.com";
  masters { 172.16.72.3; };
  forwarders { };
  allow-query { internals; externals; };
  allow-transfer { internals; };
};
zone "site.internal" {
  type master;
  file "m/sitel.internal";
```
forwarders { };
allow-query { internals; };
allow-transfer { internals; }

```

```
zone "site2.internal" {
type slave;
file "s/site2.internal";
masters { 172.16.72.3; };
forwarders { };
allow-query { internals; }
allow-transfer { internals; }

```
```

External (bastion host) DNS server config:

```
acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```

```
options {
...
allow-transfer { none; }; // sample allow-
transfer (no one)
allow-query { internals; externals; }; // restrict query access
allow-recursion { internals; externals; }; // restrict recursion
};
```

```
zone "sitel.example.com" { // sample slave zone
type master;
file "m/sitel.foo.com";
allow-query { any; };
allow-transfer { internals; externals; }
};
```

```
zone "site2.example.com" {
type slave;
file "s/site2.foo.com";
masters { another_bastion_host_maybe; };
allow-query { any; };
allow-transfer { internals; externals; }
};
```

# Chapter 4. Advanced Concepts

In the resolv.conf (or equivalent) on the bastion host(s):

```
search ...
nameserver 172.16.72.2
nameserver 172.16.72.3
nameserver 172.16.72.4
```

## 4.4. TSIG

This is a short guide to setting Transaction Signatures (TSIG) based transaction security in BIND. It describes changes to the configuration file as well as what changes are required for different features, including the process of creating transaction keys and using transaction signatures with BIND.

BIND primarily supports TSIG for server communication. This includes zone transfer, notify, and recursive query messages. Resolvers on newer versions of BIND 8 have limited support for TSIG.

TSIG might be most useful for dynamic update. A primary server for a dynamic zone should use access control to control updates, but IP-based access control is important. Key-based access control is far superior, see Proposed Standards. The nupdate program supports TSIG via the -k and -y command options.

### 4.4.1. Generate Shared Keys for Each Pair of Hosts

A secret is generated to be shared between host1 and host2. An arbitrary key name is chosen: "host1-host2.". The key name must be the same on both hosts.

#### 4.4.1.1. Automatic Generation

The following command will generate a 128 bit (16 byte) HMAC-MD5 key as described. Longer keys are better, but easier to digest with MD5. Note that the maximum key length is 512 bits; keys longer than what is needed to produce a 128 bit.

```
dnssec-keygen -a hmac-md5 -b 128 -n HOST host1-host2.
```

The key is in the file Khost1-host2.+.157+00000.private. Not directly using this file, but the base-64 encoded string following "Key:" can be extracted from the file and used as a shared secret:

Key: La/E5cG90+0sl1jq0a2da==

The string "La/E5cG90+0sl1jq0a2da==" can be used as the shared secret.

#### 4.4.1.2. Manual Generation

The shared secret is simply a random sequence of bits, encoded in base-64. Most ASCII strings are valid base-64 (assuming the length is a multiple of 4 and only valid characters are used), so the shared secret can be manually generated.

Also, a known string can be run through mmencode or a similar program to generate base-64 encoded data.

### 4.4.2. Copying the Shared Secret to Both Machines

This is beyond the scope of transport. A secure transport mechanism should be used. This could be secure FTP, ssh, telephone, or.

### 4.4.3. Informing the Servers of the Key's Existence

Imagine host1 and host 2 are both servers. The following is added to each server's named.conf file:

```
key host1-host2. {
  algorithm hmac-md5;
  secret "LaESCJG90+0sljqq0a2jdA==";
}
```

The algorithm, hmac-md5, is the only one supported by BIND. The secret is the one generated above. Since this is a secret, it is recommended that either named.conf be non-world readable, or the key directive be added to a non-world readable file that is included by named.conf.

At this point, the key is recognized. This means that if the server receives a message signed by this key, it can verify the signature. If the signature succeeds, the response is signed by the same key.

### 4.4.4. Instructing the Server to Use the Key

Since keys are shared between two hosts, only the server must be told when keys are to be used. The following is added to the named.conf file for host1, if the IP address of host2 is 10.1.2.3:

```
server 10.1.2.3 {
  keys { host1-host2. };
}
```

Multiple keys may be present, but only the first is used. This directive does not contain any secrets, so it may be in a world-readable file.

If host1 sends a message that is a request to that address, the message will be signed with the specified key; host1 will expect any responses to signed messages to be signed with the same key.

A similar statement must be present in host2's configuration file (with host1's address) for host2 to sign the.

### 4.4.5. TSIG Key Access Control

acl internals { 172.16.72.0/24; 192.168.1.0/24; };
 externals { bastion-ips-go-here; };
```
options {
...
allow-transfer { none; }; // sample allow-
transfer (no one)
allow-query { internals; externals; }; // restrict query access
allow-recursion { internals; externals; }; // restrict recursion
};
```

```
zone "sitel.example.com" { // sample slave zone
type master;
file "m/sitel.foo.com";
allow-query { any; };
allow-transfer { internals; externals; }
};
```

```
zone "site2.example.com" {
type slave;
file "s/site2.foo.com";
masters { another_bastion_host_maybe; };
allow-query { any; };
allow-transfer { internals; externals; }
};
```

### 4.4.6. Errors

The processing of TSIG can result in several errors. If a TSIG aware server receives an unknown key, FORMERR will be returned. If a TSIG aware server receives a signature that does not validate, BADSIG will be returned. If a TSIG aware server receives a message with a time outside the allowed range, BADTIME will be returned. In any of these cases, the rcode is set to NOTAUTH.
