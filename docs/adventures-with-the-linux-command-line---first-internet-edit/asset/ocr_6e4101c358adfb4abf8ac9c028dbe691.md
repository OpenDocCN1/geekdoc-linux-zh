```
me@linuxbox:~/adventure-sql$ .insert_package_files.awk \
      < package_files-deb.tsv \
      | sqlite3 adv-sql.sqlite
```

The second table is named Package_Files. Here is its schema:

```
sqlite> .schema Package_Files
CREATE TABLE Package_Files (
    package_name VARCHAR(60),
    file VARCHAR(120),
    size_bytes INTEGER
);
```

As we can see, this table has 3 columns: the package name, the name of a file installed by the package, and the size of the installed file in bytes. Let's do a SELECT to see which table works.

```
sqlite> headers on
sqlite> mode column
sqlite> width 15 50 -10
sqlite> SELECT * FROM Package_Files WHERE package_name = 'bash'
```

| package_name | size_bytes |
|---|---|
| /bin/bash | 1113504 |
| /etc/bash.bashrc | 2319 |
| /etc/skel/.bash_logout | 10312 |
| /etc/skel/.profile | 3771 |
| /usr/bin/bashbug | 807 |
| /usr/bin/clear_console | 7115 |
| /usr/share/doc/bash/COMPAT.gz | 7853 |
| /usr/share/doc/INTRO.gz | 2921 |
| /usr/share/doc/README | 2793 |
| /usr/share/doc/POSIX.gz | 3702 |
| /usr/share/doc/RASBH | 1693 |
| /usr/share/doc/README | 3839 |
| /usr/share/doc/Debian.Debian | 1919 |
| /usr/share/doc/README.abs-guide | 1105 |
| /usr/share/doc/README.commands.gz | 3021 |
| /usr/share/doc/bash/changelog.Debian | 1357 |
| /usr/share/doc/bash/copgrl.gz | 1023 |
| /usr/share/doc/bash/inputrc.arrows | 726 |
| /usr/share/doc/bash/lintian/overrides/bash | 156 |
| /usr/share/man/man/bash.1.gz | 86656 |
| /usr/share/man/man/bashinfo.1.gz | 804 |
| /usr/share/man/man/clear_console.1.gz | 1194 |
| /usr/share/man/man/bash.1.gz | 154 |
| /usr/share/man/man7/bash-builds.7.gz | 508 |
| /usr/share/man/menu/bash | 194 |
| /bin/bash | 4 |

Notice the .width column above. A negative value causes the corresponding column to be right-aligned.

# Subqueries

The SELECT statement can be used to produce many kinds of output. For example, it can be used to simply print literal strings.