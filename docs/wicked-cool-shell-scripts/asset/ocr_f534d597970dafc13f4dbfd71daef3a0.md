```
guesses=0          # Number of guesses made
number=$(($$ % $biggest ))  # Random number, between 1 and $biggest
echo "Guess a number between 1 and $biggest"

while [ "$guess" -ne $number ] ; do
  /bin/echo -n "Guess? " ; read answer
  if [ "$guess" -lt $number ] ; then
    echo "... bigger!"
  elif [ "$guess" -gt $number ] ; then
    echo "... smaller!"
  fi
  guesses=$(($guesses + 1))
done

echo "Right!! Guessed $number in $guesses guesses."

exit 0
```

> Listing 1-30: The hi low script, which may contain a few errors in need of debugging . . .

# How It Works

To understand how the random number portion at ① works, keep in mind that the sequence $$ is the processor ID (PID) of the shell that runs the script, typically a 5- or 6-digit value. Each time you run the script, it gets a different PID. The % $biggest sequence then divides the PID value by the specified biggest acceptable value and returns the remainder. In other words, 5 % 4 = 1, as does 41 % 4. It’s an easy way to produce a semi-random number between 1 and $biggest.

# Running the Script

The first step in debugging this game is to test and ensure that the number generated will be sufficiently random. To do this, we take the PID of the shell in which the script is run, using the $$ notation, and reduce it to a usable range using the % mod function ①. To test the function, enter the commands into the shell directly, as shown here:

```
$ echo $(($$ % 100 ))
5
$ echo $(($$ % 100 ))
5
$ echo $(($$ % 100 ))
5
```

This worked, but it’s not very random. A moment’s thought reveals why: when the command is run directly on the command line, the PID is always the same; but when run in a script, the command is in a different subshell each time, so the PID varies.