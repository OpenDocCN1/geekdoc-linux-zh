**Syntax:** `magic_quotes_gpc` `On` | `Off`

**Default setting:** `magic_quotes_gpc` `On`

# magic_quotes_runtime

The `magic_quotes_runtime` directive enables or disables automatic quoting of internally generated text. In other words, if you retrieve a record from database that has the `<?php` anything goes here `?>` type of tag embedded in it, the contents within the tags (which is part of the data) will be escaped (i.e. not processed) and not treated as PHP code.

**Syntax:** `magic_quotes_runtime` `On` | `Off`

**Default setting:** `magic_quotes_runtime` = `Off`

# max_execution_time

The `max_execution_time` directive sets the maximum time that a script can run to produce output. After a script goes past specified amount of seconds, PHP times out the script. Unless you plan on running PHP scripts that take a lot of time, the default value should be acceptable for most situations.

**Syntax:** `max_execution_time` `seconds`

**Default setting:** `max_execution_time` `30`

# memory_limit

The `memory_limit` directive sets the maximum RAM a PHP script can consume. The default, 8MB, should be plenty for small-to-modest PHP scripts. You can specify memory in bytes as well.

**Syntax:** `memory_limit` `bytes` `[nM]`

**Default setting:** `memory_limit` `8M`

For example, the following are equivalent:

```
```text
memory_limit 8M
memory_limit 8388608
```
```

# output_buffering

The `output_buffering` directive allows you to enable or disable output buffering. When it is set to `On`, you can print HTTP headers anywhere in a PHP script. Being able to output a header in the middle of a script even after printing other contents means that a script can display an error page even if it was partially successful earlier.

**Syntax:** `output_buffering` `On` | `Off`

**Default setting:** `output_buffering` `On`