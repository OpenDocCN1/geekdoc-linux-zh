second call expands into two parameters, with the first parameter consisting of a character string with three words. The last call expands into a total of four individual words. If you write more substantial shell scripts with functions and nested calls, this information can be very useful.

```
(Linux): $ echo $second() { $1 $2 $* $3 $* $* }
(Linux): $ first() { "*"; second $4"; second $3 }
(Linux): $ first "Here I am "again" *
Here I am * *
Here I am again *
Here * I am again)
(Linux): "$IFS/*"
(Linux): $first Here/I am again
Here/I/am again *
Here/I/am again *
Here * I am again *
```

**Listing 10.56** Expansion of parameters and IFS.

Some variables are preset by the shell or the system and can be used in login scripts or in personalized programs. A non-exhaustive overview can be found in Table 10.6. Special mention must be made of the variable IFS (Internal Field Separator). This variable determines, for example, if and where the shell separates parameters. The last call in Listing 10.56 shows a simple example.

| Variable | Meaning |
|---|---|
| HOME | Home directory (sometimes also indicated as tilde (~)) |
| PATH | Search path for programs |
| USER | The user name |
| LOGNAME | The login name |
| SHELL | The shell used |
| PS1 | Definition of the prompt |
| MAIL | The mailbox file |
| IFS | Internal field separator |

**Table 10.6** Preset shell variables.

There are further peculiarities in the expansion of variables. If the variables are to be followed immediately by additional text, the variable name must be enclosed in curly brackets (${PS1}text).