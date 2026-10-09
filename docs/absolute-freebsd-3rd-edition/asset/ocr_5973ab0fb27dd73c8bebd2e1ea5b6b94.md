An alias is a single word for the alias name, either a colon or an equal sign, and then the pkg command to run. If you run `pkg all-depends`, `pkg(8)` looks in `pkg.conf` and runs `pkg query %dn-%dv`. Every alias ends in a colon to indicate that the aliases list continues on the next line.

Many of the aliases in the default configuration represent hangovers from the `pkg_add` aeon, created for us old timers. The existing aliases are a great place to find sample queries and searches, though. And searching through the aliases turns up this fine entry:

```
noauto = "query -e '%a == 0' '%n-%v'",
```

This alias, *noauto*, runs a `pkg query` command to evaluate `%a` and print the package’s name and version number if it’s 0. It prints packages that weren’t automatically installed. I added a very similar alias to print automatic packages.

```
auto = "query -e '%a == 1' '%n-%v'",
```

When you find yourself repeatedly running complex commands, add aliases.

# Uninstalling Packages

We’ve all installed software only to rip it out in disgust. The only difference is what, exactly, disgusted us. Uninstall packages with the `pkg delete` subcommand. It’s also available as `pkg remove`. That extraneous `youtube_dl` package? Let’s remove it from the system.

```
# pkg delete youtube_dl
Checking integrity... done (0 conflicting)
```

The removal process makes sure that nothing terrible has happened to the package, that nobody else needs it, and that its removal won’t do terrible things that the package system can predict.²

You’ll then get a list of packages to be removed and how much space they’ll free up. At the end is a final chance to say no.