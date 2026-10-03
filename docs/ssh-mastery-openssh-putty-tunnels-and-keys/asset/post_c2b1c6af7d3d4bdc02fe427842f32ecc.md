
Windmill Press, 2013) useful.

We’re not going to cover DNS basics. If you’re considering distributing key fingerprints via DNS I’ll take it as given that you know what a zone file is, why an RR is important, and why you update serial numbers.

## SSHFP Records

The SSH Finger Print (SSHFP) record provides a host’s SSH fingerprint. The record looks something like this:

```
wrath IN SSHFP 1 1 07988cadf134050d458dfa5f2c062b5e68106163
```

As with any standard DNS record, the first field gives the hostname, the second indicates this is an Internet record, while the third indicates this is an SSH fingerprint record. SSH-specific details start appearing in field four, which gives the algorithm type. You don’t have to memorize which number maps to which algorithms, but the 1 here means this is an RSA fingerprint. The fifth field is the message digest algorithm used to produce this fingerprint. 1 indicates SHA-1, while a 2 represents SHA-256. Finally, the sixth field is the actual key fingerprint.

You’ll need two SSHFP records for every public key your server offers; one for SHA-1 and one for SHA-256.

## Creating SSHFP Records

Don’t even try to create SSHFP records by hand. The ssh-keygen program can read the key files on the local server and produce records, by using the -r flag. Give the hostname as an argument.

```
$ ssh-keygen -r wrath
wrath IN SSHFP 1 1 07988cadf134050d458dfa5f2c062b5e68106163
wrath IN SSHFP 1 2 b7931f47398ca1ed73e8642bd029fb69dda05913058ffb096f2358c429436013
wrath IN SSHFP 2 1 3f7319432d3ef663866a7b3996e6be113d7ea303
wrath IN SSHFP 2 2 927b540968767879ca926da1aa80db5a0975c8d9c5c99527b3a231e878802e3e
wrath IN SSHFP 3 1 cf61d5ed8a6535790d198af77fa0a409d4e8c7f760
wrath IN SSHFP 3 2 4d2277f46a699d475ff095fa274a007fdf8281ad8bccb3575feb62779e257e8e
wrath IN SSHFP 4 1 59c3ed21e086b923a4e8a49504691c844f5a1590
wrath IN SSHFP 4 2 4e2f1c2ee4850d1bb43ffd43e16d27df99d0a3491582f51423dd7d48944f513
```

Load these records into your DNS server.

You could also copy the server’s public key files to a central host and tell ssh-keygen to use those files with the -f flag.

```
$ ssh-keygen -r wrath -f ssh_host_ed25519_key.pub
```

You must run this command separately for each key file, but if you have a central automation server this approach has a lot to recommend it. Remember, the public keys are displayed to anyone who can connect to the server’s SSH port. Copying the public key files to a secure server is not usually a security risk.

As I write this some free DNS providers, such as Hurricane Electric, support SSHFP records.

## Configuring the Client

The OpenSSH client might use SSHFP records by default, depending on how the operating system distributor compiled it. Use the VerifyHostKeyDNS keyword to explicitly define what ssh should do. If set to yes, the client completely trusts keys provided by SSHFP records. If set to ask, ssh displays the key fingerprint and asks the user what to do.

This handles the host keys. Now let’s talk user authentication keys.

## Distributing authorized_keys

A lone sysadmin with only a handful of servers can pretty easily maintain her own authorized_keys file. Get up to seven or eight servers, and copying authorized_keys everywhere gets pretty tedious. Have a whole team of sysadmins, and want to ban password authentication across your hundreds of servers? You really have to look at ways to automate authorized_keys replication. You can either have your automation system replicate authentication keys on all systems, or have sshd query the network for a user’s authorized_keys at every login attempt. Both have their place.

## Replicating Key Files

Having users maintain their own key files can cause operational problems. Users have an uncanny ability to corrupt their files, especially when they think they know what they’re doing. By having a centralized system to deploy authorized_keys, you get a chance to perform some basic integrity tests before the user gets themselves in trouble. You don’t need a complicated key file parsing and validation system, but being able to say, “Did you realize that your key entries have newlines in the middle of them?” can reduce annoyance for everybody involved. Also, if a user’s workstation gets hacked into, and the intruder bootstraps that into server access, the intruder can add their own key to the user’s authorized_keys and copy it to all the servers in known_hosts. Centralizing key management and removing a user’s ability to upload new key files without passing through the automation system can be desirable.

You really don’t want your automation system mucking around in each user’s home directory. Instead, take advantage of the AuthorizedKeysFile sshd_config keyword. This lets you put a user’s authorized_keys file anywhere you want. Combine this with the %u token to have root own all the user keys.

```
AuthorizedKeysFile /etc/ssh/keys/%u
```

Remember that the %u token represents the username. With this AuthorizedKeysFile setting, the authentication keys for the user mw1 would be in /etc/ssh/keys/mw1, while the keys for the user djm would be in /etc/ssh/keys/djm. Key files outside the user’s home directory look exactly like any other authorized_keys, but they must be owned by root. Even if our hypothetical intruder penetrates an account, they can’t edit the keys without privilege escalation.

Use any features your operating system supports to secure these files. On a UFS filesystem, maybe the immutable flag would suit your environment. Or NFSv4 ACLs. If something annoyed you by refusing to let you change a file, consider it for protecting authorized key files.

## Querying the Network for Keys

If you have centralized authentication system such as LDAP, you can store user authentication keys in that system. OpenSSH can query that information source with the AuthorizedKeysCommand and AuthorizedKeysCommandUser keywords.

```
AuthorizedKeysCommand /usr/scripts/getAuthorizedKeys.pl
AuthorizedKeysCommandUser ldap
```

Any time you look at network-based authentication people’s brains leap into LDAP. LDAP is specifically meant for this sort of directory lookup—it’s pretty much a database optimized for reads. I can’t go into detail here, as LDAP directories vary wildly between vendors. No matter which you use, however, you’ll need to get an SSH key schema loaded into your directory. Talk with your LDAP administrator and see what they can provide. The exact schema needed varies with the directory arrangement, but it usually involves attaching an sshPublicKeys entry to the user’s account. LDAP administrators for large enterprises that are built upon commercial LDAP offerings are often reluctant to extend core directory entries, because that limits their ability to get vendor support. In my experience, solving this problem required more effort than any other part of key distribution.

Once you have the schema loaded, you need a script to fetch authorized_keys from the directory. The type of script varies precisely as much as the types of authentication systems people use. A script that authenticates against Active Directory will be completely different from one that authenticates against a home-brewed OpenLDAP directory. CentOS ships with a script to authenticate against their LDAP server, ssh-ldap-helper(8). People have solved this problem for a variety of directory services, and made their scripts available, so be sure to look for existing solutions before spending the next ten years debugging your own.

The AuthorizedKeysCommandUser keyword defines the account that will run the script in AuthorizedKeysCommand. If you don’t set AuthorizedKeysCommandUser, sshd will not run the script. All attempts to get a user’s authorized_keys will fail. I recommend creating a user with no privileges except running this one script. Isolated unprivileged users are a ridiculously inexpensive security solution that doesn’t get used often enough.

Just because LDAP gets all of the attention, don’t limit yourself by thinking LDAP is a requirement. It’s convenient if you have it, yes, but you can use any
