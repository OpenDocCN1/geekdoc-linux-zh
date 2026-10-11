Enter KDC database master key:
Re-enter KDC database master key to verify:

The command in Listing 13.5 prompts you for the Kerberos master key (you should pick a word that is hard to guess, containing both mixed-case characters and numbers) and creates the following files:

+   * `/var/kerberos/krb5kdc/principal`: This is a Kerberos database file.
+   * `/var/kerberos/krb5kdc/principal.kadm5`: This is the Kerberos administrative database.
+   * `/var/kerberos/krb5kdc/principal.kadm5.lock`: This is the lock file associated with the Kerberos administrative database.
+   * `/var/kerberos/krb5kdc/.K5.HONTANON.COM`: This file is called the *stash*, a local copy of the master key that is used to authenticate the KDC to itself before starting the kadm5d and krb5kdc daemons.

> **WARNING** The stash file should be heavily guarded and should by owned and readable only by the root user. The stash file should not be part of your regular backup scheme because this would force you to protect the privacy of your backup media (which would contain the master key of the KDC).

# ### The kadm5.acl File

Take a look at the kadm5.acl file, typically located in /var/kerberos/krb5kdc. This file defines which principals are allowed to use the kdb5_util to modify which parts of the database. You need to have at least one Kerberos principal in this file, along with a list of permissions for that principal. The format of entries in the kadm5.acl file is as follows:

```
principal permissions [target-principal]
```

These fields have the following meanings:

+   * *principal* is an entry that uses the syntax

```
primary/instance@REALM
```

where *primary* is a username (e.g., *ramon* in the following example), *instance* defines a specific role (e.g., *admin* in the following example) and *REALM* corresponds to a Kerberos realm (e.g., *HONTANON.COM* in the following example). For example, a complete principal specification would be *ramon/admin@HONTANON.COM*.

+   * The *permissions* field can be made up of one or more of the characters listed in Table 13.1.