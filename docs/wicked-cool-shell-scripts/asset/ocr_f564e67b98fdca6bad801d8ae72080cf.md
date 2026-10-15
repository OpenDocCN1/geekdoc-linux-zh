We include the complicated sequence of sed substitutions at the end of this block because it's not a well-formed list: there are one-word names (Fiona) and two-word names (Bad News), but spaces are also used to create the columnar data. To solve this problem, the first space in each line is converted into an underscore and all other spaces are then removed. If the voice has a single-word name, it will then look like this: "Ralph_", and the final sed substitution will remove any trailing underscores. At the end of this process, two-word names have an underscore, so they'll need to be fixed when output to the user. However, the code has the nice side effect of making the while loop a lot easier to write with the default space-as-separator.

The other fun segment is where each voice introduces itself in sequence—the sayit demo invocation—at 9.

This is all quite easy, once you understand how the say command itself works.

# Running the Script

Since this script produces audio, there's not much you can see here in the book, and since we don't yet have the audiobook of Wicked Cool Shell Scripts (can you imagine all the things you wouldn't see?), you'll need to do some of this yourself to experience the results. But the script's ability to list all the installed voices can be demonstrated, as in Listing 13-11.

# The Results

```
$ sayit -d
Available voices: Agnes, Albert, Alex, Bad News, Bahh, Bells, Boing,
Bruce, Bubbles, Cellos, Daniel, Deranged, Fred, Good News, Hysterical,
Junior, Karen, Kathy, Moira, Pipe Organ, Princess, Ralph, Samantha,
Tessa, Trinoids, Veena, Vicki, Victoria, Whisper, Zarvox
HANDY TIP: use "sayit.sh demo" to hear all the different voices
$ sayit "Yo, yo, dog! Whassup?"
$ sayit -v "Pipe Organ" -r 60 "Yo, yo, dog! Whassup?"
$ sayit -v "Ralph" -r 80 -f alice.txt
```

Listing 13-11: Running the sayit script to print supported voices and then speak

# Hacking the Script

A close examination of the output of say -v \? reveals that there's at least one voice where the language encoding is wrong. Fiona is listed as en-scotland, not en_scotland, which would be more consistent (given that Moira is listed as en_IE, not en-irish or en-ireland). An easy hack is to have the script work with both en_ and en-. Otherwise, dabble with it and think about when it could be useful to have a script—or daemon—talk to you.