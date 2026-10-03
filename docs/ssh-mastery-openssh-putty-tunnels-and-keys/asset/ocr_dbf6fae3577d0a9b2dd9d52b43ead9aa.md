operating system distributor compiled it. Use the VerifyHostKeyDNS keyword to explicitly define what ssh should do. If set to yes, the client completely trusts keys provided by SSHFP records. If set to ask, ssh displays the key fingerprint and asks the user what to do.

This handles the host keys. Now let’s talk user authentication keys.

# Distributing authorized_keys

A lone sysadmin with only a handful of servers can pretty easily maintain her own authorized_keys file. Get up to seven or eight servers, and copying authorized_keys everywhere gets pretty tedious. Have a whole team of sysadmins, and want to ban password authentication across your hundreds of servers? You really have to look at ways to automate authorized_keys replication. You can either have your automation system replicate authentication keys on all systems, or have sshd query the network for a user’s authorized_keys at every login attempt. Both have their place.

# Replicating Key Files

Having users maintain their own key files can cause operational problems. Users have an uncanny ability to corrupt their files, especially when they think they know what they’re doing. By having a centralized system to deploy authorized_keys, you get a chance to perform some basic integrity tests before the user gets themselves in trouble. You don’t need a complicated key file parsing and validation system, but being able to say, “Did you realize that your key entries have newlines in the middle of them?” can reduce annoyance for everybody involved. Also, if a user’s workstation gets hacked into, and the intruder bootstraps that into server access, the intruder can add their own key to the user’s authorized_keys and copy it to all the servers in known_hosts. Centralizing key management and removing a user’s ability to upload new key files without passing through the automation system can be desirable.

You really don’t want your automation system mucking around in each user’s home directory. Instead, take advantage of the AuthorizedKeysFile sshd_config keyword. This lets you put a user’s authorized_keys file anywhere you want. Combine this with the %u token to have root own all the user keys.

```
AuthorizedKeysFile /etc/ssh/keys/%u
```

Remember that the %u token represents the username. With this AuthorizedKeysFile setting, the authentication keys for the user mw1 would be in /etc/ssh/mw1, while the keys for the user djm would be in /etc/ssh/djm. Key files outside the user’s home directory look exactly like any other authorized_keys, but they must be owned by root. Even if our hypothetical intruder penetrates an account, they can’t edit the keys without privilege escalation.

Use any features your operating system supports to secure these files. On a