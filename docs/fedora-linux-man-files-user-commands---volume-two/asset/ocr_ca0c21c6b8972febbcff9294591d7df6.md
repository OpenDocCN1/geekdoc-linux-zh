# OPTIONS

The following options are supported:

# General Options

**-h, —help**

Prints a short help text and exits.

**-V, —version**

Print the version string of firewalld. This option is not combinable with other options.

**-q, —quiet**

Do not print status messages.

# Status Options

**—state**

Check whether the firewalld daemon is active (i.e. running). Returns an exit code 0 if it is active, *NOT_RUNNING* otherwise (see the section called “EXIT CODES”). This will also print the state to *STDOUT*.

**—reload**

Reload firewall rules and keep state information. Current permanent configuration will become new runtime configuration, i.e. all runtime only changes done until reload are lost with reload if they have not been also in permanent configuration.

**—complete-reload**

Reload firewall completely, even netfilter kernel modules. This will most likely terminate active connections, because state information is lost. This option should only be used in case of severe firewall problems. For example if there are state information problems that no connection can be established with correct firewall rules.

**—runtime-to-permanent**

Save active runtime configuration and overwrite permanent configuration with it. The way this is supposed to work is that when configuring firewalld you do runtime changes only and once you’re happy with the configuration and you tested that it