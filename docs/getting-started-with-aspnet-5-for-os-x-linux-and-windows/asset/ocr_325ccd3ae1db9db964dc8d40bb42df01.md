```
dnvm alias <alias>
    display value of the specified alias

dnvm alias <alias> <semver>|<alias>|<package>
    <alias>
        <semver>|<alias>|<package>   the name of the alias to set
        the DN X version to set the alias to. Alternative ly use the version of the specified alias

dnvm unalias <alias>
    remove the specified alias

dnvm [help|-h|--help|--help]
    displays this help text.

dnvm update-self
    updates dnvm itself.
agusk$ dnvm list

Active Version                Runtime Arch Location                 Alias
----- ------                  ---- ---- ----- ---                 -----
    *  1.0.0-beta4            mono            ~/.dnx/runtimes      default
agusk$

```