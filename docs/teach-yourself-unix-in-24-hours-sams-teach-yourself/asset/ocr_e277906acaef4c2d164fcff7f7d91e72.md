# ACTION

1. The easy searches with grep are those that search for specific words without any
special regular expression notation:

```
% grep /etc/passwd
taylorj?:1048:1375:James Taylor:/users/taylorj:/bin/csh
maylorj?:769:1375:Melanie Taylor:/users/mtaylor:/usr/local/bin/csh
daylorj?:375:1618:Dave Taylor:/users/taylorj:/usr/local/lib/msh
taylorrj?:203:1022:James Taylor:/users/taylorrj:/bin/csh
taylorrj?:662:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylorm?:869:1508:Melanie Taylor:/users/taylorm:/bin/csh
taylorj?:1989:1412:Dave Taylor:/users/taylorj:/bin/csh
```

I searched for all entries in the passwd file that contain the pattern taylor.

2. I've found more matches than I wanted, though I don't want to see all alternatives. If I'm looking for my ^ character before the left-roots the pattern:

```
% grep "*taylor*" /etc/passwd
taylorj?:1048:1375:James Taylor:/users/taylorj:/bin/csh
taylorrj?:203:1022:James Taylor:/users/taylorrj:/bin/csh
taylorrj?:662:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylorm?:869:1508:Melanie Taylor:/users/taylorm:/bin/csh
taylorj?:1989:1412:Dave Taylor:/users/taylorj:/bin/csxh
```

Now I want to narrow the search. I want to specify a pattern that says
show me all lines that start with taylor, followed by a character that is not a\lowercase letter.

3. To accomplish this, I use the [~xy] notation, which indicates an exclusion set or of characters that cannot match:

```
% grep "^taylor[^a-z]" /etc/passwd
taylorj?:1048:1375:James Taylor:/users/taylorj:/bin/csh
taylorrj?:1989:1412:Dave Taylor:/users/taylorj:/bin/csh
```

It worked! You can specify two ways: You either list each character or use
h hyphen to specify a starting character with the left of the hyphen and
ending with the character to the right of the hyphen. That is, a-z is the range
beginning with a and ending with z, and 0-9 includes all digits.

4. To see which accounts were excluded, remove the ^ for an inclusion range,
which is a set of characters which one pattern must match:

```
% grep "^taylor[a-z]"" /etc/passwd
taylorj?:1048:1375:James Taylor:/users/taylorj:/bin/csh
taylorrj?:203:1022:James Taylor:/users/taylorrj:/bin/csh
taylorrj?:662:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylormx?:869:1508:Melanie Taylor:/users/taylorm:/bin/csh
```

![](bbox=[0.065, 0.883, 0.135, 0.933])