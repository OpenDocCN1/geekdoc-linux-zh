# OffSec

By prematurely terminating the implied SQL query again, we can inject an arbitrary statement:

```
' or 1=1 in (select @version) -- //
```

Listing 192 - Error-based payload

In this case, we want to retrieve the MySQL version via the @@version directive.

> MySQL accepts both version() and @@version statements.

We can now paste the injection payload in the Username field and verify the returned output.