Returning to the redhat.mc file, the next line is the following:

```
define('confDEF_USER_ID','8:12')
```

A **define** statement creates a new macro or assigns a value to an existing macro. The first item is the name of the macro, which is confDEF_USER_ID in this instance. Second is what this macro expands to, if you want to set that value immediately. In this case, the macro expands to 8:12. Two back quotes and two apostrophes are included because the colon is a metacharacter. The double quotes allow it to be taken literally rather than be specially interpreted.

Next is the following line:

```
OSTYPE('linux')
```

You want this line to appear like this regardless of which Linux distribution you use. After this line is the following:

```
undefine('UUCP_RELAY')
undefine('BITNET_RELAY')
```

An **undefine** statement is used to remove existing macros from the final product. Many macros are available in **m4**, but the ones discussed here are those that are specific to configuring **sendmail**. The **m4** macro processor itself is a very useful tool. To learn more about it, go to www.gnu.org/manual/m4-1.4/m4.html.

The two macros removed at this stage are UUCP_RELAY and BITNET_RELAY. These were both at one point fairly standard, but today are not often used. Unless you are using Unix-to-Unix Copy (UUCP) to deliver mail and use intermittently connected machines, you need nothing UUCP-related. And, unless you have a specific need to send email to BITNET (Because It's Time Network)—a network originally created to connect universities together, which uses a different addressing structure than the Internet—removing this macro isn't harmful, either.

> **NOTE:** For more information on the various relay macros, go to **www.sendmail.org/m4/domains.html**.

After this section comes a series of macro definitions, such as these:

```
define('confAUTO_REBUILD')
define('confTO_CONNECT', '1m')
define('confTRY_NULL_MX_LIST',true)
define('confDONT_PROBE_INTERFACES',true)
define('PROCMAIL_MAILER_PATH','/usr/bin/procmail')
```