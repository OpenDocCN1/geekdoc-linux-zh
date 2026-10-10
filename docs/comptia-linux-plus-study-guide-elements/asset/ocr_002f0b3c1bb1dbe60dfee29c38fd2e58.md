automatically loads dependencies. This greater convenience means that **modprobe** relies on configuration files. It also means that you can use options (placed between the command name and the module name) to modify **modprobe**'s behavior, as summarized in Table 1.3.

# TABLE 1.3 Options for modprobe

| Option | Effect |
|---|---|
| -v or --verbose | This option tells modprobe to display extra information about its operations. Typically, this includes a summary of every insmod operation it performs. |
| -C filename | The modprobe program uses a configuration file called /etc/modprobe.conf. You can change the file by passing a new file with this option, as in modprobe -C /etc/mymodprobe.conf floppy. |
| -n or --dry-run | This option causes modprobe to perform checks and all other operations except the actual module insertions. You might use this option in conjunction with -v to see what modprobe would do without loading the module. This may be helpful in debugging problems. |
| -r or --remove | This option reverses modprobe's usual effect; it causes the program to remove the specified module and any on which it depends. (Depended-on modules are not removed if they're in use.) |
| -f or --force | This option tells modprobe to force the module loading even if the kernel version doesn't match what the module expects. This action is potentially dangerous, but it's occasionally required when using third-party binary-only modules. |
| --show-depends | You can see all the modules on which the specified module depends by using this option. It doesn't install any of the modules; it's purely informative in nature. |
| -l or --list | This option displays a list of available options whose names match the wildcard you specify. For instance, typing modprobe -l v* displays all modules whose names begin with v. If you provide no wildcard, modprobe displays all available modules. Like --show-depends, this option doesn't cause any modules to be loaded. |

> Table 1.3 is incomplete. Other modprobe options are relatively obscure, so you're not likely to need them often. Consult the modprobe man page for more information.