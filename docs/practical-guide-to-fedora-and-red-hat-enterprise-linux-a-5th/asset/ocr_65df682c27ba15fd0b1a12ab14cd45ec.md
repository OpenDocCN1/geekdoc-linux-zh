Because SpamAssassin considered the preceding email to be spam, it modified the Subject line by adding [SPAM] at the beginning of the line.

**Configuration**  Edit `/etc/mail/spamassassin/local.cf` to configure SpamAssassin globally. Users can override the global options and add their own options in `~/.spamassassin/user_prefs`. You can put the options discussed in this section in either of these files. Use `perldoc` (page 977) to display the configuration document that lists all the options:

```
`$ perldoc Mail::SpamAssassin::Conf`
```

As shown in the preceding example, SpamAssassin rewrites the Subject line of email that it rates as spam. The **rewrite_subject** keyword in the configuration files controls this behavior. A 1 following this keyword indicates that SpamAssassin will rewrite Subject lines. Change the 1 to a 0 (zero) to turn off this behavior:

```
`rewrite_subject 0`
```

The **required_hits** keyword specifies the minimum number of hits a piece of email must receive before SpamAssassin considers it to be spam. The default is 5.0. With a higher number, SpamAssassin marks fewer pieces of email as spam.

```
`required_hits 5.00`
```

Sometimes mail from addresses that should be marked as spam is not, or mail from addresses that should not be marked as spam is. Use the **whitelist_from** keyword to specify addresses that should never be marked as spam and **blacklist_from** to specify addresses that should always be marked as spam:

```
`whitelist_from  sams@corp.com`  `blacklist_from  spammer.net`
```

You can specify multiple addresses, separated by **SPACES**, on the **whitelist_from** and **blacklist_from** lines. Each address can include wildcards. You can also use multiple lines.

**SELinux**  When SELinux is set to use a targeted policy, the SpamAssassin daemon, `spamd`, is protected by SELinux. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with **system-config-selinux**” on page 416.

# Configuring SpamAssassin

SpamAssassin looks in many locations for configuration files; for details, refer to the `spamassassin man` page. The easiest configuration file to work with is `/etc/mail/spamassassin/local.cf`. You can edit this file to configure SpamAssassin globally. Users can override these global options and add their own options in the `~/.spamassassin/user_prefs` file. You can put the options discussed in this section in either of these files. You can use `perldoc` (page 977) to display information on SpamAssassin options:

```
`$ perldoc Mail::SpamAssassin::Conf`
```