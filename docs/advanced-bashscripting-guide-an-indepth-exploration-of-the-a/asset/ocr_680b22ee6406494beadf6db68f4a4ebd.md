# Chapter 30. Debugging

The Bash shell contains no debugger, nor even any debugging-specific commands or constructs. Syntax errors or outright typos in the script generate cryptic error messages that are often of no help in debugging a non-functional script.

# Example 30–1. A buggy script

```
#!/bin/bash
# ex74.sh

# This is a buggy script.

a=37

if [$a -gt 27 ]
then
  echo $a
fi

exit 0
```

Output from script:

```
./ex74.sh: [37]: command not found
```

What's wrong with the above script (hint: the **if**)?

What if the script executes, but does not work as expected? *This is all the too familiar logic error.*

# Example 30–2. test24, another buggy script

```
#!/bin/bash
# This is supposed to delete all filenames in current directory
# containing embedded spaces.
# It doesn't work. Why not?

badname=$(ls | grep ' 'n
# echo "$badname"
rm "$badname"

exit 0
```

Try to find out what's wrong with Example 30–2 by uncommenting the **echo "$badname"** line. Echo statements are useful for seeing whether you expect is actually what you get.

In this particular case, **rm "$badname"** will not give the desired results because $badname should not be quoted. Ploting it in quotes ensures that **rm** has only one argument (it will match only one filename). A