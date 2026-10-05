# Chapter 20 Electronic Mail

Using the colon as a value separator presents a problem when you express IPv6 addresses, which use colons as parts of the address. You can escape the colons by doubling them, but the easiest and most readable fix is to redefine the separator character with the < character as assign values to the option. For example, both of the two lines set the value of the localhost_interfaces option, which contains the IPv4 and IPv6 localhost addresses:

```
local_interfaces = 127.0.0.1 ::1
local_interfaces = <; 127.0.0.1 ::1
```

The second form, in which the semicolon has been defined as the separator, is more readable and less fragile.

There are a options—more than 500 in the options index of the documentation. And we said sendmail was complicated! Most options have sensible defaults, and all have descriptive names. It's handy to have a copy of the doc/spec.txt file from the distribution in your favorite text editor when you are researching a new option. We don't cover all the options, just the ones that occur in our example configuration.

# Lists

Exim has four kinds of lists, introduced by the keywords hostlist, domainlist, addresslist, and localpartslist. Here are two examples using hostlist:

+   - hostlist_my_relay_list = 192.168.1.0/24 : friend.example.com
- hostlist_my_relay_list = /usr/local/exim/relay_hosts.txt

Members can be listed in-line or taken from a file. If in-line, they are separated by colons. There can be up to 16 named lists of each type. In the in-line example above, we include all machines on a local /24 network and a specific hostname.

The symbol @ can be a member of a list; it means the name of the local host and makes it possible to write a single generic configuration file for most nonhosts at your site. The notation [] is also useful and means all IP addresses on which Exim is listening; that is, all IP addresses of localhost.

To reference a list, just put + in front of its name to match the list or ! to match nonmembers; for example, +my_relay_list. There must be no space between + and the name of the list.

Lists can include references to other lists and the $ indication name. Lists that include references to variables (e.g., $variable_name) make processing slower because Ultim cannot cache the results of evaluating the list, which it does by default.

# Macros

You can use macros to define parameters, error messages, etc. The parsing is primitive, so you cannot define a macro whose name is a subset of another macro unpredictable.