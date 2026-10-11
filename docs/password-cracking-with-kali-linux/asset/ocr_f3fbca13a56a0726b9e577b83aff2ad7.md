# CREATING A KWP WORDLIST

To create a simple kwp wordlist, we will use the English keymap and the “2-10 max 3 directional changes” route file, as seen below:

```
`$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-10-max-3-directional-changes.route`
```

This causes kwp to create multiple keymap walk combinations, of 2- 11 characters with a maximum of 3 direction changes:

```
bvbnm,..;p0
cxcvbnm,ki8
vcvbnm,.lo9
xzcvcbnm]u7
-[poiuytrf
@poiuytred
8iuytrewqa
9oiuytrews
=][poiuytg
i';lkjhgf v
ikjhgfdsaz
olkjhgfd sx
p;lkjhgf dc
```

The output of the command is sent directly to the screen, so to create an output file you would need to output the command to a text file:

```
`$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-10-max-3-directional-changes.route > basic kwp.txt`
```

You can then use the resultant text file as a wordlist in Hashcat.
To create a more complex wordlist, use one of the larger route files:

```
`$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-16-max-3-directional-changes.route > largekwp.txt`
```