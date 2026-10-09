
first back-reference string $1 corresponds to the string found in the first set of parentheses (from the left). So $1 is set to whatever is matched in `(\*/J+)` and $2 is set to the next string found in `(.*)`. When a URL request is as follows:

```
http://blackhole.evoknow.com/~kabir/welcome.html
```

The value of $1 is `kabir`, and $2 is `welcome.html`; so the substitution string looks like:

```
/users/kabir/welcome.html
```

When you have **more than one `RewriteRule`** specified, the first `RewriteRule` operates on the original URL and if a match occurs, the second rule no longer operates on the original URL. Instead, it gets the URL substituted by first rule as the URL on which to apply rules. In a scenario in which a match occurs at every step, a set of three rewrite rules will function as follows:

```
RewriteRule search-pattern-for-original-URL substitution1
    [flags]
RewriteRule search-pattern-for-substitution1 substitution2
    [flags]
RewriteRule search-pattern-for-substitution2 substitution3
    [flags]
```

It is possible to apply more than one rule to the original URL by using the `C` flag to instruct the rewrite engine to chain multiple rules. In such a case, you may not want to substitute until all rules are matched so that you can use a special substitution string to disable a substitution in a rule.

Table 9-2 lists the details of the possible flags.

| **Flag** | **Meaning** |
| :--- | :--- |
| `C \| chain` | This flag specifies that the current rule be chained with the next rule. When chained by a `C` flag, a rule is looked at if and only if the previous rule in the chain results in a match. Each rule in the chain must contain the flag, and if the first rule does not match, the entire chain of rules is ignored. |
| `E=var:value` | You can set an environment variable using this directive. The variable is accessible from rewrite conditions, Server Side Includes, CGI scripts, and so on. |
| `F \| forbidden` | When a rule using this flag is matched, an HTTP response header called `FORBIDDEN` (status code 403) is sent back to the browser. This effectively disallows the requested URL. |
| `G \| gone` | When a rule using this flag is matched, an HTTP response header called GONE (status code 410) is sent back to the browser. This informs the browser that the requested URL is no longer available on this server. |
| `L \| last` | This tells the rewrite engine to end rule processing immediately so that no other rules are applied to the last substituted URL. |
| `N \| next` | This tells the rewrite engine to restart from the first rule. However, the first rule no longer tries to match the original URL, because it now operates on the last substituted URL. This effectively creates a loop. You must have terminating conditions in the loop to avoid an infinite loop. |
| `NC \| nocase` | This tells the rewrite engine to become case insensitive for the pattern match |
| `NS \| nosubreq` | Use this flag to avoid applying a rule on an internally generated URL request. |
| `P \| proxy` | Using this flag will convert a URL request to a proxy request internally. This will only work if you have compiled Apache with the `mod_proxy` module and configured it to use the proxy module. |
| `QSA \| qsaappend` | This flag allows you to append data (such as key=value pairs) to the query string part of the substituted URL. |
| `R [= HTTP code] \| redirect` | Forces external redirects to client while prefixing the substitution with `http://server[:port]/`. If no HTTP response code is given, the default redirect response code 302 (MOVED TEMPORARILY) is used. This rule should be used with the L or last flag. |
| `S=n \| skip=n` | Skips next n rules. |
| `T=MIME-type \| file type=MIME-type` | Forces the specified MIME-type to be the MIME-type of the target of the request. |

Note You can add conditions to your rules by preceding them with one or more `RewriteCond` directives, which are discussed in the following section.

### RewriteCond

The `RewriteCond` directive is useful when you want to add an extra condition for a rewrite rule specified by the `RewriteRule` directive. You can have several `RewriteCond` directives per `RewriteRule`. All rewrite conditions must be defined before the rule itself.

**Syntax:** `RewriteCond _test_string_ condition_pattern [_flag-list_]`

**Default:** None

**Context:** Server config, virtual host, per-directory config (`.htaccess`)

The test string may be constructed with plain text, server variables, or back-references from both the current rewrite rule and the last rewrite condition. To access the *nth* back-reference from the last `RewriteRule` directive, use `$n`; to access the *nth* back-reference from the last `RewriteCond` directive, use `%n`.

To access a server variable, use the `${_variable name_}` format. For example, to access the `REMOTE_USER` variable, specify `%{REMOTE_USER}` in the test string.

Table 9-3 lists several special data access formats.

| Format Specifier | Meaning |
| :--- | :--- |
| `%{ENV:_variable_}` | Use this to access any environment variable that is available to the Apache process. |
| `%{HTTP:_header_}` | Use this to access the HTTP header used in the request. |
| `%{LA-U:_variable_}` | Use this to access the value of a variable that is not available in the current stage of processing. For example, if you need to make use of the `REMOTE_USER` server variable in a rewrite condition stored in the server's configuration file (`httpd.conf`), you cannot use `%{REMOTE_USER}` because this variable is only defined after the server has performed the authentication phase, which comes after `mod_rewrite`'s URL processing phase. To look ahead at what the username of the successfully authenticated user is, you can use `%{LA-U:REMOTE_USER}` instead. However, if you are accessing the `REMOTE_USER` data from a `RewriteCond` in a per-directory configuration file, you can use `%{REMOTE_USER}` because the authorization phase has already finished and the server variable has become available as usual. The lookup is performed by generating a URL-based internal subrequest. |
| `%{LA-F:_variable_}` | Same as the `%{LA-U:_variable_}` in most cases, but lookup is performed using a filename-based internal subrequest. |

The condition pattern can also use some special notations in addition to being a regular expression. For example, you can perform lexical comparisons between the test string and the condition pattern by prefixing the condition pattern with a `<`, `>`, or `=` character. In such a case, the condition pattern is compared with the test string as a plain-text string.

There may be times when you want to check whether the test-string is a file, directory, or symbolic link. In such a case, you can replace the condition pattern with the special strings shown in Table 9-4.

| Conditional Options | Meaning |
| :--- | :--- |
| `-d` | Tests whether the test-string-specified directory exists |
| `-f` | Tests whether the test-string-specified file exists |
| `-s` | Tests whether the test-string-specified nonzero-size file exists |
| `-l` | Tests whether the test-string-specified symbolic link exists |
| `-F` | Tests the existence and accessibility of the test-string-specified file |
| `-U` | Tests the validity and accessibility of the test-string-specified URL |

You can use `!` in front of the above conditions to negate their meanings. The optional flag list can consist of one or more comma-separated strings as shown in Table 9-5.

| Flag | Meaning |
| :--- | :--- |
| `NC` | nocase: Performs a case-insensitive condition test. |
| `OR` | ornext: Normally, when you have more than one `RewriteCond` for a `RewriteRule` directive, these conditions are AND'ed together for the final substitution to occur. However, if you need to create an OR relationship between two conditions, use this flag. |
