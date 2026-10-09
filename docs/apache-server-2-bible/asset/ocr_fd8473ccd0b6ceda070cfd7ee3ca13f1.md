**Syntax:** ISAPIReadAheadBuffer `size`
**Default setting:** ISAPIReadAheadBuffer `49152`
**Context:** Server config

# ISAPILogNotSupported

The `ISAPILogNotSupported` directive enables or disables logging of all unsupported feature requests from ISAPI extension DLLs. This is only useful to isolate a problem related to an ISAPI extension that is not behaving properly.

**Syntax:** ISAPILogNotSupported `On` | `Off`
**Default setting:** ISAPILogNotSupported `on`
**Context:** Server config

# ISAPIAppendLogToErrors

The `ISAPIAppendLogToErrors` directive enables or disables the storing of requests from ISAPI extension DLLs in the error log.

**Syntax:** ISAPIAppendLogToErrors `On` | `Off`
**Default setting:** ISAPIAppendLogToErrors `Off`
**Context:** Server config

# ISAPIAppendLogToQuery

The `ISAPIAppendLogToQuery` directive enables or disables logging of query data to server's access log.

**Syntax:** ISAPIAppendLogToQuery `On` | `Off`
**Default setting:** ISAPIAppendLogToQuery `Off`
**Context:** Server config

# UserDir in Windows

Apache currently does not work with Windows user accounts and therefore it cannot detect home directories for Windows users. If you wish to provide Web sites for users, the following workaround can be used:

+   1. Choose a directory to be the top-level home directory for all users.
+   For example, you can create a directory called `C:\home` and use it for this purpose.