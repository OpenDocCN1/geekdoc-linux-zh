# ## LOGGING DIRECTIVES

**ErrorLog** *Specifies where Apache sends error messages.*

```
```
ErrorLog filename | syslog[:facility]
```
```

where *filename* specifies the name of the file, relative to ServerRoot (page 955), that Apache sends error messages to. The **syslog** keyword specifies that Apache send errors to **syslogd** (page 620); *facility* specifies which **syslogd** facility to use. The default facility is **local7**.

Contexts: **server config, virtual host**
Default: **logs/error_log**
Fedora/RHEL: **logs/error_log**

**LogLevel** *Specifies the level of error messages that Apache logs.*

```
```
LogLevel level
```
```

where *level* specifies that Apache log errors of that level and higher (more urgent). Choose *level* from the following list, which is presented here in order of decreasing urgency and increasing verbosity:

+   *   **emerg**    System unusable messages
+   *   **alert**    Need for immediate action messages
+   *   **crit**     Critical condition messages
+   *   **error**    Error condition messages
+   *   **warn**     Nonfatal warning messages
+   *   **notice**   Normal but significant messages
+   *   **info**     Operational messages and recommendations
+   *   **debug**    Messages for finding and solving problems

Contexts: **server config, virtual host**
Default: **warn**
Fedora/RHEL: **warn**

# ## DIRECTIVES THAT CONTROL CONTENT

**AddHandler** *Creates a mapping between filename extensions and a built-in Apache handler.*

```
```
AddHandler handler extension [extension] ...
```
```

where *handler* is the name of a built-in handler and *extension* is a filename extension that maps to the **handler**. Handlers are actions that are built into Apache and are directly related to loaded modules. Apache uses a handler when a client requests a file with a specified filename extension.

For example, the following **AddHandler** directive causes Apache to process files that have a filename extension of **.cgi** with the **cgi-script** handler:

```
```
AddHandler cgi-script .cgi
```
```