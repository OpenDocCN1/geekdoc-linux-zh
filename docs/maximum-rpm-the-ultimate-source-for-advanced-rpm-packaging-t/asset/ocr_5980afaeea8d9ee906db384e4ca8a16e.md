# Table 5.1. Query-mode command syntax and options.

| | Options | Package Selection Options | Section |
|---|---|---|---|
| | rpm -q (or --query) | | |
| | pkg1...pkgN | Query installed package(s) | 5.2.1.1 |
| | -p <file> (or .) | Query package file <file> (URLs are usable) | 5.2.1.4 |
| | -f <file> | Query package owning <file> | 5.2.1.3 |
| | -a | Query all installed packages | 5.2.1.2 |
| | --whatprovides <x> | Query packages providing capability <x> | 5.2.1.6 |
| | -g <group> | Query packages belonging to group <group> | 5.2.1.5 |
| | --whatrequires <x> | Query packages requiring capability <x> | 5.2.1.7 |
| | | | |
| | | Information Selection Options | Section |
| | <null> | Display full package label | 5.2.2 |
| | -i | Display summary package information | 5.2.2.1 |
| | -l | Display list of files in package | 5.2.2.2 |
| | -c | Display list of configuration files | 5.2.2.4 |
| | -d | Display list of documentation files | 5.2.2.5 |
| | -s | Display list of files in package, with state | 5.2.2.6 |
| | --scripts | Display install, uninstall, verify scripts | 5.2.2.10 |
| | --queryformat (or -qf) | Display queried data in custom format | 5.2.2.11 |
| | --dump | Display all verifiable information for each file | 5.2.2.9 |
| | --provides | Display capabilities package provides | 5.2.2.7 |
| | --requires (or -R) | Display capabilities package requires | 5.2.2.8 |
| | | | |
| | | General Options | Section |
| | -v | Display additional information | 5.2.2.3 |
| | -vv | Display debugging information | 5.2.3 |
| | --root <path> | Set alternate root to <path> | 5.2.4 |
| | --rcfile <rcfile> | Set alternate rpmc file to <rcfile> | 5.2.5 |
| | --dbpath <path> | Use <path> to find the RPM database | 5.2.6 |