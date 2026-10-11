site needs to follow. So, an export statement looks like the following as it is broken down further:

```
path who(how)
```

When designating who has access to the information, use one of the formats listed in Table 17.1.

A special item not included in Table 17.1 is =public. You have to use this who setting differently from the others. The following two lines have to be in a file if you want to declare a directory to be a publicly mountable NFS export:

```
path -public
path (how)
```

This example also illustrates how to set a rule that applies to everyone. If you have the how information displayed with no who information associated with it, it is assumed you mean that no limits exist on who can access this export.

When designating the how portion of an export rule, use the options listed in Table 17.2.

Putting all of these together results in interesting structures. The following revisits the general format for an export rule with all the pieces in place:

```
path who1(how1) who2(how2) ... whoN(howN)
```

Any how item that consists of more than one option is used in this format:

```
(option1,option2,....,optionN)
```

Table 17.1 Formats available to designate who is allowed access in /etc/exports.