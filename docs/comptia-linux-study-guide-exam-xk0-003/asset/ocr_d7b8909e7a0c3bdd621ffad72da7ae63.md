automatically loads dependencies. This greater convenience means that **mdprobe** relies on configuration files. It also means that you can use options (placed between the command name and the module name) to modify **mdprobe**'s behavior, as summarized in Table 1.3.

# **TABLE 1.3 Options for mdprobe**

| Option | Effect |
| :--- | :--- |
| `-v` or `--verbose` | This option tells mdprobe to display extra information about its operations. Typically, this includes a summary of every `lnsmod` operation it performs. |
| `-C filename` | The mdprobe program uses a configuration file called `/etc/modprobe.conf`. You can change the file by passing a new file with this option, as in `mdprobe -C /etc/mymdprobe.conf floppy`. |
| `-n` or `--dry-run` | This option causes mdprobe to perform checks and all other operations *except* the actual module insertions. You might use this option in conjunction with `-v` to see what mdprobe would do without loading the module. This may be helpful in debugging problems. |
| `-r` or `--remove` | This option reverses mdprobe's usual effect; it causes the program to remove the specified module and any on which it depends. (Depended-on modules are *not removed* if they're in use.) |
| `-f` or `--force` | This option tells mdprobe to force the module loading even if the kernel version doesn't match what the module expects. This action is potentially dangerous, but it's occasionally required when using third-party binary-only modules. |
| `--show-depends` | You can see all the modules on which the specified module depends by using this option. It doesn't install any of the modules; it's purely informative in nature. |
| `-l` or `--list` | This option displays a list of available options whose names match the wildcard you specify. For instance, typing `mdprobe -l v*` displays all modules whose names begin with `v`. If you provide no wildcard, mdprobe displays all available modules. Like `--show-depends`, this option doesn't cause any modules to be loaded. |

![](bbox=[0.13, 0.81, 0.23, 0.88])

> Table 1.3 is incomplete. Other mdprobe options are relatively obscure, so you're not likely to need them often. Consult the **mdprobe** man page for more information.