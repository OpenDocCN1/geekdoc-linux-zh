# # 11.  DNS With BIND

**TIP:** Review Chapter 9’s discussion of logging to refresh your memory of which entities **syslogd** knows and what the severity levels are.

Or, maybe you want to send particular types of data into the great /dev/null void (anything sent here gets discarded). You can do so with the following:

```
null;
```

You can also choose what gets printed. Three items are available for this:

```
print-category value;
print-severity value;
print-time value;
```

In all three cases, the value is either **yes** or **no**. None of these three is necessary. Choose as many or as few as you need. Finally, the **channel** part of the **logging** statement is done, so close it, if you used it, with the following:

```
};
```

The other subsection available in a **logging** statement is **category**, with which you can lump a number of different channels together and specify categories of information that need to be logged. The available categories are listed in Table 11.3.

**Table 11.3** Categories available in /etc/named.conf.

| Category | Logs |
| :------- | :------------------------------------------------------------- |
| **cname** | Messages that list what points to a CNAME value. |
| **config** | Messages pertaining to the configuration file. |
| **db** | Database operations. |
| **default** | What you get if you do not specify categories. Many consider this setting to be sufficient, because it logs **syslog** and **debug** messages. |
| **event** | Messages that pertain to timed events, user-action–initiated events, events opened by other programs, and more. |
| **insist** | Messages pertaining to internal consistency checks. |
| **lame-servers** | Messages pointing out that a server **named** dealt with was not fully compliant with the latest protocols. |
| **load** | Messages pertaining to zone data loading. |
| **maintenance** | Messages pertaining to maintenance routines. |
| **ncache** | Messages regarding failed lookup caching. |