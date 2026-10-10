# NOTES

If applying any specified option fails, *program* will not be run and **setpriv** will return with exit code 127.

Be careful with this tool — it may have unexpected security consequences. For example, setting `no_new_privs` and then execing a program that is SELinux-confined (as this tool would do) may prevent the SELinux restrictions from taking effect.