```
~~~
~]# firewall-cmd --direct --remove-rule ipv4 filter IN_public_allow \
    -m tcp -p tcp --port 666 -j ACCEPT
~~~
```

Add the `--permanent` option to make the setting persistent.

# ### 5.14.3. Listing Rules using the Direct Interface

To list the rules in the “IN_public_allow” chain, enter the following command as **root**:

```
~~~
~]# firewall-cmd --direct --get-rules ipv4 filter IN_public_allow
~~~
```

Note that this command (the `--get-rules` option) only lists rules previously added using the `--add-rule` option. It does not list existing `iptables` rules added by other means.

# ## 5.15. CONFIGURING COMPLEX FIREWALL RULES WITH THE "RICH LANGUAGE" SYNTAX

With the “rich language” syntax, complex firewall rules can be created in a way that is easier to understand than the direct-interface method. In addition, the settings can be made permanent. The language uses keywords with values and is an abstract representation of `iptables` rules. Zones can be configured using this language; the current configuration method will still be supported.

# ### 5.15.1. Formatting of the Rich Language Commands

All the commands in this section need to be run as **root**. The format of the command to add a rule is as follows:

```
~~~
firewall-cmd [--zone=zone] --add-rich-rule='rule' [--timeout=timeval]
~~~
```

This will add a rich language rule *rule* for zone *zone*. This option can be specified multiple times. If the zone is omitted, the default zone is used. If a timeout is supplied, the rule or rules only stay active for the amount of time specified and will be removed automatically afterwards. The time value can be followed by s (seconds), m (minutes), or h (hours) to specify the unit of time. The default is seconds.

To remove a rule:

```
~~~
firewall-cmd [--zone=zone] --remove-rich-rule='rule'
~~~
```

This will remove a rich language rule *rule* for zone *zone*. This option can be specified multiple times. If the zone is omitted, the default zone is used.

To check if a rule is present:

```
~~~
firewall-cmd [--zone=zone] --query-rich-rule='rule'
~~~
```

This will return whether a rich language rule *rule* has been added for the zone *zone*. The command prints **yes** with exit status **0** if enabled. It prints **no** with exit status **1** otherwise. If the zone is omitted, the default zone is used.

For information about the rich language representation used in the zone configuration files, see the firewalld.zone(5) man page.