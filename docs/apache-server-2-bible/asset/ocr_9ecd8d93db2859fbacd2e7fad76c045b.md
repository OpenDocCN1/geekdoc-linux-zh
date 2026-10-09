You can also use the **built-in** `ob_start()` and `ob_end_flush()` directives to start and end flushing of the contents directly. **For example**:

```
<?php
ob_start();  // Buffer all output
echo "Buffered contents \n";
ob_end_flush(); // Page rendered. flush the output buffer.
?>
```

Here the output is buffered.

# safe_mode

The `safe_mode` directive sets the safe mode for PHP when it is used as a CGI solution. When set to `On`, this directive ensures that PHP scripts run by the PHP interpreter in CGI mode are not allowed any access beyond the document root directory of the Web site.

+   *   **Syntax:** `safe_mode On | Off`
+   *   **Default setting:** `safe_mode Off`

# safe_mode_allowed_env_vars

The `safe_mode_allowed_env_vars` directive enables you to set a prefix for all the environment variables that a user can change by using the `putenv()` function. The default value enables users to change any environment variable that starts with `PHP_` prefix.

+   *   **Syntax:** `safe_mode_allowed_env_vars prefix`
+   *   **Default setting:** `safe_mode_allowed_env_vars PHP_`

# safe_mode_protected_env_vars

The `safe_mode_protected_env_vars` directive allows you to set a comma-delimted list of environment variables that cannot be changed by any PHP script that uses the `putenv()` function.

+   *   **Syntax:** `safe_mode_protected_env_vars environment_variable [environment_variable ...]`
+   *   **Default setting:** `safe_mode_protected_env_vars = LD_LIBRARY_PATH`

If you wish to protect all the environment variable that starts with `HTTP_` prefix, you can use:

```
safe_mode_protected_env_vars = HTTP_
```