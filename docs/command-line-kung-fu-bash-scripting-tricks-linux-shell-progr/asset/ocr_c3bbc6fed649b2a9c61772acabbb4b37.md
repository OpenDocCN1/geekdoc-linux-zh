```
$ wikidig jazz
"Jazz is a musical style that originated at the beginning of the 20th century in black communities in the Southern United States. It was born out of a mix of African and European music traditions. Its African pedigree is evident in its use of blue notes, improvisation, polyrhythms, syncopation and the swung note. From its early development until the present day jazz has also…
http://en.wikipedia.org/wiki/Jazz"
```

# Make Non-Interactive Shell Sessions Behave the Same as Interactive Sessions

Make any customizations in `~/bashrc`. The contents of `~/bash_profile`:

```
if [ -f ~/.bashrc ]; then
source ~/.bashrc
fi
```

The shell behaves in slightly different ways when you log on interactively versus when you just connect to run a single command. The contents of .profile or .bash_profile are only executed for interactive sessions. If you are not aware of this subtle difference it may leave you scratching your head as to why something works perfectly when you log in and execute a command versus when you just ssh in to run that same command. You can save yourself some hassle by making your interactive and non-interactive sessions behave the same. To do this, configure .bash_profile to reference .bashrc and put all of your configuration in .bashrc.

Here is an example to better illustrate the difference between interactive and non-interactive shells. For example, if you define an alias for ll in `~/bash_profile` it will work during an interactive session but it will not be available during a non-interactive session.