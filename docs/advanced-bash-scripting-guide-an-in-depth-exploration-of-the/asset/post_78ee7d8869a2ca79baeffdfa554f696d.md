
# Advanced Bash-Scripting Guide

```
echo $BLANK80
done

# Set foreground color to black.
echo -ne '\E[30m'
tput cup 5 0

# Draw the fences.
echo "----------------------------------------"
echo "----------------------------------------"
tput cup 15 0
echo "----------------------------------------"
echo "----------------------------------------"

# Set foreground and background colors to white.
echo -ne '\E[37;47m'

# Draw three white lines.
for n in `seq 3`; do
    echo $BLANK80
done

# Set foreground color to black.
echo -ne '\E[30m'

# Create 9 files to stores handicaps.
for n in `seq 10 7 68`; do
    touch $n
done

# Set the first type of "horse" script will draw.
HORSE_TYPE=2

# Create position-file and odds-file for every "horse".
# In these files, store the current position of the horse,
# the type and the odds.
for HN in `seq 9`; do
    touch horse_${HN}_position
    touch odds_${HN}
    echo -1 > horse_${HN}
    echo $HORSE_TYPE >> horse_${HN}
    # Define a random handicap for horse.
    HANDICAP=$(random_1_9)
    # Check if the random_1 returned a good value.
    while $HANDICAP [1-9] & /dev/null; do
        HANDICAP=$(random_1_9)
    done
    # Define last handicap position for horse.
    LHP=$(expr $HANDICAP * 7 + 3)
    for FILE in `seq 10 7 $LHP`; do
        echo $HN >> $FILE
    done

    # Calculate odds.
    case $HANDICAP in
        1) ODDS=`echo $HANDICAP * 0.25 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        2) ODDS=`echo $HANDICAP * 0.40 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        4 | 5) ODDS=`echo $HANDICAP * 0.55 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        7 | 8) ODDS=`echo $HANDICAP * 0.75 + 1.25 | bc`
           echo $ODDS > odds_${HN}

        9) ODDS=`echo $HANDICAP * 0.90 + 1.25 | bc`
           echo $ODDS > odds_${HN}
    esac
done
```

```bash
# Print odds.
print_odds() {
    tput cup 6 0
    echo -ne '\E[30;42m'
    for HN in seq 9; do
        echo "#$HN odds_${HN}"
    done
}
```

```bash
# Draw the horses at starting line.
draw_horses() {
    tput cup 6 0
    echo -ne '\E[30;42m'
    for HN in seq 9; do
        echo "\\"
    done
}
```

```bash
print_odds
echo -ne '\E[47m'
# Wait for an enter key press to start the race.
# The escape sequence '\E[25l' disables the cursor.
tput cup 17 0
echo -e "\E[25l]Press key to start the race..."
read -s
```

```bash
# Disable normal echoing in the terminal.
# This avoids key presses that might "contaminate" the screen
# during the race.

# Start the race.
draw_horses
echo -ne '\E[37;47m'
move_and_echo 18 1 $BLANK80
echo -ne '\E[30m'
move_and_echo 18 1 Starting...
sleep 1

# Set the column of the finish line.
WINNING_POS=74

# Define the time the race started.
START_TIME=`date +s`

# COL variable needed by following "while" construct.
COL=0

while [ $COL -lt $WINNING_POS ]; do
  MOVE_HORSE=0

  # Check if the random_1_9 function has returned a good value.
  while echo $MOVE_HORSE | grep [1-9] & /dev/null; do
    MOVE_HORSE=$(random_1_9)
  done

  # Define old type and position of the "randomized horse".
  HORSE_TYPE=$(cat horse_${MOVE_HORSE}_position | tail -n 1)
  COL=$(expr `cat horse_${MOVE_HORSE}_position | head -n 1`)

  ADD_POS=1
  # Check if the current position is an handicap position.
  if seq 10 7 6 | grep -w $COL & /dev/null; then
    if grep -w $MOVE_HORSE $COL > /dev/null; then
      ADD_POS=0
      grep -w $MOVE_HORSE $COL > ${COL}_new
      rm -f ${COL}_new
    else
      ADD_POS=1
    fi
  else
    ADD_POS=1
  fi
  COL=$(expr $COL + $ADD_POS)
  echo $COL > horse_${MOVE_HORSE}_position # Store position.

  # Choose the type of horse to draw.
  case $HORSE_TYPE in
    1) HORSE_TYPE=2; DRAW_horse=draw_two
    2) HORSE_TYPE=1; DRAW_horse=draw_one
  esac
  echo $HORSE_TYPE >> horse_${MOVE_HORSE}_position # Store current type.

  # Set foreground color to black and background to green.
  echo -ne '\E[30;42m'

  # Move the cursor to next horse position.
  tput cup $(expr $MOVE_HORSE + 5)
  cat horse_${MOVE_HORSE}_position | head -n 1
  # Draw the horse.
  $DRAW_horse
  sleep 1

  # When all horses have gone beyond line 15, reprint odds.
  touch field15
  if [ $COL -eq 15 ]; then
    echo $MOVE_HORSE >> field15
  fi
  if [ `wc -l field15 | cut -d " " -f1` -eq 9 ]; then
    print_odds
    rm field15
  fi

  # Define the horse.
  HIGHEST_POS=$(cat *position | sort -n | tail -1)

  # Set background color to white.
  echo -ne '\E[47m'
  tput cup 17
  echo -n Current leader: $(grep -w $HIGHEST_POS *position | cut -c7-)

  # Define the time the race finished.
  FINISH_TIME=$(date +%s)

  # Set background color to green and enable blinking text.
  echo -ne '\E[30;42m'
  echo -ne '\E[5m'

  # Make the winning horse blink.
  tput cup $(expr $MOVE_HORSE + 5)
  cat horse_${MOVE_HORSE}_position | head -n 1
  $DRAW_horse

  # Disable blinking text.
  echo -ne '\E[25m'

  # Set foreground and background color to white.
  echo -ne '\E[37;44m'
  move_and_echo 18 1 $BLANK80

  # Set foreground color to black.
  echo -ne '\E[30m'

  # Make winner blink.
  tput cup 17 0
  echo -ne '\E[5mWINNER:$MOVE_HORSE\E[0m] Odds: Race time: $(expr $FINISH_TIME - $START_TIME) secs'

  # Restore cursor and old colors.
  echo -ne '\E[25m'
  echo -ne '\E[0m'

  # Restore echoing.
  stty echo

  # Remove race temp directory.
  rm -rf $HORSE_TMP_DIR

tput cup 19 0

exit 0

See Example A-21, Example A-44, Example A-52, Example A-40.

There is, however, a major problem with all: ANSI escape sequences are emphatically non-portable. What works on some terminals (or the console) may work differently, or not at all, on others. A "colored" script that looks stunning on the screen's author's machine may produce unreadable output on others. This somewhat compromises the usefulness of coloring scripts, and possibly relegates the technique to the status of a gimmick. Colorized scripts are probably inappropriate in a commercial setting, i.e., your supervisor might disapprove.

Alister's ansi-color utility (based on Moshe Jacobson's color utility) considerably simplifies using ANSI escape sequences. It substitutes a clean and logical syntax for the clumsy constructs just discussed.

Henry/teikedvl has created a utility (http://scriptecholor.sourceforge.net/) to simplify creation of colorized scripts.

## 36.6. Optimizations

Most shells are quick solutions to non-complex problems. As such, optimizing them for speed is not much of an issue. Consider the case, though, where a script carries out an important task, does it well, but runs too slowly. Rewriting it in a compiled language may not be a palatable option. The simplest fix is to rewrite the parts of the script that slow down. Is it possible to apply principles of code optimization even for a lowly script?

- Check the loops in script. Time consumed by repetitive operations adds up quickly. If at all possible, remove time-consuming operations within loops.
- Use builtin commands in preference to system commands. Builtins execute faster and usually do not launch a subshell when invoked.
- Avoid unnecessary commands, particularly in a pipe.

```
cat "$file" | grep "$word"
grep "$word" "$file"

# The above command-lines have an identical effect,
# but the second runs faster since it launches one fewer subprocess.
The cat command seems especially prone to overuse in scripts.
```
