# Chapter 9 Special m4 Configurations

The EXPOSED_USER macro is not the only way to handle duplicate usernames. The macro works for names like root, which have a special meaning and are found on all Linux systems, but it may not be the solution you want when the duplicated usernames are the names of real users. Instead of skipping masquerading for every user who has a duplicated name, you may want to replace the username portion of the outbound address. Rewriting usernames is our next topic.

# Masquerading Usernames

Transforming the user portion of an outbound address requires a database. Unlike hosts that can be masqueraded as a single value, each username requires a unique value. The user database and the genericstable, both described in Chapter 6, can be used to rewrite usernames. The user database, usually named /etc/mail/userdb.db, handles both inbound and outbound addresses—duplicating functions performed by the aliases database and the genericstable does not work well with masquerading. For that reason, it is not covered. See Chapter 6 for details of the user database. The genericstable, on the other hand, is an excellent corollary to masquerading. The genericstable handles the user portion of the outbound address while masquerading handles the host portion.

The input address passed to the genericstable for processing must either have no host portion or a host portion that matches a value in class G. Use the GENERICIS_DOMAIN macro to add individual values in class G. Class G performs the same function for the genericstable as class M for masquerading. To configure the genericstable to be compatible with masquerading, class G should contain the same values as class M.

If you plan to add more than a few values to class G, load class G from a file using the GENERICIS_DOMAIN_FILE. Use the same file for class G that you use for class M if you want to make masquerading compatible. For example, you might have the two macros in your configuration if you wanted to masquerade usernames on exactly the same systems that you masquerade hostnames:

```
MASQUERADE_DOMAIN_FILE(`/etc/mail/masquerade-domain-names`)
GENERICIS_DOMAIN(`/etc/mail/masquerade-domain-names`)
```

Also like values in class M, values in class G require an exact match. The generics_entire_domain feature to override this default behavior. The generics_entire_domain acts exactly like the masquerade_entire_domain feature described in the previous section. When generics_entire_domain is used, the values in class G are treated as domain names and any host whose these domains is considered a match for class G. List-9.5 shows the effect of the genericstable on output addresses.