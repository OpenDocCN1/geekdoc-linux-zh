The format of the `buildarchtranslate` entry is slightly different from most other `rpmmfc` file entries. Instead of the usual `<name>:<value>` format, the `buildarchtranslate` entry looks like this:

`buildarchtranslate:<label>: <string>`

The `<label>` is compared against information from `uname(2)`. If a match is found, then `<string>` is used by RPM to define the build architecture.

# B.4.4. `buildosttranslate`

The `buildosttranslate` entry is used in the process of defining the operating system RPM will use as the build operating system. As the name implies, it is used to translate the raw information returned by `uname(2)` to the canonical operating system defined by `os_canon`.

The format of the `buildosttranslate` entry is slightly different from most other `rpmmfc` file entries. Instead of the usual `<name>:<value>` format, the `buildosttranslate` entry looks like this:

`buildosttranslate:<label>: <string>`

`<label>` is compared against information from `uname(2)`. If a match is found, `<string>` is used by RPM to define the build operating system.

# B.4.5. `arch_compat`

The `arch_compat` entry is used to define which architectures are compatible with one another. This information is used when packages are installed; in this way, RPM can determine whether a given package file is compatible with the system. The format of the entry is

`arch_compat:<label>: <list>`

`<label>` is an architecture string, as defined by an `arch_canon` entry. `<list>` following it consists of one or more architectures, also defined by `arch_canon`. If there is more than one architecture in the list, they should be separated by a space.

The architectures in the list are considered compatible to the architecture specified in the label.

# B.4.6. `os_compat`

Default value: (operating system specific)

The `os_compat` entry is used to define which operating systems are compatible with one another. This information is used when packages are installed; in this way, RPM can determine whether a given package file is compatible with the system. The format of the entry is

`<name>;<label>: <list>`