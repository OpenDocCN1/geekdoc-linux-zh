```
RS* < @ S=w> S*         S: $1 < @ $2 .> $3
RS* < @ $]> S*          S: $1 < @ $1 .> $2
RS* < @ S=w> S*         S: $1 < @ $2 .> $3
RS* < @ S*=P> S*        S: $1 < @ $2 $3 .> $4
RS* < @ S* . ,> S*      $1 < @ $2 .> $3
```

```
#==============================================================================
##  Ruleset 4 - Final Output Post-rewriting  ##
#==============================================================================
S4

RS* <@>          S@        handle <> and list:;
# strip trailing dot off possibly canonical name
RS* < @ S+ . ,> S*       $1 < @ $2 > $3

# eliminate internal code — should never get this far!
RS* < @ *LOCAL*> S*      $1 < @ $]> $2

# externalize local domain info
RS* < S+ > S*     $1 $2 $3    defocus
R@ S+: < @ $1 : $+      S: $1 ., $2 .> $3     `route-addr> canonical
Re S*               S@ $1                ... and exit

# UUCP must always be presented in old form
R@< @ S- . UUCP         $2/$1    u@h.uucp <> h:u

# delete duplicate local names
RS* S S=w @ S=w          $1 $2     u@host@host => u@host
```

```
#==============================================================================
##  Ruleset 97 - recanonicalize and call ruleset zero  ##
##  (used for recursive calls)                  ##
#==============================================================================
S97
RS*                 S: S>3 S$
RS*                 S@ S>0 $1

#==============================================================================
##  Ruleset 0 - Parse Address   ##
#==============================================================================
S0

RS*                 S: S>Parse0 $1     initial parsing
R<>                $S}local $: <@>     special case error msgs
```

![](bbox=[0.89, 0.66, 1.0, 0.75])