```
```
agusk@ubuntu15:~$ dnvm upgrade
Determining latest version
Latest version is 1.0.0-beta4
Downloading dnx-mono.1.0.0-beta4 from https://www.nuget.org/api/v2
Download: https://www.nuget.org/api/v2/package/dnx-mono/1.0.0-beta4
############################################## 100.0%
Installing to /home/agusk/.dnx/runtimes/dnx-mono.1.0.0-beta4
Adding /home/agusk/.dnx/runtimes/dnx-mono.1.0.0-beta4/bin to process PATH
Setting alias 'default' to 'dnx-mono.1.0.0-beta4'
agusk@ubuntu15:~$ dnvm help

    ██████████████████████████

.NET Version Manager - Version 1.0.0-beta6-10381
By Microsoft Open Technologies, Inc.

DNVM can be used to download versions of the .NET Execution Environment and mana
ge which version you are using.
You can control the URL of the stable and unstable channel by setting the DNx_FE
ED and DNx_UNSTABLE_FEED variables.

Current feed settings:
```

```

You can also see a list of your DNx runtime by typing this command.

```
```
$ dnvm list
```

```

```
```
dnvm alias <alias>
    display value of the specified alias

dnvm alias <alias> <sever>|<alias>|<package>
    <alias>              the name of the alias to set
    <sever>|<alias>|<package>    the DNx version to set the alias to. Alternativel
    y use the version of the specified alias

dnvm unalias <alias>
    remove the specified alias

dnvm [help|-h|-help|--help]
    displays this help text.

dnvm update-self
    updates dnvm itself.
agusk@ubuntu15:~$ dnvm list

Active Version          Runtime Arch Location           Alias
--------- ----------    --------  ---  --------    -----   ----
        *   1.0.0-beta4    mono      ~/.dnx/runtimes    default

agusk@ubuntu15:~$
```

```