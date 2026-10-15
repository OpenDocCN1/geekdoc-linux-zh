
guessed: eioum, steps from gallows: 5, word so far: -e--e--iou--
Guess a letter: n
* Great! The letter "n" appears in the word!

guessed: eioumn, steps from gallows: 5, word so far: -en-en-iou--
Guess a letter: r
* Nope, "r" does not appear in the word.

guessed: eioumnr, steps from gallows: 4, word so far: -en-en-iou--
Guess a letter: s
* Great! The letter "s" appears in the word!

guessed: eioumnrs, steps from gallows: 4, word so far: sen-en-ious--
Guess a letter: t
* Great! The letter "t" appears in the word!

guessed: eioumnrst, steps from gallows: 4, word so far: sententious--
Guess a letter: l
* Great! The letter "l" appears in the word!

guessed: eioumnrstl, steps from gallows: 4, word so far: sententiousl-
Guess a letter: y
** You’ve been pardoned!! Well done! The word was "sententiously".
*** New Game! ***
steps from gallows: 6, word so far: ---------
Guess a letter: quit

Listing 12-4: Playing the hangman shell script game

## Hacking the Script

Obviously it’s difficult to have the guy-hanging-on-the-gallows graphic with a shell script, so we use the alternative of counting "steps to the gallows." If you were motivated, however, you could probably have a series of predefined "text" graphics, one for each step, and output them as the game proceeds. Or you could choose a nonviolent alternative of some sort!

Note that it is possible to pick the same word twice, but with the default word list containing 2,882 different words, there’s not much chance of that. If this is a concern, however, the line where the word is chosen could also save all previous words in a variable and screen against them to ensure that there aren’t any repeats.

Finally, if you’re motivated, it’d be nice to have the guessed-letters list sorted alphabetically. There are a couple of approaches to this, but we’d use sed|sort.

## #85 A State Capitals Quiz

Once you have a tool for choosing a line randomly from a file, there’s no limit to the types of quiz games you can write. We’ve pulled together a list of the capitals of all 50 states in the United States, available for download from http://www.no starch.com/wcs2/. Save the file state.capitals.txt in your /usr/lib/games directory. The script in Listing 12-5 randomly chooses a line from the file, shows the state, and asks the user to enter the matching capital.

### The Code

```
#!/bin/bash
# states--A state capital guessing game. Requires the state capitals
# data file state.capitals.txt.

db="/usr/lib/games/state.capitals.txt"   # Format is State[tab]City.

if [ ! -r "$db" ] ; then
  echo "So: Can’t open $db for reading." >&2
echo "(get state.capitals.txt" >&2
echo "save the file as $db and you’re ready to play!)" >&2
exit 1
fi

guesses=0; correct=0; total=0

while [ "$guess" != "quit" ] ; do

  thiskey="$(randomquote $db)"

  # $thiskey is the selected line. Now let’s grab state and city info, and
  # then also have "match" as the all-lowercase version of the city name.
  state="$(echo $thiskey | cut -d\t -f1 | sed 's/-/ /g')"
  city="$(echo $thiskey | cut -d\t -f2 | sed 's/-/ /g')"
  match="$(echo $city | tr '[:upper:]' '[:lower:]')"

guess=""; total=$(( $total + 1 ));

echo ""
echo "What city is the capital of $state?"

# Main loop where all the action takes place. Script loops until
# city is correctly guessed or the user types "next" to
# skip this one or "quit" to quit the game.

while [ "$guess" != "$match" -a "$guess" != "next" -a "$guess" != "quit" ]
do
  /bin/echo -n "Answer: "
  read guess
```

```
if [ "$guess" = "$match" -o "$guess" = "$city" ] ; then
    echo ""
    echo "*** Absolutely correct! Well done! ***"
    correct=$(($correct + 1))
    guess=$match
elif [ "$guess" = "next" -o "$guess" = "quit" ] ; then
    echo ""
    echo "$city is the capital of $state."  # What you SHOULD have known :)
else
    echo "I'm afraid that's not correct."
fi
done

done
echo "You got $correct out of $total presented."
exit 0
```

Listing 12-5: The states trivia game shell script

### How It Works

For such an entertaining game, states involves very simple scripting. The data file contains state/capital pairs, with all spaces in the state and capital names replaced with dashes and the two fields separated by a single space. As a result, extracting the city and state names from the data is easy.

Each guess is compared against both the all-lowercase version of the city name (match) and the correctly capitalized city name to see whether it's correct. If not, the guess is compared against the two command words next and quit. If either matches, the script shows the answer and either prompts for another state or quits, as appropriate. If there are no matches, the guess is considered incorrect.

### Running the Script

This script has no arguments or command flags. Just start it up and play!

### The Results

Ready to quiz yourself on state capitals? Listing 12-6 shows our state capital trivia skills in action!

```
$ states

What city is the capital of Indiana?
Answer: Bloomington
I'm afraid that's not correct.
Answer: Indianapolis

*** Absolutely correct! Well done! ***
```
