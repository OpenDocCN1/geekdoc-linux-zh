
```
$ unscramble
Picked out a word!

You need to unscramble: ninrenoccg

Your guess (quit|next) : concerning

*** You got it with tries = 1! Well done!! ***

Picked out a word!

You need to unscramble: esivrmipod

Your guess (quit|next) : quit
The unscrambled word was "improvised". Your tries: 0
Done. You correctly figured out 1 out of 2 scrambled words.
```

### 清单 12-2：运行 `unscramble` shell 脚本游戏

显然，第一次猜对是凭借灵感的！

#### 修改脚本

如果能有某种给出提示的方法，这个游戏会更有趣；同样，如果有一个标志用来指定可接受的最短单词长度，也会更好。要实现前者，或许可以显示未乱序单词的前 `n` 个字母，但在计分上给予一定的惩罚；每请求一次提示，就多显示一个字母。要实现后者，你需要一个扩充的单词词典，因为脚本自带的词典最短单词长度为 `10` 个字母——挺有难度的！

### #84 刽子手：在太晚之前猜出单词

刽子手是一种带有阴森隐喻的文字游戏，但它仍是一款有趣的经典游戏。在游戏中，你猜测哪些字母可能出现在隐藏单词里；每猜错一次，吊在绞刑架上的那个人就会被多画出身体的一个部位。错误太多，这个人就会被完全画出来，所以你不仅输了，而且，嗯，你大概也活不成了。这后果实在有点严厉！

#### The Code

```bash
#!/bin/bash
# hangman - a simple version of the hangman game. Instead of showing a
# gradually embodied hanging man, this simply has a bad-guess countdown.
# You can optionally indicate the initial distance from the gallows as
# the only argument.

wordlib="/usr/lib/games/long-words.txt"
empty="."   # We need something for the sed [set] when $guessed=".
games=0

# Start by testing for our word library datafile.

if [ ! -r "$wordlib" ] ; then
echo "Sorry: Missing word library $wordlib" >&2
echo "(online: http://www.intuitive.com/wicked/examples/long-words.txt)" >&2
echo "save the file as $wordlib and you're ready to play!" >&2
exit 1
fi

# The big while loop. This is where everything happens.

while [ "$guess" != "quit" ] ; do
    match="$(randomquote $wordlib)"   # Pick a new word from the library.

if [ $games -gt 0 ] ; then
echo ""
echo "*** New Game! ***"
fi

games="$(( $games + 1 ))"
guessed="" ; guess="" ; bad=${1:-6}
partial="$(echo $match | sed "s/[^$empty${guessed}]/_/g")"

# The guess -> analyze -> show results -> loop happens in this block.

while [ "$guess" != "$match" -a "$guess" != "quit" ] ; do

echo ""
if [ ! -z "$guessed" ] ; then  # Remember, ! -z means "is not empty".
/bin/echo -n "guessed: $guessed, "
fi
echo "steps from gallows: $bad, word so far: $partial"

/bin/echo -n "Guess a letter: "
read guess
echo ""
if [ "$guess" = "$match" ] ; then  # Got it!
 echo "You got it!"
 elif [ "$guess" = "quit" ] ; then  # You're out? Okay.
  exit 0
 # Now we need to validate the guess with various filters.
 elif [ $(echo $guess | wc -c | sed 's/[[:space:]]//g') -ne 2 ] ; then
  echo "Uh oh: You can only guess a single letter at a time"
 elif [ ! -z "$(echo $guess | sed 's/[[:lower:]]//g')" ] ; then
  echo "Uh oh: Please only use lowercase letters for your guesses"
 elif [ -z "$(echo $guess | sed "s/[$empty$guessed]//g")" ] ; then
  echo "Uh oh: You have already tried $guess"
 # Now we can actually see if the letter appears in the word.
 elif [ "$(echo $match | sed "s/$guess//g")" != "$match" ] ; then
  guessed="$guessed$guess"
  partial="$(echo $match | sed "s/[^$empty$guessed]/_/g")"
  if [ "$partial" = "$match" ] ; then
   echo "*** You've been pardoned!! Well done! The word was \"$match\"."
   guess="$match"
  else
   echo "* Great! The letter \"$guess\" appears in the word!"
  fi
 elif [ $bad -eq 1 ] ; then
  echo "*** Uh oh: you've run out of steps. You're on the platform..."
  echo "*** The word you were trying to guess was \"$match\""
  guess="$match"
 else
  echo "* Nope, \"$guess\" does not appear in the word."
  guessed="$guessed$guess"
  bad=$(($bad - 1 ))
 fi
done
exit 0
```

*Listing 12-3: The hangman shell script game*

#### How It Works

The tests in this script are all interesting and worth examination. Consider the test at ① that checks whether the player has entered more than a single letter as a guess.

Why test for the value `2` rather than `1`? Because the entered value has a carriage return from when the user hit ENTER `which is a character, \n`, it has two letters if it's correct, not one. The `sed` in this statement strips out all non-space values, of course, to avoid any confusion with the leading tab that `wc` likes to emit.
