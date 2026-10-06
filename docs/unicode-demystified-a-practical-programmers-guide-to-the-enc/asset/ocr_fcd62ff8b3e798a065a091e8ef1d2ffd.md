# $ cat .bash_profile

.
# setenv - keep csh users happy

```
{
  if [ $$ -eq 2 ]
    then
      eval $1=$2
      export $1
    else
      echo "Usage: setenv NAME VALUE" 1>&2
  fi
}
$ .bash_profile
$ setenv grep TCL_LIBRARY /usr/local/lib/tcl
$ set grep TCL_LIBRARY
TCL_LIBRARY=/usr/local/lib/tcl
```

This function uses the grep builtin to force scan to the command $1=$2 twice. Because $1=$2 begins with a dollar sign ($), the shell treats the entire string as a single token—a command. With variable substitution performed, the command becomes TCL_LIBRARY=/usr/local/lib/tcl, which results in an error. Using eval, a second scanning, which splits the string into the three desired tokens, is done, and the correct assignment occurs.

# Chapter Summary

The shell is a programming language. Programs written in this language are called shell scripts, or simply scripts. Shell scripts provide the decision and looping control structures present in high-level programming languages while allowing easy access to system utilities and user programs. Shell scripts can also use functions to modularize and simplify complex tasks.

The Bourne Again and Z Shell control structures use decisions to select alternatives are if...then, if...then...else, and if...then...elif. The case control structure provides a multiway branch and can be used when you want to express alternatives, using a simple pattern-matching syntax.