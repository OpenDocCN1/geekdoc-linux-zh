```
# It's not really a shuffle. It's a random extraction of card values
#  from the 'deck' array, creating newdeck[] as the "shuffled" deck.

count=1

while [ $count != 53 ]
do
    pickCard
    newdeck[$count]=$picked
    count=$(($count + 1))
done

function pickCard
{
# This is the most interesting function: pick a random card from
#  the deck. Uses the deck[] array to find an available card slot.

local errcount randomcard

threshold=10    # Max guesses for a card before we fall through
errcount=0

# Randomly pick a card that hasn't already been pulled from the deck
#  a max of $threshold times. Fall through on fail (to avoid a possible
#  infinite loop where it keeps guessing the same already dealt card).

while [ $errcount -lt $threshold ]
do
    randomcard=$(($RANDOM % 52 + 1))
    errcount=$(($errcount + 1))

    if [ ${deck[$randomcard]} -ne 0 ] ; then
        picked=${deck[$randomcard]}
        deck[$picked]=0   # Picked--remove it.
        return $picked
    fi
done

# If we get here, we've been unable to randomly pick a card, so we'll
#  just step through the array until we find an available card.

randomcard=1

while [ ${newdeck[$randomcard]} -eq 0 ]
do
    randomcard=$(($randomcard + 1))
done

picked=$randomcard
deck[$picked]=0     # Picked--remove it.

return $picked
}
```