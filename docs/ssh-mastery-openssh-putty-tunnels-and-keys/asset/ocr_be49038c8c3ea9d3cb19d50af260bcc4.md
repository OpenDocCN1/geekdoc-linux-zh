UFS filesystem, maybe the immutable flag would suit your environment. Or NFSv4 ACLs. If something annoyed you by refusing to let you change a file, consider it for protecting authorized key files.

# Querying the Network for Keys

If you have centralized authentication system such as LDAP, you can store user authentication keys in that system. OpenSSH can query that information source with the AuthorizedKeysCommand and AuthorizedKeysCommandUser keywords.

```
AuthorizedKeysCommand /usr/scripts/getAuthorizedKeys.pl
AuthorizedKeysCommandUser ldap
```

Any time you look at network-based authentication people’s brains leap into LDAP. LDAP is specifically meant for this sort of directory lookup—it’s pretty much a database optimized for reads. I can’t go into detail here, as LDAP directories vary wildly between vendors. No matter which you use, however, you’ll need to get an SSH key schema loaded into your directory. Talk with your LDAP administrator and see what they can provide. The exact schema needed varies with the directory arrangement, but it usually involves attaching an sshPublicKeys entry to the user’s account. LDAP administrators for large enterprises that are built upon commercial LDAP offerings are often reluctant to extend core directory entries, because that limits their ability to get vendor support. In my experience, solving this problem required more effort than any other part of key distribution.

Once you have the schema loaded, you need a script to fetch authorized_keys from the directory. The type of script varies precisely as much as the types of authentication systems people use. A script that authenticates against Active Directory will be completely different from one that authenticates against a home-brewed OpenLDAP directory. CentOS ships with a script to authenticate against their LDAP server, ssh-ldap-helper(8). People have solved this problem for a variety of directory services, and made their scripts available, so be sure to look for existing solutions before spending the next ten years debugging your own.

The AuthorizedKeysCommandUser keyword defines the account that will run the script in AuthorizedKeysCommand. If you don’t set AuthorizedKeysCommandUser, sshd will not run the script. All attempts to get a user’s authorized_keys will fail. I recommend creating a user with no privileges except running this one script. Isolated unprivileged users are a ridiculously inexpensive security solution that doesn’t get used often enough.

Just because LDAP gets all of the attention, don’t limit yourself by thinking LDAP is a requirement. It’s convenient if you have it, yes, but you can use any