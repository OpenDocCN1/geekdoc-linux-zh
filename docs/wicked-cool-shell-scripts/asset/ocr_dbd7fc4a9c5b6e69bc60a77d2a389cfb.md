# The Results

```
$ library-test
First off, do you have echo in your PATH? (1=yes, 2=no) 1
The echo command is in the PATH.

Enter a year you think might be a leap year: 432423
Your value is too big: largest acceptable value is 9999.
Please enter a year in the correct format: 432
You're right! 432 is a leap year.
```

# Listing 1-29: Running the library-test script

On your screen, the error messages for a value that is too large will be in bold. Also, the correct guess of a leap year will be displayed in green.

Historically, 432 wasn't a leap year because leap years didn't start appearing in the calendar until 1752. But we're talking about shell scripts, not calendar hacks, so we'll let this slide.

# #13 Debugging Shell Scripts

Although this section doesn't contain a true script per se, we want to spend a few pages talking about some basics of debugging shell scripts, because it's a sure bet that bugs are always going to creep in!

In our experience, the best debugging strategy is to build scripts incrementally. Some script programmers have a high degree of optimism that everything will work right the first time, but starting small can really help move things along. Additionally, you should make liberal use of echo statements to track variables and invoke your scripts explicitly using bash -x to display debugging output, like so:

```
$ bash -x myscript.sh
```

Alternatively, you can run set -x beforehand to enable debugging and set +x afterward to stop it, as shown here:

```
$ set -x
$ ./myscript.sh
$ set +x
```

To see the -x and +x sequences in action, let's debug a simple number-guessing game, shown in Listing 1-30.

# The Code

```
#!/bin/bash
# hi low--A simple number-guessing game

biggest=100        # Maximum number possible
guess=0            # Guessed by player
```