
foobirds.org MASQUERADE_AS(`foobirds.org`) is used with the default settings. But if FEATURE(`limited_masquerade`) is also used, the mail goes out as mail from bridal-gowns.com, unless you explicitly add bridal-gowns.com to class M.

Use MASQUERADE_DOMAIN to add individual values to class M. For example, to add hawk.foobirds.org to class M, add the following m4 macro to the configuration file:

```
MASQUERADE_DOMAIN(`hawk.foobirds.org`)
```

The MASQUERADE_DOMAIN macro is most useful when only a few values need to be added to class M and when those values change very infrequently. The MASQUERADE_DOMAIN_FILE macro to load class M from file when you have more than a few names that you wish to masquerade. Assume that you want to load class M from a file named /etc/mail/masquerade-domain-names. You could add the following m4 macro to the configuration file:

```
MASQUERADE_DOMAIN_FILE(`/etc/mail/masquerade-domain-names`)
```

As the macro MASQUERADE_DOMAIN IMPLIES, the values stored in class M do not have hostnames; they can be full domain names. By default, the hostname port of the input address must exactly match a value in class w or class M to be rewritten to the masquerade value. Thus, if class M contains terms.foobirds.org, the input address kirstan@terms.foobirds.org is rewritten to the address kirstan@sooty.terms.foobirds.org is not rewritten. This means that in a domain are not masqueraded if the name of the domain is found in class w or class M. Use FEATURE(`masquerade_entire_domain`) to change this default behavior so that every component of a domain is defined in class w or class M is masqueraded. If masquerade_entire_domain is specified and class M contains terms.foobirds.org, the input address kirstan@terms.foobirds.org is rewritten and so is the address kirstan@sooty.terms.foobirds.org. Listing 9.4 illustrates the effect that these options have on masquerading.

Listing 9.4 Testing Masquerade Options

```
[root]# diff ../domain/old-foobirds.m4 ../foobirds.m4
8a19
> MASQUERADE_AS(`foobirds.org`)`dn
> MASQUERADE_DOMAIN(`foobirds.org`)`dn
> FEATURE(`limited_masquerade`)`dn
> FEATURE(`masquerade_entire_domain`)`dn
[root]# m4 ../cf.m4 redhat811.ll > masquerade.cf
[root]# sendmail -bt -masquerade.cf
```

![](img/b8082498451dba2bf0cf2907c85c4c83_273_0.png)

# Chapter 9 Special m4 Configurations

ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>

```
>=$w
wren.foobirds.org
[172.16.12.3]
patient-rights.org
autofusiness.com
wren
localhost
iminary.com
> /tryflags HS
> /tsmtp fred@imaginary.com
canonify input: fred @ imaginary . com
... Many lines deleted returns: fred @ imaginary . com
final
Rcode = 75, addr = fred@imaginary.com
> $-M
foobirds.org
> /tsmt sara@hawk.foobirds.org
The header sender sara@hawk.foobirds.org for mailer esmtp
canonify input: sara @ hawk . foobirds . org
... Many lines deleted
final returns: sara @ foobirds . org
Rcode = 0, addr = sara@foobirds.org
> -D
```

Listing 9.4 opens with a diff command shows the four m4 macros added to the foobirds.m4 configuration file. The four macros tell Sendmail to:

- Masquerade the host portion of outgoing addresses as foobirds.org
- Store the value foobirds.org in class M
- Only masquerade addresses if the host portion of the address matches the value in class M
- Treat the value in class M as a domain and masquerade any hostname within that domain

The new test.mc file is processed through m4 to create a Sendmail configuration .cf. The sendmail command is run with the -bt option to enter test mode and with the -C option to load the new configuration. In test mode, the contents of class w is displayed, the tryflags are set to HS to request sender address, and the address fred@imaginary.com is processed for the esmtp tiler. (imaginary.com is one of the virtual domains we created in Chapter 6.)

The address is not masqueraded, even though the host portion of the address is contained in class w and masquerading is enabled. This test shows the effect of the limited masquerade feature, which limits masquerading to values stored in class M and ignores values defined in class w. Next, the contents of class M with foobirds.org, which is the value stored in class M with the MASQUERADE_DOMAIN macro. The address sara@hawk.foobirds.org is processed as header sender for esmtp mail. This time the address is masqueraded as sara@foobirds.org. We know that this is not because hawk.foobirds.org is not in class—it's not, and even if it was, class w is not being masqueraded. Additionally, hawk.foobirds.org is not in class M. The only value in class M is foobirds.org. The reason that hawk.foobirds.org is masqueraded is that this is part of foobirds.org domain and the masquerade_entire_domain option has been selected. Masquerading all of the hosts within a domain is very useful, particularly when a single server handles the entire domain.

Sometimes, of course, you want to masquerade some of the hosts in a domain, but not every host. In those cases, it is simplest to use the masquerade_entire_domain feature to include the bulk of the domain's systems and use the MASQUERADE_EXCEPTION macro to exclude the individual hosts you don't want to masquerade. The configuration shown in Listing 9.4 masquerades every host in foobirds.org domain. Assume you wanted to masquerade every host except foobirds.org. You could add the following macro to the configuration shown in Listing 9.4 to accomplish this:

```
MASQUERADE_EXCEPTION('*.foobirds.org')
```

Another exception to masquerading is created for special usernames. Class E contains the list of usernames over masquerading. When the user portion of the input address contains a value found in class E, the host portion of the address is not masqueraded—even if the host portion of the address is listed in class w or class M. The usernames in class E are those that are not unique among the systems being masqueraded. For example, every system has a root user and many postmaster. If mail root@foobirds.org is masqueraded as mail from root@foobirds.org and mail from root@ibis.org is also masqueraded as root@foobirds.org, there is no way for the mail server to determine the correct host when the recipient replies to root@foobirds.org. Placing the username in class E adds values to class E. The original old-foobirds.m4 file already had an EXPOSED_USER macro for root because it was derived from the redhat.mc file, which had this macro. The following two lines add both root and postmaster to class E:

```
EXPOSED_USER(root)
EXPOSED_USER(postmaster)
```

![](img/b8082498451dba2bf0cf2907c85c4c83_275_0.png)

# Chapter 9 Special m4 Configurations

The EXPOSED_USER macro is not the only way to duplicate usernames. The macro works for names like root, which have a special meaning and are on all Linux systems, but it may not be the solution you want when the duplicated names are the logon names of real users. Instead of skipping masquerading for every user who has a duplicated username, you may want to replace the username portion of the outbound address. Rewriting usernames is our next topic.

# Masquerading Usernames

Transforming the user portion of an outbound address requires a database. Unlike hosts that can be masqueraded as a single value, each username requires a unique value. The user database and the genericstable, both described in Chapter 6, can be used to rewrite usernames. The user database, usually named /etc/mail/user.db, handles both inbound and outbound addresses—duplicating functions performed by the aliases database and the genericstable. The user database does not work well with masquerading. For reason, it is not covered. See Chapter 6 for details of the user database. The genericstable, on the other hand, is an essential corollary to masquerading. The genericstable handles the user portion of the outbound address while masquerading handles the host port.

The input address to genericstable for processing must either have no port or a host port that matches a value in class G. Use the GENERIC_DOMAIN macro to add individual values in class G for masquerading. To configure the genericstable to be compatible with masquerading, class G should contain the same values as class M.

If you want to add more than a few values to class G, load class G from a file using the GENERIC_DOMAIN_FILE macro. Use the same file for class G that you use for M if you want to make the following two macros in your configuration if you wanted to masquerade usernames on the exact same systems that you masquerade hostnames:

```
MASQUERADE_DOMAIN_FILE(`/etc/mail/masquerade-domain-names`)
GENERIC_DOMAIN_FILE(`/etc/mail/masquerade-domain-names`)
```

Also like values in class M, values require an exact match. Use the generics_entire_domain feature to override this default behavior. The generics_entire domain feature acts exactly like the masquerade_entire_domain feature described in the previous section. When generics_entire_domain is used, the values in class G are treated as domain names and any host within those domains is considered a match for class G. Listing 9.5 shows the effect of the genericstable on output addresses.
