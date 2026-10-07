The effect of the MASQUERADE_AS command shown above is the same as setting the sendmail1.cf M variable to foobirds.org. In fact, the only thing that MASQUERADE_AS is a value in M. Listing 9.2 demonstrates this fact.

# Listing 9.2 The Impact of MASQUERADE_AS on sendmail.cf

```
[root] # diff ../domain/old-foobirds.m4 ../domain/foobirds.m4
8a9
> MASQUERADE_AS(`foobirds.org`)' > dn1
[root] # m4 ../m4/cf.m4 redhat811.mc > masquerade.cf
[root] # diff plain.cf masquerade.cf
12c8c128
< DM
```

> DMobirds.org
In Listing 9.2, the first diff command shows that the only difference between the two DOMAIN files is that the new file has a MASQUERADE_AS command that is not found in old-foobirds.m4. The new file is processed through m4 to build Sendmail configurations. The plain.cf configuration file was created in Listing 9.1. Listing 9.2 creates the configuration named masquerade.cf. The second diff compares the contents of these two files. Where the plain.cf file stores no value in M, the masquerade.cf file stores foobirds.org in M. This is the only difference between these configurations and is the only change that the MASQUERADE_AS command makes.

From the testing we did in Chapter 7, we know that storing a value in M causes Sendmail to rewrite the host port of header addresses to the found value in M. There are some limitations. The value in M is used to rewrite the address only if the input address has no host port or the host part from the input address is in class w. Additionally, masquerading is only applied to the header address. The sendmail -bt tests in Listing 9.3 demonstrates these effects.

# Listing 9.3 Testing the Default MASQUERADE_AS Settings

```
[root] # sendmail -bt -masquerade.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enterter <ruleset> <address>
$=$w
wren.foobirds.org
[172.16.12.3]
wren
localhost
>/tryflags HS
```