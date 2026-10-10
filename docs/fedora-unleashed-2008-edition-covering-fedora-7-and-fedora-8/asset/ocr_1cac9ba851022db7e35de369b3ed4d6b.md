nameserver daemon) and rndc components (a control utility that permits various interactions with a running instance of named). You also might need to configure the resolver software, as discussed later. Three configuration files are used:

+   ▸ `rndc.key` to specify the key used to authenticate between `rndc` and `named`
+   ▸ `rndc.conf` to configure `rndc`
+   ▸ `named.conf` to configure `named`

When `rndc` communicates with `named`, it uses cryptographic keys to digitally sign commands before sending them over the network to `named`. The configuration file, `/etc/rndc.key`, specifies the key used for the authentication.

The only authentication mechanism currently supported by `named` is the use of a secret key, encrypted with the HMAC-MD5 algorithm and shared between `rndc` and `named`. The easiest way to generate a key is to use the `dnsssec -keygen` utility. In the following example, the utility is asked to generate a 128-bit HMAC-MD5 user key named `rndc`:

```
$ dnsssec -keygen -a hmac-md5 -b 128 -n user rndc
Krndc.+157+14529
$ cat Krndc.+157+14529.private
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: mKKd2FiHMFef1JqXL/24cfw==
```

The utility creates two files with the `.key` and `.private` extensions, respectively. The `key` line in the `.private` file reveals the secret that `rndc` and `named` need to share (`mKKd2FiHMFef1JqXL/24cfw==`). When you have this, you can set up the `rndc.key` configuration file, which is shared by both `rndc.conf` and `named.conf`:

```
key "rndc" { algorithm hmac-md5; secret "mKKd2FiHMFef1JqXL/24cfw==";};
\*\*\*\*\*\*\*\*
```

# `rndc.conf`

`rndc` uses a TCP connection (on port 53) to communicate with `named`. The configuration file, `/etc/rndc.conf` by default, must specify a server to talk to as well as include the corresponding key (which must be recognized by `named`) to use while talking to it:

```
\*\*\*\*\*\*\*\*
# Use the key named "rndc" when talking to the nameserver "localhost."
server localhost {
```

```
key                 "rndc";
};

# Defaults.
options {
```

```
default-server       localhost;
```