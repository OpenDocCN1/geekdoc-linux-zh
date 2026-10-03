# Setting the System Locale, Terminal, Timezone, and Time Server

The keyword to set the system locale is:

```
system_locale=<value>
```

Where <value> is an entry from the /usr/lib/locale directory. The following example sets the value to English:

```
system_locale=en_US
```

The keyword to set the terminal type is:

```
terminal=<terminal_type>
```

Where <terminal_type> is an entry from the /usr/share/lib/terminfo database. The following example sets the terminal type to vt100:

```
terminal=vt100
```

The keyword to set the timezone is:

```
timezone=<timezone>
```

Where <timezone> is an entry from the /usr/share/lib/zoneinfo directory. The following entry sets the timezone to Eastern Standard Time:

```
timezone=EST
```

The keyword to set the time server is

```
timeserver=<value>
```

Where <value> can be LOCALHOST, HOSTNAME, or IP_ADDRESS. The following example sets the time server to be the localhost:

```
timeserver=localhost
```

The following rules apply to keywords in the sysidcfg file:

+   ♦ Keywords can be in any order.
♦ Keywords are not case-sensitive.
♦ Keyword values can be optionally enclosed in single quotes (').
♦ Only the first instance of a keyword is valid; if you specify the same keyword more than once, the first keyword specified will be used.