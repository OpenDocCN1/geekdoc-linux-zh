# Environment-Related Modules

The modules listed in Table 5-1 enable you to manipulate the environment that is available to other modules or to external programs, such as CGI (Common Gateway Interface) scripts, SSI (Server-Side Include), mod_perl scripts, PHP scripts, Java servlets, and the like.

| | | |
|---|---|---|
| | | **Table 5-1** |
| | | **Environment-Related Modules** |
| **Module** | | **Purpose** |
| `mod_env` | | Passes environments to external programs such as CGI and SSI scripts. |
| `mod_setenvif` | | Sets conditional environment variables using information from the client side. |
| `mod_unique_id` | | This module generates a unique ID per request. It has no directives. This module is not compiled by default. You must configure the source by using `-enable-unique-id` option with the `configure` script and by compiling and installing Apache. |

# mod_env

`mod_env` is compiled by default. It enables you to pass environment variables to external programs such as CGI scripts, SSI, `mod_perl` scripts, PHP scripts, and the like. `mod_env` has the following directives.

# PassEnv

The `PassEnv` directive tells the module to pass one or more environment variables from the server’s own environment to the CGI and SSI scripts.

**Syntax:** `PassEnv variable [...]

Context:** Server config, virtual host

For example, the following directive passes the HOSTTYPE and PATH environment variables to programs.

```
`PassEnv HOSTTYPE PATH`
```